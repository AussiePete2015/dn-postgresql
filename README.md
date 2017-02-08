&copy; 2016 DataNexus Inc.

Role Name
=========

Builds a stand-alone postgresql database with SSL connectivity. If multiple servers have been provisioned and tagged with "Role:master" and "Role:replica" 
a streaming master-replica will be provisioned.

Requirements
------------

* ec2
* boto

Role Variables
--------------

    application: postgresql
    postgresql_version: "9.2.18-1.el7"
    python_postgres_adapter_version: "2.5.1-3.el7"
    postgresql_package_list:
      - "python-psycopg2-{{ python_postgres_adapter_version }}"
      - "postgresql-{{ postgresql_version }}"
      - "postgresql-server-{{ postgresql_version }}"
      - "postgresql-contrib-{{ postgresql_version }}"
      - "postgresql-libs-{{ postgresql_version }}"
    postgresql_data_dir: "/data/pgsql"
    postgresql_home_dir: "/var/lib/pgsql"
    postgresql_bin_path: "/usr/bin"
    postgresql_config_path: "{{ postgresql_data_dir }}"
    postgresql_daemon: postgresql
    postgresql_interface: eth1
    ansible_ssh_private_key_file: "aws_{{ hostvars[inventory_hostname].ec2_key_name }}_private_key.pem"

Dependencies
------------
Instances must be tagged: 

    Cloud
    Tenant
    Project
    Domain
    Application
    [Role]

Playbook
----------------
The _site.yml_ playbook contains the necessary code to provision either an individual server or a master-replica pair.

Call like the  playbook like this:

    AWS_PROFILE=PROFILE ansible-playbook -e "project=PROJECT application=postgresql domain=DOMAIN  host_inventory=tag_Application_{{ application }} ansible_user=USER" site.yml

where:
  
    PROFILE is your ~/.aws/credentials profile

and

    PROJECT is the project name
    DOMAIN is the domain: development or production or similar
    USER is the instance login, ec2-user, redhat, centos, etc
    
The command that was used repeatedly during development and testing on AWS was:

    AWS_PROFILE=datanexus ansible-playbook -e "project=demo application=postgresql domain=development  host_inventory=tag_Application_{{ application }} ansible_user=centos" test.yml

License
-------

Apache

Author Information
------------------

[Christopher Keller](mailto:ckeller@datanexus.org)