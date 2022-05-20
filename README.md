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

# references

