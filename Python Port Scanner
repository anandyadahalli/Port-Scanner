import socket
import threading
import re

def scan_port(host, port):
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(5)
        result = sock.connect_ex((host, port))
        if result == 0:
            print("Port", port, "is open.")
        sock.close()
    except socket.timeout:
        print(f'Timeout reached while connecting to port {port}')
    except Exception as e:
        print(f'An error occurred: {e}')

def scan_ports(host, start_port, end_port):
    try:
        if not (1 <= start_port <= 65535) or not (1 <= end_port <= 65535):
            raise ValueError("Ports must be between 1 and 65535")
        if start_port > end_port:
            raise ValueError("Start port must be less than or equal to end port")
        thread_list = []
        for port in range(start_port, end_port+1):
            t = threading.Thread(target=scan_port, args=(host, port))
            thread_list.append(t)
            t.start()
        for t in thread_list:
            t.join()
    except Exception as e:
        print(f'An error occurred: {e}')

while True:
    host = input("Enter host to scan(e.g. www.example.com,192.168.1.1): ")
    if host == "":
        print("Host cannot be empty")
        continue
    pattern = re.compile("^(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\\-]*[a-zA-Z0-9])\\.)*([A-Za-z0-9]|[A-Za-z0-9][A-Za-z0-9\\-]*[A-Za-z0-9])$")
    if not pattern.match(host):
        print("Invalid host")
        continue
    try:
        socket.inet_aton(host)
    except socket.error:
        try:
            socket.gethostbyname(host)
        except socket.gaierror:
            print("Invalid host")
            continue
    try:
        start_port = int(input("Enter start port: "))
        end_port = int(input("Enter end port: "))
    except ValueError:
        print("Port must be a number")
        continue
    scan_ports(host, start_port, end_port)
