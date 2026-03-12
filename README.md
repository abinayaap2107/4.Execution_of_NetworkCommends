# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## Program
server
```
import socket
import subprocess
import platform

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server listening on port 8000...")
c, addr = s.accept()
print("Connected:", addr)

while True:
    command = c.recv(1024).decode().strip()
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:
        # Run ANY command the client sends
        completed = subprocess.run(
            command, 
            capture_output=True, 
            text=True, 
            shell=True
        )
        output = completed.stdout + (completed.stderr or "")
    except Exception as e:
        output = f"Command failed: {e}"

    c.sendall(output.encode('utf-8'))

c.close()
s.close()

```
client
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

print("Connected. Type any network command (ipconfig, ping, etc.) or 'exit'.")

while True:
    cmd = input("Enter command: ").strip()
    if not cmd:
        continue

    s.send(cmd.encode('utf-8'))
    
    if cmd.lower() == "exit":
        print("Exiting...")
        break

    output = s.recv(65536).decode()
    print("\n----- RESULT -----")
    print(output)
    print("------------------\n")

s.close()

```

## Output
<img width="1920" height="906" alt="Screenshot (59)" src="https://github.com/user-attachments/assets/57f4471f-e2a5-4d1a-a6d8-63aeb34b3754" />
<img width="1920" height="180" alt="Screenshot (60)" src="https://github.com/user-attachments/assets/4e6cebcf-e716-45dd-b267-995df4b3b220" />
<img width="1920" height="880" alt="Screenshot (61)" src="https://github.com/user-attachments/assets/c71129db-f7f6-464c-bf06-66774eabf77b" />
<img width="1920" height="420" alt="Screenshot (62)" src="https://github.com/user-attachments/assets/85d885eb-a3b9-406d-97a9-9c67a63a5f95" />





## Result
Thus Execution of Network commands Performed 
