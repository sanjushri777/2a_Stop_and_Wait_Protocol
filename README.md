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
### client.py
```python
import socket
c=socket.socket()
c.connect(('localhost',8000))
frame_size=int(input("Enter the size"))
while True:
    print(f"Frame size is: {frame_size}")
    data=input("enter data upto the above frame size:")
    if data.lower()=='exit':
        c.send(data.encode())
        print("[client]:EXITING...")
        c.close()
        break
    else:
        frame=data[:frame_size]
        c.send(frame.encode())
        ack=c.recv(1024).decode()
        if ack:
            print("ack received")
        else:
            print("no ack received")
            c.close()
            break
```
### server.py
```python
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(1)
print("Server is listening..")
c,addr=s.accept()
print("Connection established with address: ",addr)
while True:
    data=c.recv(1024).decode()
    if data.lower()=='exit':
        print("[SERVER]: client has terminated the session,closing server")
        c.close()
        break
    else:
        print(f"[SERVER]:Recieved from client {data}")
        ack=f"Ack:Received data is' {data}'"
        print(f"[SERVER]: Sending Acknowledgement {ack}")
        c.send(ack.encode())
```
## OUTPUT
![image](https://github.com/user-attachments/assets/4004f1de-363a-4458-a210-89f5999fe95b)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
