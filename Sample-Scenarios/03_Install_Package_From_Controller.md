# Subject

we want to setup a `controller node`, and 2 `managed nodes`, and configure our `controller node` to be able to connect to `managed nodes` by ssh key;

the we want to install `nginx` in managed nodes from `controller_node`. so we will do the following steps:

1. setup 2 `managed nodes`.
2. setup `controller node`.
3. setup ssh key in `controller node`.
4. create a host file in `controllel node`.
5. test the ping of `controller node` to `managed nodes`.
6. uninstall `nginx` from managed nodes.
7. install `nginx` in managed nodes.



**Caution:** for steps 1 to 5 refer to link `https://github.com/hamedvalizadeh/ansible-tutorial/blob/master/Sample-Scenarios/01_Setup_A_Simple_Inventory.md`.



# Uninstall Nginx

to be sure that managed `nginx` is installed or not in maned nodes, execute the following command in each of them:

```powershell
sudo apt-cache policy nginx
```



if it was installed, execute the following command to uninstall it:

```powershell
sudo apt purge nginx
```



# Install Nginx

now we can install `nginx` in our managed nodes from controller node; to do so execute the following `ad-hoc` command in controller node:

```powershell
sudo ansible all -i hosts.yaml -m ansible.builtin.yum -a 'name=nginx state=latest' -u hamed --become --ask-become-pass
```



the above command will prompt to ask the password of the the user `hamed`, and then will install the `nginx` package in managed nodes.



**HINT:** the option `--become` means to run this command on managed nodes as `root` user. it will do the job if the user `hamed` is member of `sudoers` group.

