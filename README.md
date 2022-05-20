# ansible-patch
Patchwork of ansible exercises and workshops.

## Lesson 1

1. Starting from [here](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html)

1. Install Ansible: https://docs.ansible.com/ansible

1. Check your SSH connections
    > Action: check your SSH connections
    Confirm that you can connect using SSH to all the nodes in your inventory using the same username. If necessary, add your public SSH key to the authorized_keys file on those systems.

    Hint: `ssh-copy-id` may help here.

    ```sh
    ansible all -m ping -i etc/ansible/hosts -u clouduser
    ```

## Lesson 2

1. Create a script for installing Quay registry (`tasks/scripts/install-quay.sh`)
1. Create an [inventory file](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#adding-variables-to-inventory) `actual.hosts` with the target hosts, matching the structure of `etc/ansible/hosts`
1. Create a file `registry-data.env`, with the following values:

    ```
    registry_user=...
    registry_pwd=...
    redhat_pull_secret=...
    ```
1. Encrypt the file with 

    ```
    ansible-vault encrypt /absolute/path/to/registry-data.env
    ```

    The command will ask you for a password to encrypt and decrypt the file.

    Note: You can edit it with `ansible-vault edit /absolute/path/to/registry-data.env`

1. If you don't want to pass the Encrypt the file every time you use it, create a file named `registr-data.pwd` with the plaintext passord as its sole content.
 
1. Launch the playbook:

    ```sh
     ansible-playbook \
        -i /absolute/path/to/actual.hosts \
        -u clouduser \
        -M . ./tasks/quay.yaml \
        -e @/absolute/path/to/registry-data.env \
        --vault-password-file /absolute/path/to/registr-data.pwd
    ```

## References 

- [Ansible - Getting Started](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html)
- [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#from-pip)
