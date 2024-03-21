# ansible_ldap
## Install a minimal LDAP environment for testing using Ansible
### Requirements
- Set **new_ldap_password** via extra_vars
- Debian 11
### Instructions
- Add your ldap servers to the inventory file. Tested only in Debian 11
- Execute the playbook, adding your ldap admi password via extra vars
~~~
ansible-playbook -i inventory install_ldap.yml -e new_ldap_password=YOUR_ADMIN_PASSWORD
~~~
 
