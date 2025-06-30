import socket
import logging
import threading
import requests

# Configure logging
logging.basicConfig(
    filename='honeypot.log',
    level=logging.INFO,
    format='%(asctime)s - %(message)s',
)

HOST = '0.0.0.0'
PORTS = [2222, 2323, 8080]  # Add more ports as needed

def get_geolocation(ip):
    try:
        response = requests.get(f"http://ip-api.com/json/{ip}", timeout=5)
        data = response.json()
        if data['status'] == 'success':
            return f"{data['country']}, {data['regionName']}, {data['city']}"
        else:
            return "Unknown Location"
    except Exception as e:
        return "Geo lookup failed"

def handle_client(conn, addr, port):
    ip = addr[0]
    geo = get_geolocation(ip)
    logging.info(f"[{port}] Connection from {ip} ({geo})")

    conn.sendall(b"Unauthorized access is prohibited.\n")
    try:
        while True:
            data = conn.recv(1024)
            if not data:
                break
            logging.info(f"[{port}] {ip} sent: {data.decode().strip()}")
            conn.sendall(b"Command not accepted.\n")
    except Exception as e:
        logging.error(f"[{port}] Error with {ip}: {e}")
    finally:
        conn.close()

def start_listener(port):
    print(f"Honeypot listening on port {port}")
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        s.bind((HOST, port))
        s.listen()
        while True:
            conn, addr = s.accept()
            threading.Thread(target=handle_client, args=(conn, addr, port), daemon=True).start()

if __name__ == "__main__":
    for port in PORTS:
        threading.Thread(target=start_listener, args=(port,), daemon=True).start()

    # Keep main thread alive
    while True:
        pass
