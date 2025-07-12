
## Linux firewall basic

> Using *multipass*

```bash

multipass launch --name server1 --disk 10G --memory 1G --cpus 2
multipass launch --name server2 --disk 10G --memory 1G --cpus 2


multipass exec server1 -- bash -c "sudo apt update && sudo apt upgrade -y"
multipass exec server2 -- bash -c "sudo apt update && sudo apt upgrade -y"


multipass exec server1 -- bash -c "sudo apt install nginx -y"

multipass exec server1 -- bash -c "curl localhost"

multipass exec server2 -- bash -c "curl server1"

### Change webpage


multipass exec server1 -- bash -c "echo '<html><body><h1>Hello</h1</body></html>' | sudo tee /var/www/html/index.html"


### Enable the firewall

multipass exec server1 -- bash -c "sudo ufw allow OpenSSH"

multipass exec server1 -- bash -c "sudo ufw --force enable"

multipass exec server1 -- bash -c "sudo ufw status numbered"

multipass exec server1 -- bash -c "sudo ufw --force delete 2"


multipass exec server1 -- bash -c "sudo cat /var/log/ufw.log"

### Whitelist server2 for inbound port 80

SERVER2IP=$(multipass list | grep server2 | column -t | awk '{print $3}')

multipass exec server1 -- bash -c "sudo ufw allow from $SERVER2IP to any port 80"



### Clean up

multipass delete --all --purge

```
