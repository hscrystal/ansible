# Ansible Infrastructure as Code

```shell
ansible-playbook -i ./inventories/<environment> playbook.yml
```

## How to add new Managed Node


### On the new Managed Node

* Install required packages.

    ```shell
    sudo apt install python-minimal aptitude
    ```
    
* Create `ansible` user with a simple password we will set a hard password later.

    ```shell
    sudo adduser ansible
    ```

* Assign `ansible` user into `sudo` group and made `ansible` user no need password when using `sudo` command.

    ```shell
    sudo adduser ansible sudo
    sudo visudo
    # add follwing the at bottom
    ansible ALL=(ALL) NOPASSWD:ALL
    ```
    
### On the Control Machine

* Update inventory file in `./invetories` directory.

* Put ssh public key into new Managed Node.

    ```shell
    ssh-copy-id -i ./ssh_keys/ubuntu.pub ansible@<new-managed-node>
    ```

* Test the connection.

    ```shell
    ansible -i ./inventories/<enviroment> <Managed Node name> -m ping
    ```
    
* Reset `ansible` user password, we don't need any more.
    ```shell
    ssh -i ./ssh_keys/ubuntu  ansible@<new-managed-node> "sudo sh -c 'echo ansible:`gpw 1 13` | chpasswd'"
    ```
