# DRCK-Ansible
This repository contains the Ansible scripts used to automate the CD in our CICD pipeline.  
It also contains files required for the script to use.  

Before using the script, generating TLS certificates for the following is required:  
- backend.crt (Server certificate for backend application)
- client.crt (Client certificate for frontend application to communicate with backend application and for backend application to communicate with database application)
- database.crt (Server certificate for database application)

Follow the steps here to generate the certs: [https://www.digitalocean.com/community/tutorials/how-to-set-up-and-configure-a-certificate-authority-ca-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-set-up-and-configure-a-certificate-authority-ca-on-ubuntu-20-04)

What each script is for:  
- deploy_xxx.yaml: deploy the specified application
- cleanup_xxx.yaml: cleanup the directory of the specified application and dependencies.

To run the scripts:  
```
For deploy:
ansible-playbook playbooks/deploy_frontend.yaml -i inventory.yaml -K
ansible-playbook playbooks/deploy_django.yaml -i inventory.yaml -K
ansible-playbook playbooks/deploy_database.yaml -i inventory.yaml -K

For cleanup:
ansible-playbook playbooks/cleanup_frontend.yaml -i inventory.yaml -K
ansible-playbook playbooks/cleanup_django.yaml -i inventory.yaml -K
ansible-playbook playbooks/cleanup_database.yaml -i inventory.yaml -K
```
