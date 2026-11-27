# 2b. IMPLEMENTATION OF SLIDING WINDOW PROTOCOL

## AIM
To implement the Sliding Window Protocol using Python socket programming to control the transmission of multiple frames and ensure reliable data communication between the sender and receiver.

## ALGORITHM
1. Start the program.
2. Get the frame size from the user.
3. Create the frames based on the user request.
4. Get the window size from the user.
5. Send frames to the client from the server side based on the window size.
6. If the frames reach the client, it sends an ACK signal to the server.
7. After receiving ACK, the server sends the next set of frames.
8. Stop the program.

## PROGRAM

### SERVER (server.py)

```python
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)

print("Server waiting for client...")
c, addr = s.accept()

size = int(input("Enter number of frames to send: "))
l = list(range(size))

ws = int(input("Enter Window Size: "))

i = 0

while i < len(l):
    st = i + ws

    print("Sending frames:", l[i:st])
    c.send(str(l[i:st]).encode())

    ack = c.recv(1024).decode()

    if ack:
        print(ack)
        i += ws
    else:
        break

c.close()
s.close()
```

### CLIENT (client.py)

```python
import socket

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

## OUTPUT

<img width="1900" height="1061" alt="Screenshot 2026-11-27 082607" src="https://github.com/user-attachments/assets/a219de0b-17a8-44df-be3d-f519b9ded8e9" />


<br><br><br>

## RESULT

Thus, the Python program to implement the Sliding Window Protocol using socket programming was successfully executed.
