Pre-requisites for using AWS collection:
Control node to have -
1. Update unix - sudo apt-get update
2. Ansible - sudo apt-get install ansible
3. Python3 - sudo apt-get install python3
4. Boto3   - sudo apt-get install python3-boto3
5. AWS Collections - ansible-galaxy collection install amazon.aws
6. setup vault - 
  create password for ansible vault - openssl rand -base64 2048 > /home/vault.pass
  add aws accounts creds using      - ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
  e.g ec2_access_key: <>
      ec2_secret_key: <>

Run playbook - 
ansible-playbook -i hosts.ini ec2_create_instances.yaml --vault-password-file /home/vault.pass  //hosts file here can be empty

--------------------------------------------------------------------------------------------------------------------

Pre-requisites for using Ansible modules:
Managed node to have -
1. Update unix - sudo apt-get update
2. Python3 - sudo apt-get install python3

Control node to have -
1. Update unix - sudo apt-get update
2. Ansible - sudo apt-get install ansible
3. Python3 - sudo apt-get install python3
4. Give passwordless access to control node on managed nodes -
   ssh-copy-id -i ~/.ssh/id_rsa.pub -o IdentityFile=~/Downloads/ansible_host.pem ubuntu@3.108.223.143
or
4. run ssh-gen [on both control and managed noded]
   copy public_key [id_rsa.pub] of control node in authorized_keyw file of all managed nodes

Run playbook - 
ansible-playbook -i hosts.ini ec2_shutdown.yml --vault-password-file /home/vault.pass  //provide IP addressed in hosts file

e.g. hosts.ini file
ubuntu@13.233.161.157
ubuntu@3.108.223.143
ec2-user@13.111.214.140


-------------------------------------------------------------------------------------------------------------------
create role and accordingly edit filed in role and refrence it in yaml files -
ansible-galaxy init <role_name>  //this will create various folders like tasks, vars, defaults etc.
