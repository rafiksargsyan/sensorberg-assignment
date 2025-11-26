# sensorberg-assignment
The document describes installation and configuration of Eclipse Mosquitto MQTT
message broker on Rocky 9 Linux using Ansible

Please edit the ```inventory.ini``` file and set the IP address of the machine
where you want to install Mosquitto server. After that run the following command
from the root directory of the repository:

```ansible-playbook -i inventory.ini playbook.yml -u <USERNAME_ON_REMOTE_HOST> -K```

>Please note that for the purpose of easy demonstration ```client.key``` and ```server.key```
are openly included in the repository, while in the production environment they must be
stored in some kind of secret store.

The server certificate has been generated for CN ```sensorberg```. To test the connection
you can use one of the two methods:

- Use the following command (notice ```--insecure``` option), *PEM pass phrase* is ***sensorberg***:
```mosquitto_pub -d -h <REMOTE_HOST_IP> -p 8883 -t "test/status" -m "Broker is up" --cafile ./client/ca.crt --cert ./client/client.crt --key ./client/client.key --insecure```
- Edit your ```/etc/hosts``` file and add ```sensorberg``` hostname for the IP address. Use the following command, *PEM pass phrase* is ***sensorberg***:
  ```mosquitto_pub -d -h sensorberg -p 8883 -t "test/status" -m "Broker is up" --cafile ./client/ca.crt --cert ./client/client.crt --key ./client/client.key```

## High availability setup ideas
