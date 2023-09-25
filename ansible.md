# Ansible
Ansible is an IT automation tool, it automates the management of remote systems and controls their desired state. . It can configure systems, deploy software and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates. 


**Ansible manages machines in an agent-less manner**. There is never a question of how to upgrade remote daemons or the problem of not being able to manage systems because daemons are uninstalled. Also, security exposure is greatly reduced because Ansible uses OpenSSH — the open source connectivity tool for remote login with the SSH (Secure Shell) protocol.

Ansible is decentralized–it relies on your existing OS credentials to control access to remote machines.

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