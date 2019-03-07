# Install root cert 

## Windows 

First  execute this powershell script on windows:
https://github.com/ansible/ansible/blob/devel/examples/scripts/ConfigureRemotingForAnsible.ps1

Ports need to be open:
- winrm-https: 5986 

Configure ansible host file

```yaml
ec2-34-241-50-89.eu-west-1.compute.amazonaws.com ansible_user=Administrator ansible_password=xyz"" ansible_port=5986 ansible_connection=winrm ansible_winrm_server_cert_validation=ignore
```

Verify connectivity

    ansible all -i hosts -m win_ping

## Usage 

Put your root ca to roles/rootca/files/ca.crt

Sample playbook

```yaml
- hosts: all
  become: no
  vars:
    root_ca: ca.crt
  roles:
    - rootca
```

Sample inventory

```yaml
[all]
#ubuntu 18.10
ec2-52-211-28-56.eu-west-1.compute.amazonaws.com ansible_user=ubuntu
```

Sample command 

    ansible-playbook -v -i hosts server.yaml


Tested with:
- Ubuntu 18.10
- RHEL6
- RHEL7
- Windows Server 2016

### Links 
[Link1](https://argonsys.com/microsoft-cloud/articles/configuring-ansible-manage-windows-servers-step-step/)
[Link2](https://www.businessnewsdaily.com/11036-how-to-use-ansible-on-windows.html)
