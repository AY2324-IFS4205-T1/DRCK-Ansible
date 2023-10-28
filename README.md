# DRCK-Ansible
This repository contains the Ansible scripts used to automate the CD in our CICD pipeline.  
It also contains files required for the script to use.  

Before using the script, the following items are required:  
- backend.crt (TLS Server certificate for backend application)
- backend.key (Private key use to generate the CSR for the backend server certificate)
- client.crt (TLS Client certificate for frontend application to communicate with backend application and for backend application to communicate with database application)
- client.key (Private key use to generate the CSR for the client certificate)
- database.crt (TLS Server certificate for database application)
- database.key (Private key use to generate the CSR for the database server certificate)
- pg15tde.tar.gz (Compiled version of PostgreSQL 15 TDE)

After generating the certs, create a directory call `certs` in `playbooks/files` and put the TLS certificates and the private keys used to generate the certificates in that directory.
After getting the compiled version of PostgreSQL 15 TDE, put the `pg15tde.tar.gz` file in `files/postgresql` directory

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
