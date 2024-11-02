For computer networks project:

For changing the network and connection between client and server : https://youtu.be/DzmUOeFdc-w?si=Gf7LWbr7781mHKoF

The code that should be saved in both client and server as follows:

On server machine:
import socket

# Set the server's IP address (this machine's IP) and port
SERVER_IP = '192.168.56.101'  # Replace with your server machine IP
SERVER_PORT = 12345

def handle_client(client_socket):
    print("Client connected!")
    while True:
        data = client_socket.recv(1024).decode()
        if not data or data == "EXIT":
            print("Client disconnected.")
            break
        print(f"Received from client: {data}")
        response = "Response from server"
        client_socket.sendall(response.encode())

    client_socket.close()

def main():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind((SERVER_IP, SERVER_PORT))
    server_socket.listen(5)
    print(f"Server listening on {SERVER_IP}:{SERVER_PORT}")

    while True:
        client_socket, addr = server_socket.accept()
        print(f"Accepted connection from {addr}")
        handle_client(client_socket)

if _name_ == "_main_":
    main()

On client machine:

import socket

# Set the server's IP address (the IP address of the server machine)
SERVER_IP = '192.168.56.101'  # Replace with your server machine IP
SERVER_PORT = 12345

def main():
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    try:
        client_socket.connect((SERVER_IP, SERVER_PORT))
        print(f"Connected to server {SERVER_IP}:{SERVER_PORT}")

        while True:
            request = input("Enter message (or EXIT to quit): ")
            client_socket.sendall(request.encode())
            if request == "EXIT":
                break
            response = client_socket.recv(1024).decode()
            print(f"Server response: {response}")

    except Exception as e:
        print(f"Error: {e}")

    finally:
        client_socket.close()

if _name_ == "_main_":
    main()

Just change the IP addr according to your machine. Note: In both client and server code, the ip will be same that is server's IP​
