# Leading Path Redis Enterprise Automation Project

## Contact Info
Jonathan DeLanders
jonathan.delanders@theleadingpath.com

## Prerequisites

 - Git
 - Terraform/Packer
 - Ansible
 - Helm / kubectl
 - aws cli

The instructions were tested on a centos 7 machine in aws.   If you are on mac or windows check the links provided in each section which have thorough documentation for each platform.   If you want we can launch you a node in aws to work with also.   Contact Jonathan DeLanders if you prefer this.

### Centos 7 install/configure tools

```
# git
sudo yum install -y git
```
```
# Install and upgrade pip
sudo yum install python3-pip
sudo pip3 install --upgrade pip
```


```
# terraform
# https://learn.hashicorp.com/tutorials/terraform/install-cli

# dependencies
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
# terraform
sudo yum install -y terraform
# packer
sudo yum install -y packer
```

```
# install ansible
#https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#prerequisites-installing-pip

python3 -m pip install --user ansible
```

```
# install helm
# https://helm.sh/docs/intro/install/
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

```
# aws cli
# ensure you have installed pip from previous steps
# https://docs.aws.amazon.com/cli/v1/userguide/install-linux.html
pip3 install awscli --upgrade --user

# packer/terraform and ansible depend on the next step.  Enter your aws access key id and secret key when prompted
aws configure
```

## Terraforming Redis

```
# crdb1
cd redisent-terraform/crdb1
terraform apply

# crdb2
cd redisent-terraform/crdb2
terraform apply

# crdb3
cd redisent-terraform/crdb3
terraform apply

# crdb4
cd redisent-terraform/crdb4
terraform apply

# crdb5
cd redisent-terraform/crdb5
terraform apply
```

## Installing Redis with Ansible

# provision crdb1
cd redisent-ansible
ansible-playbook -i inventory/redisent-aws-inventory/crdb1 -u centos playbooks/install.yml
ansible-playbook -i inventory/redisent-aws-inventory/crdb1 -u centos playbooks/create-crdb.yml

# provision crdb2
cd redisent-ansible
ansible-playbook -i inventory/redisent-aws-inventory/crdb2 -u centos playbooks/install.yml
ansible-playbook -i inventory/redisent-aws-inventory/crdb2 -u centos playbooks/join-crdb.yml

# provision crdb3
cd redisent-ansible
ansible-playbook -i inventory/redisent-aws-inventory/crdb3 -u centos playbooks/install.yml
ansible-playbook -i inventory/redisent-aws-inventory/crdb3 -u centos playbooks/join-crdb.yml

# provision crdb4
cd redisent-ansible
ansible-playbook -i inventory/redisent-aws-inventory/crdb4 -u centos playbooks/install.yml
ansible-playbook -i inventory/redisent-aws-inventory/crdb4 -u centos playbooks/join-crdb.yml

# provision crdb5
cd redisent-ansible
ansible-playbook -i inventory/redisent-aws-inventory/crdb4 -u centos playbooks/install.yml
ansible-playbook -i inventory/redisent-aws-inventory/crdb4 -u centos playbooks/join-crdb.yml
```

## Terraforming AWS EKS kubernetes

## Installing monitoring charts with Helm and kubectl
