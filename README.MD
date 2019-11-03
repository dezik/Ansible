Ansible configuration

1. Install Ansible
2. Generate ssh keys on remote machine and copy them to host machine:
    `ssh-copy-id -i ~/.ssh/mykey user@host`
3. Try to connect to remote machine by ssh to check if connection don't require password:
    `ssh vagrant@127.0.0.1 -p 2222`
4. Create `inventory` file with configuration of servers:
    `centos ansible_host=127.0.0.1 ansible_port=2222 ansible_user=vagrant`
5. Check if host accessible for Ansible:
    `ansible -i inventory centos -m ping`
6. Create `playbook.yml` file:
    ```yml
    - 
        name: Create file on remote host
        hosts: centos
        tasks:
            - 
                lineinfile:
                    path: /tmp/test.txt
                    create: yes
                    line: put line here
    ```
7. Run playbook:
    `ansible-playbook  -i inventory playbook.yml`



#Tips&Tricks
* To check ansible wide variable which can be used on remote host:
    `ansible -i inventory centos -m setup`
* To create ansible role you need to generate proper folders structure first:
    `ansible-galaxy init mysql`