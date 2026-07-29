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
## PROGRAM 
server:
```
import socket

# Create socket
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Bind to localhost and port
server.bind(("localhost", 8001))

# Listen for client
server.listen(1)

print("Server is waiting for connection...")

conn, addr = server.accept()
print("Connected by:", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    if data.lower() == "exit":
        print("Client disconnected.")
        break

    print("Frame Received :", data)

    ack = "ACK Received"
    conn.send(ack.encode())
    print("Acknowledgement Sent\n")

conn.close()
server.close()
```
client:
```
import socket
import time

# Create socket
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connect to server
client.connect(("localhost", 8001))

n = int(input("Enter number of frames: "))

for i in range(1, n + 1):
    frame = input(f"Enter data for Frame {i}: ")

    print(f"\nSending Frame {i}...")
    client.send(frame.encode())

    ack = client.recv(1024).decode()
    print("Server:", ack)

    print("Waiting before sending next frame...\n")
    time.sleep(2)

client.send("exit".encode())

client.close()

```
## OUTPUT
server
~~~
<img width="777" height="180" alt="Screenshot 2026-07-29 113653" src="https://github.com/user-attachments/assets/eebd1b8e-f143-47b9-9e05-19391772e0a8" />


~~~
client
<img width="742" height="466" alt="Screenshot 2026-07-29 113518" src="https://github.com/user-attachments/assets/11fcdc15-75eb-4ea6-862e-4169adc072d2" />

~~~

~~~
## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
