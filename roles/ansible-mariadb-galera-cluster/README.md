Role Name
=========

Installs mariadb mysql https://mariadb.org/
###### Configurable options (clustering and cacti monitoring ready)

Requirements
------------

None

Role Variables
--------------

````
---
# defaults file for ansible-mariadb-galera-cluster
cacti_db_password: cactiuser  #defines the password for cacti db monitoring...define here or globally in group_vars/all/accounts
cacti_db_user: cactiuser  #defines the user for cacti db monitoring...define here or globally in group_vars/all/accounts
deb_db_password: "{{ mysql_root_password }}"  #defines debian db password...generate using echo password | mkpasswd -s -m sha-512
email_notifications: 'notifications@{{ smtp_domain_name }}'  #defines email address to receive notifications...define here or in group_vars/group
enable_cacti_monitoring: false  #defines if cacti monitoring should be enabled for mysql
enable_galera_monitoring_script: false
galera_cluster_name: [] # Define the name of the cluster...define here or in group_vars/group
galera_cluster_nodes: [] # Define the IP addresses of the nodes which will be part of the cluster...define here or in group_vars/group
galera_monitor_script_name: galeranotify.py
galera_monitor_script_path: /etc/mysql
mariadb_debian_repo: 'deb http://ftp.osuosl.org/pub/mariadb/repo/{{ mariadb_version }}/{{ ansible_distribution|lower }} {{ ansible_distribution_release|lower }} main'
mariadb_debian_repo_key: '0xcbcb082a1bb943db'
mariadb_debian_repo_keyserver: 'keyserver.ubuntu.com'
mariadb_version: 10.0
mysql_master: false  #defines a node in the cluster as master...define as true for one host in host_vars/host
mysql_root_password: root #defines mysql root password...generate using echo password | mkpasswd -s -m sha-512
notify_mail_from: 'galeranotify@{{ smtp_domain_name }}'  #defines email address that cluster notifications will be sent from
notify_mail_to: '{{ email_notifications }}'
notify_smtp_server: '{{ smtp_server }}'  #defines smtp server to send notifications through
pri_domain_name: example.org
reconfigure_galera: false  #defines if the cluster should be reconfigured
smtp_domain_name: '{{ pri_domain_name }}' #defines smtp domain for email...define here or globally in group_vars/all/email
smtp_server: 'smtp.{{ pri_domain_name }}'  #defines smtp server to send email through...define here or globally in group_vars/all/servers
````

Dependencies
------------

None

Example Playbook
----------------

#### GitHub
````
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-mariadb-galera-cluster
  tasks:
````
#### Galaxy
````
---
- hosts: all
  become: true
  vars:
  roles:
    - role: mrlesmithjr.mariadb-galera-cluster
  tasks:
````

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com