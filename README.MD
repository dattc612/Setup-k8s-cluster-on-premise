# Setting Up an On-premise Kubernetes Cluster 
Change configuration in inventory.yaml file

```yaml
virtualmachines:
  hosts:
    vm01: # or localhost
      ansible_connection: ssh
      ansible_host: 192.168.1.10
      ansible_port: 22
      ansible_user: username
      ansible_password: password
      ansible_become: yes 
      ansible_become_method: sudo
      ansible_become_pass: password
```
Or use local machine. [More information](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)

# Run ansible-playbook to initialize the cluster
```shell
cd ansible_setup_env
ansible-playbook -i inventory.yaml playbook.yaml -v
```

# Deploy gitlab and jenkins

## Note 
  
Remove the cached key for 192.168.1.11 on the local machine (not required)
```
ssh-keygen -R 192.168.1.11
```

Add this host's fingerprint to your known_hosts file to manage. Connect ssh manually for the first time
```
ssh vagrant@192.168.1.11 
```

## Deploy
```shell
ansible-playbook -i inventory.yaml playbook.yaml
```

## Add ip 192.168.1.11 into hosts with DNS name jenkins.dev.com and gitlab.dev.com  
```text
192.168.1.11	jenkins.dev.com
192.168.1.11 	gitlab.dev.com
```

## For the first login
```yaml
  gitlab:
    user: root
    password: <get from gitlab-gitlab-initial-root-password secret>
  jenkins: 
    user: admin
    password: <get from jenkins secret>
```