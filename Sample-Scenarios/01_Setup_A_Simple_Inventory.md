# Subject

we want to setup a `controller node`, and 2 `managed nodes`, and configure our `controller node` to be able to connect to `managed nodes` by ssh key. so we will do the following steps:

1. setup 2 `managed nodes`.
2. setup `controller node`.
3. setup ssh key in `controller node`.
4. create a host file in `controllel node`.
5. test the ping of `controller node` to `managed nodes`.



# Setup Managed Nodes

do the following steps 2 times to setup 2 Linux servers:

1. to setup the server, follow this link `https://github.com/hamedvalizadeh/linux-tutorial/blob/master/Setup.md`.
   - in first iteration, named the server hostname `managed_node_1` (in our example the IP address is `192.168.56.105`).
   - in second iteration, named the server hostname `managed_node_2` (in our example the IP address is `192.168.56.107).
   - in each server create a user with username `mnguser` and password `123` and add the user to `sudo` group by executing the command `adduser mnguser sudo`.
2. to setup ssh capability on each server, follow link `https://github.com/hamedvalizadeh/linux-tutorial/blob/master/ssh.md`. 



# Setup Controller Node

setup the controller node by the help of the document in `https://github.com/hamedvalizadeh/vagrant-tutorial/blob/master/Sample-Scenarios/Simple-VM-Run.md`.

by default the hostname is `vagrant` after you finished the setup process; it is better to rename it to `controllernode` by the help of following command: 

```powershell
sudo hostnamectl set-hostname controller_node_1
```



# Setup SSH key

to have more secure way of connecting to managed nodes from controller node by the help of SSH, we will use ssh key in `controller_node_1`; so follow all sections from section `Generate keys in Client` to the end of document `https://github.com/hamedvalizadeh/linux-tutorial/blob/master/Sample-Scenarios/ssh/ssh-key.md`.



# Create Host File

in the `controller_node_1` server, make a directory named `inventory` and inside it create a file named `hosts.yaml` and copy the following content to it:

```yaml
all:
 children:
   test_servers:
     hosts:
       managed_node_1:
         ansible_host: 192.168.56.105
         ansible_user: mnguser
         ansible_port: 22
         ansible_ssh_private_key_file: /home/vagrant/.ssh/id_rsa
       managed_node_2:
         ansible_host: 192.168.56.107
         ansible_user: mnguser
         ansible_port: 22
         ansible_ssh_private_key_file: /home/vagrant/.ssh/id_rsa
```



# Test the ping

to test every thing is ok and is setup correctly, execute the following `ad-hoc` command:

```powershell
sudo ansible all -i inventory/hosts.yaml -m ping
```



this should result to something like bellow:

```powershell
managed_node_2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
managed_node_1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```



