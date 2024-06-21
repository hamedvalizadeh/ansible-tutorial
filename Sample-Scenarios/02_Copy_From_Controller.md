# Subject

we want to setup a `controller node`, and 2 `managed nodes`, and configure our `controller node` to be able to connect to `managed nodes` by ssh key, and create a directory named `dir_created_by_controller` in managed nodes and then create a file from our controller node to the just created directory in managed nodes. so we will do the following steps:

1. setup 2 `managed nodes`.
2. setup `controller node`.
3. setup ssh key in `controller node`.
4. create a host file in `controllel node`.
5. test the ping of `controller node` to `managed nodes`.
6. create file in controller node named `file_from_controller.txt`.
7. create directory named in managed nodes.
8. copy file from controller node to managed nodes.



**Caution:** for steps 1 to 5 refer to link `https://github.com/hamedvalizadeh/ansible-tutorial/blob/master/Sample-Scenarios/01_Setup_A_Simple_Inventory.md`.



# Create Directory

from controller node execute the following `ad-hoc` command:

```powershell
sudo ansible -i inventory/hosts.yaml all -a "mkdir ~/dir_created_by_from_controller_node"
```



this command will create a directory named `directory_created_by_from_controller_node`, inside the home directory of the the user `mnguser` inside each managed nodes.



# Copy File

first create a directory named `dir_in_controller_node` in the path `~/` inside controller node, and create a file named `file_in_controller_node.txt` in this directory and fill it with the content you want. then execute the following `ad-hoc` command:

```powershell
sudo ansible -i inventory/hosts.yaml all -m copy -a "src=~/dir_in_controller_node/file_in_controller_node.txt dest=~/dir_created_by_from_controller_node/file_from_controller_node.txt"
```

