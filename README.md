# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM:
'''
import socket
import threading

# ---------------- SERVER ----------------
def server_program():
    server = socket.socket()
    server.bind(('localhost', 8001))
    server.listen(1)

    print("Server is waiting for connection...")

    conn, addr = server.accept()
    print(f"Connected with {addr}")

    while True:
        msg = input("Server Message: ")

        if msg.lower() == 'exit':
            conn.send("Server closed connection".encode())
            break

        conn.send(msg.encode())

        ack = conn.recv(1024).decode()

        if ack:
            print("Client:", ack)
        else:
            break

    conn.close()
    server.close()


# ---------------- CLIENT ----------------
def client_program():
    client = socket.socket()
    client.connect(('localhost', 8001))

    while True:
        data = client.recv(1024).decode()

        if not data:
            break

        print("Server:", data)

        if data.lower() == "server closed connection":
            break

        client.send("Acknowledgement Received from client".encode())

    client.close()


# ---------------- MAIN ----------------
server_thread = threading.Thread(target=server_program)
client_thread = threading.Thread(target=client_program)

server_thread.start()
client_thread.start()

server_thread.join()
client_thread.join()
'''
## OUTPUT:
'''
Connected with ('127.0.0.1', 59663)
Server Message: Hello
Server: Hello
Client: Acknowledgement Received from client
Server Message: How are you
Server: How are you
Client: Acknowledgement Received from client
'''
## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
