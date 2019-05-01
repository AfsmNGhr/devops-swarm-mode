### ELK

[What is the ELK Stack?](https://www.elastic.co/elk-stack)

Set up firewall for gelf driver of logstach

```sh
sudo ufw allow from $IP to any port 12201 proto udp
```
