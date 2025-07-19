## Deploy Azure VM using AZ collection

# Pre-requisites:
1. ENsure Ansible, Python is installed and properly configured.

High Level Steps:
1. Install CLI and ansible[azure] package:

$ pip3 install ansible[azure]
$ pip3 install azure-cli

2.install galaxy az-collection
$ ansible-galaxy collection install azure.azcollection --force

3. Install recommended modules
sudo pip3 install -r ~/.ansible/collections/ansible_collections/azure/azcollection/requirements.txt

4. login to azure to create service principal
$ az login -> then login

6. Create service principal and add credentials file
az ad sp create-for-rbac --name "ansible-sp" --role="Contributor" --scopes="/subscriptions/<sub-id>" --sdk-auth

now it will return the data , paste the data to adjacent options in ~/.azure/credentials file(a demo file is attached).

You need to print in below format
--------------------------------------------
[default]
subscription_id=
client_id=
secret=
tenant=
--------------------------------------------

7. Test your connection with an adhoc command
$ ansible localhost -m azure.azcollection.azure_rm_resourcegroup -a "name=<name> location=<location>"

8. Now if you want write a playbook. A demo playbook to create a azure vm is attached. (Verified playbook).