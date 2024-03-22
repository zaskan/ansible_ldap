# ansible_ldap
## Install a minimal LDAP environment for testing using Ansible
### Requirements
- Set **new_ldap_password** via extra_vars
- A Debian 11 ldap server
### Instructions
- Add your ldap servers to the inventory file. Tested only in Debian 11 Servers
- Execute the playbook, adding your ldap admin password via extra vars
~~~
ansible-playbook -i inventory install_ldap.yml -e new_ldap_password=YOUR_ADMIN_PASSWORD
~~~

If you want to add your ldap servers to an Ansible Controller, add your credentials in the `configure_controller.yaml` playbook and execute it in the same way.
 
