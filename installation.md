# Installation

to install the `Ansible` first it is better to install dependencies needed by `Ansible`, so execute the following command:

```powershell
sudo apt install -y software-properties-common
```

 

then it is good idea to introduce the repository to download and install the `Ansible` package from it. so execute the following code:

```powershell
sudo add-apt-repository --yes --update ppa:ansible/ansible
```



now it is good to by executing following command to check which version of `Ansible` is candidate to be installed:

```powershell
sudo apt-cache policy ansible
```



now update repository by running following repository:

```powershell
sudo apt update
```



now to install the `Ansible` execute the following commands:

```powershell
sudo apt install -y ansible
```



# Check The Installation

we can check the version installed by executing following command:

```powershell
sudo ansible --version
```



and to check the functionality, we can run the following `ad-hoc` command:

```powershell
sudo ansible localhost -m ping
```

 

the output of the above command should be a `success` command, something like bellow script:

```yaml
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
} 
```
