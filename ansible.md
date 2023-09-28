# Ansible
Ansible is an IT automation tool, it automates the management of remote systems and controls their desired state. . It can configure systems, deploy software and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates. 


**Ansible manages machines in an agent-less manner**. There is never a question of how to upgrade remote daemons or the problem of not being able to manage systems because daemons are uninstalled. Also, security exposure is greatly reduced because Ansible uses OpenSSH — the open source connectivity tool for remote login with the SSH (Secure Shell) protocol.

Ansible is decentralized–it relies on your existing OS credentials t control access to remote machines.

A basic Ansible environment has 3 main components :
1. **Control node**
A system on which ansible. You run Ansible commands such as	`ansible` or `ansible-inventory` on a control node.
2. **Managed node**
A remote system, or a host, that Ansible controls
3. **Inventory**
A list of managed nodes that are logically organized. Your create an inventory on the control node to describe host deployments to ansible.




### Inventory
Inventories organize managed nodes in centralized files that provide Ansible with system information and network locations. 

Using an inventory file, Ansible can manage a large number of hosts with a single command. 


To build and create an invetory we do as follows:


1. Create a file named `inventory.ini` inside `ansible_quickstart` direcotry. 
2. Add a new `[myhosts]` group to the `inventory.ini` file and specify the ip addresses of the hosts you want to manage.
```ini
[myhosts]
192.168.1.40
192.168.1.45
```

3. Verify your inventory
```sh
ansible-inventory -i inventory.ini --list
```

4. Ping the `myhosts` group that you set in the inventory
```sh
ansible myhosts -m ping -i inventory.ini
```


Creating an inventory in YAML format becomes a sensible option as the number of managed nodes increases. For example, the following is an equivalent of the inventory.ini that declares unique names 
for managed nodes and uses the ansible_host field:

```yaml
myhosts:
	hosts:
		my_host_01:
			ansible_host: 192.168.1.40
		my_host_02:
			ansible_host: 192.168.1.45

```



### Playbooks
Playbooks are automation blueprints, in `YAML` format, that ansible uses to deploy and confiure managed hosts.

##### Playbook
A list of plays that define the order in which Ansible performs operations, from top to bottom, to achieve an overall goal. 

##### Play
An ordered list of tasks that maps the managed nodes in an inventory.

##### Task
A list of one or more modules that defines the operations that Ansible performs.


##### Module
A unit of code or binary that Ansible runs on managed nodes. 


*To create a playbook that pings your hosts and prints a “Hello world” message:*

1. Create a file named `playbook.yaml` in your `ansible_quickstart` directory, that you created earlier, with the following content:

```yaml
- name: My first play
 	hosts: myhosts
	tasks:
	- name: Ping my hosts
	ansible.builtin.ping:
	- name: Print message
	ansible.builtin.debug:
		msg: Hello world
```

2. Run your playbook.
```sh
ansible-playbook -i inventory.ini playbook.yaml
```

