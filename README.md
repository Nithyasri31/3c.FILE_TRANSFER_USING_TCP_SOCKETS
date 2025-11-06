# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
server
```
import socket, os

port = 8000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(1)
print("Server listening...")

conn, addr = s.accept()
print("Got connection from", addr)

data = conn.recv(1024)
print("Server received:", data.decode())

# Ensure folder exists
folder = r"C:\Users\admin\Documents\CN EXPS"
os.makedirs(folder, exist_ok=True)

filename = os.path.join(folder, "mytext.txt")
if not os.path.exists(filename):
    with open(filename, "w") as f:
        f.write("This is a test file for transfer.\n")

with open(filename, 'rb') as f:
    while True:
        l = f.read(1024)
        if not l:
            break
        conn.send(l)

print("✅ Done sending file")
conn.close()
```
client
```
import socket, os

s = socket.socket()
host = socket.gethostname()
port = 8000
s.connect((host, port))
s.send("Hello server!".encode())

# Ensure folder exists
folder = r"C:\Users\admin\Documents\CN EXPS"
os.makedirs(folder, exist_ok=True)

received_path = os.path.join(folder, "received_file.txt")
with open(received_path, 'wb') as f:
    while True:
        data = s.recv(1024)
        if not data:
            break
        f.write(data)

print("✅ Successfully received the file at", received_path)
s.close()
```
## OUPUT
<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/7bdb288b-1ee8-442b-93c5-f011a7e93fa8" />
<img width="1576" height="706" alt="Screenshot 2025-11-06 105940" src="https://github.com/user-attachments/assets/42b039fa-db6b-4b3d-9967-1c3dd165e312" />



## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
