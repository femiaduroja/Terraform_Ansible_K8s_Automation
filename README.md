# Terraform and Ansible
We are using Terraform for provisioning the intrstructure which include VPC | Internet Gateway | RT | Servers (Ansible & Jenkins)

# Ansible Installation
``` sh
# Create a REDHAT EC2 instance in aws cloud and assigned IAM roles
AmazonEC2FullACCESS
AmazonVPCFullACCESS
$ sudo useradd ansible
$ echo "ansible  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/ansible
$ sudo su - ansible
# Enable PassowrdLogin and assign password to ansible user
$ sudo yum install python3 -y
$ sudo alternatives --set python /usr/bin/python3
# Install pip package manager for for python 
$ sudo yum -y install python3-pip -y
$ pip3 install ansible --user
# install boto aws python SDK use to manages resources in aws cloud
$ pip3 install boto3 --user
```
# Infrastructure as Code: Terraform Installation

``` sh
$ sudo su ansible
 sudo yum install wget git unzip -y
 wget https://releases.hashicorp.com/terraform/0.12.26/terraform_0.12.26_linux_amd64.zip
 sudo unzip terraform_0.12.26_linux_amd64.zip -d /usr/local/bin/
 #Export terraform binary path temporally
 export PATH=$PATH:/usr/local/bin
#Add path permanently for current user.By Exporting path in .bashrc file at end of file.
$ vi .bashrc
   export PATH="$PATH:/usr/local/bin"
# Source .bashrc to reflect for current session
 source ~/.bashrc   
```
# Clone Terraform and Ansible Scripts
``` sh
 git clone https://github.com/LandmakTechnology/Terraform-Ansible-k8s-Automation.git
 cd terraform-ansible-k8s-automation
```
#### <span style="color:orange"> Update Your KEY NAME in variables.tf File Before Executing Terraform Script </span>

# Infrastructure as Code: Terraform
#### Create the Intrstructure (VPC | Subnets | Route Tables | IGW | EC2 Instances etc.)
``` sh
# Initialise to install plugins
$ terraform init terafrom_scripts/
# Validate teffaform scripts
$ terraform validate terafrom_scripts/
# Plan terraform scripts which will list resouce which will be created
$ terraform plan terafrom_scripts/
# Apply to create resources
$ terraform apply --auto-approve terafrom_scripts/
```
# Configuration Management Using Ansible with DYNAMIC INVENTORY
#### Check if DYNAMIC INVENTORY Script is Working
``` sh
$ chmod +x DynamicInventory.py
$ ./DynamicInventory.py
# Ansible command to setup k8s cluste using DynamicInventory.

###### <span style="color:red">Replace \<Pemfile> with your pemfile path in server </span>
```sh
$ ansible-playbook -i DynamicInventory.py site.yml -u ubuntu --private-key=<PemFilePath>  --ssh-common-args "-o StrictHostKeyChecking=no"
```
# DESTROY Infrastructure  
```sh
$ terraform destroy --auto-approve terafrom_scripts/
```
