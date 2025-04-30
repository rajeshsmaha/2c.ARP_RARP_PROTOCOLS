# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP

SERVER:

          import socket
          s = socket.socket()
          s.bind(('localhost', 8000))
          s.listen(5)
          print("Server is listening...")
          
          c, addr = s.accept()
          print(f"Connection established with {addr}")
          
          address = {
              "165.165.80.80": "6A:08:AA:C2",
              "165.165.79.1": "8A:BC:E3:FA"
          }
          
          while True:
              ip = c.recv(1024).decode()
          
              if not ip:  
                  break
          
              try:
                  mac = address[ip]  # Get the MAC address for the IP
                  print(f"IP: {ip} -> MAC: {mac}")
                  c.send(mac.encode())  
              except KeyError:
                  print(f"IP: {ip} not found in ARP table.")
                  c.send("Not Found".encode())
          c.close()
          s.close()

CLIENT:

          import socket
          c = socket.socket()
          c.connect(('localhost', 8000))
          
          while True:
              ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")
          
              if ip.lower() == "exit":  
                  break
          
              c.send(ip.encode())
              mac = c.recv(1024).decode()
              print(f"MAC Address for {ip}: {mac}")
          c.close()

## OUPUT - ARP

SERVER:

![image](https://github.com/user-attachments/assets/4fe46d76-4f9f-4d3c-9191-f67ae45309da)

CLIENT:

![image-1](https://github.com/user-attachments/assets/edc92b19-ca1a-4438-8c4b-5a77a14d728e)

## PROGRAM - RARP

SERVER:

          import socket
          s = socket.socket()
          s.bind(('localhost', 8000))
          s.listen(5)
          print("Server is listening for RARP requests...")
          c, addr = s.accept()
          print(f"Connection established with {addr}")
          
          rarp_table = {
              "6A:08:AA:C2": "165.165.80.80",
              "8A:BC:E3:FA": "165.165.79.1"
          }
          
          while True:
              mac = c.recv(1024).decode()
          
              if not mac:  
                  break
          
              try:
                  ip = rarp_table[mac]  
                  print(f"MAC: {mac} -> IP: {ip}")
                  c.send(ip.encode())  
              except KeyError:
                  print(f"MAC: {mac} not found in RARP table.")
                  c.send("Not Found".encode())
          c.close()
          s.close()

CLIENT:

      import socket
      c = socket.socket()
      c.connect(('localhost', 8000))
      
      while True:
          mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
          if mac.lower() == "exit":  
              break
          c.send(mac.encode())
          ip = c.recv(1024).decode()
          print(f"IP Address for {mac}: {ip}")
      c.close()



## OUPUT -RARP

SERVER:

![image-3](https://github.com/user-attachments/assets/cedff050-3e23-455e-96ec-6078b42e3d16)

CLIENT:
![image-2](https://github.com/user-attachments/assets/1d8dd2b3-511c-4429-8f37-c586a086082f)


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
