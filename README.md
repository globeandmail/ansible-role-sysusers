# ansible-role-sysusers

This role manages users on the target host(s), including SSH authorized_keys.


Role Variables
--------------

sysusers

This role has the same behaviour as the Ansible 'user' module, with the addition of the 'authorized' property which utilizes the 'authorized_key' module (see example).

For reference,
   http://docs.ansible.com/user_module.html
   http://docs.ansible.com/authorized_key_module.html


Example Playbook
----------------

The recommended way of using this role is to include the role in the top play (that runs on all nodes) and define the variable in group_vars or host_vars files.

Example play including this role:

    - hosts: all
      roles:
      - ansible-role-sysusers


Defining Variables:

  group_vars/dev-all.yml

   sysusers:
    - name: userone
    - name: usertwo
      uid: 1234
      group: usertwo
      groups:
      - www-data
      - mysql
      shell: '/bin/bash'
      password: '$6$xtQrZzV5jWd0arrz$5vqjD0Qsfylh0P4CB/Fe68Zcrxqj7QPLQgL6MNES1x/Wp8waCA3deQzzGRyvOzXtDh6ctQwNiHz90QF/dh9UM0'
      authorized:
      - key: 'ssh-rsa DEF456 keycmt'


##### To generate the encrypted password for the user, use 'mkpasswd'. On Ubuntu, the utility is in the 'whois' package.

   mkpasswd --method=SHA-512

  (See http://docs.ansible.com/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module)
