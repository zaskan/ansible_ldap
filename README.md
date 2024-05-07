# ansible_ldap
## Install a minimal LDAP environment for testing using Ansible
### Requirements
- Set **new_ldap_password** via extra_vars
- A Debian 11 ldap server
- (Optional) kcli
- (Optional) An Ansible or AWX controller
### Instructions

Optionally, you can provision the servers via [kcli](https://kcli.readthedocs.io/en/latest/). In that case, you need to have kcli installed in your host machine.
Add the desired hostnames to your inventory file. Once the vm is provisioned, the playbook will add to the file the additional information needed.

~~~
[all]
ldap01.example.com
~~~

The command below will try to provision the vms in the host.

~~~
ansible-playbook -i inventory kcli_deploy_infra.yml
~~~

Once you have the servers provisioned, follow the steps below to configure ldap on them.

- Add your ldap servers to the inventory file if you didn't before. 

~~~
[all]
ldap01.example.com ansible_host=192.168.124.171 ansible_user=root
~~~

- Execute the playbook, adding your ldap admin password via extra vars

~~~
ansible-playbook -i inventory install_ldap.yml -e new_ldap_password=YOUR_ADMIN_PASSWORD
~~~

- If you want to create extra objects in the ldap, add the information to files/extra_objects.ldif and execute the following playbook.

~~~
ansible-playbook -i inventory configure_ldap.yml -e ldap_password=YOUR_ADMIN_PASSWORD
~~~

If you want to add your ldap servers to an Ansible Controller, add your credentials in the `configure_controller.yaml` playbook and execute it in the same way.

In this case the server list should contain an ordinal number matching with the ldap server order number in settings/ldap

If you want to configure your Ansible Controller or Awx to use these servers for authentication, add the credentials to `configure_controller.yml` and execute:

~~~
ansible-playbook -i inventory configure_controller.yml -e ldap_password=YOUR_ADMIN_PASSWORD
~~~
