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
ansible-playbook -i inventory.yaml playbook.yaml -v
```


