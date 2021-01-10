# Dependencies

## Install Ansible
Example below is for CentOS 8
```
sudo dnf -y install python3-pip
sudo pip3 install --upgrade pip
pip3 install ansible --user
```

## Clone Repo
```
git clone https://github.com/lspiehler/ansible_cisco_backup.git
cd ansible_cisco_backup
```

## Define Local Variables
```
cat << EOF > extra_vars.yml
---
  ansible_user: <cisco_username>
  ansible_password: <cisco_password>
  network_backup_repository: <git_repo_url>
  group_tag: all
EOF
```

## Create an inventory
```
cat << EOF > hosts.ini
[all]
Switch ansible_host=192.168.1.6 ansible_network_os=ios
EOF
```

## Install Dependencies
```
ansible-galaxy install -r roles/requirements.yml
ansible-galaxy collection install cisco.ios
pip3 install netaddr paramiko
```

## Optionally disable host key checking
```
cat << EOF > ansible.cfg
[defaults]
host_key_checking = False
EOF
```

# Run the playbook
```
ansible-playbook -i hosts.ini backup.yml -e @extra_vars.yml
```
