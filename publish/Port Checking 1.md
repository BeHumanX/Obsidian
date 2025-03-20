Here's some command used in unix based system for port checking

| Command         | Purpose                                       | Example                     |
| --------------- | --------------------------------------------- | --------------------------- |
| `netstat -tuln` | Check all listening ports.                    | `sudo netstat -tuln`        |
| `ss -tuln`      | Modern alternative to `netstat`.              | `sudo ss -tuln`             |
| `nc -zv`        | Check if a specific port is open.             | `nc -zv localhost 80`       |
| `nmap`          | Scan ports on a host.                         | `sudo nmap -p 80 localhost` |
| `lsof -i`       | Check which process is using a port.          | `sudo lsof -i :80`          |
| `fuser`         | Check which process is using a port.          | `sudo fuser 80/tcp`         |
| `ufw status`    | Check firewall rules for open ports (Ubuntu). | `sudo ufw status`           |
