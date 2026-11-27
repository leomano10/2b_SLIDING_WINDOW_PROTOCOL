# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
server:
```
s = socket.socket()
s.connect(('localhost', 8000))

while True:
    data = s.recv(1024).decode()

    if data:
        print("Received frames:", data)

        s.send("ACK: Frames received".encode())
    else:
        break

s.close()
```
client:
```

import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)

print("Server waiting for client...")
c, addr = s.accept()

while True:
    i = input("Enter a data: ")

    if i.lower() == "exit":
        break

    c.send(i.encode())

    ack = c.recv(1024).decode()

    if ack:
        print("Acknowledgement:", ack)
    else:
        break

c.close()
s.close()
```
## OUPUT
<img width="565" height="435" alt="image" src="https://github.com/user-attachments/assets/1d8e98ff-2b1f-4bb5-a371-4a5891737789" />
<img width="588" height="440" alt="image" src="https://github.com/user-attachments/assets/8817a9bc-49bb-4ff4-b6db-7cdf3ddb9214" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
