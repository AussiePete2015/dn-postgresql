&copy; 2016 DataNexus Inc.

Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

IThe _site.yml_ playbook contains the following:

    - hosts: "{{ host_inventory }}"
      roles:
        - { role: postgresql, become: yes }

Call like the entire playbook like this:

    AWS_PROFILE=PROFILE ansible-playbook -e "INVENTORY" --private-key=aws_developer_developer_private_key.pem --user=centos site.yml

where:
  
    PROFILE is your ~/.aws/credentials profile

and

    INVENTORY is the query intersection of tags to uniquely identify the required hosts 

Supported tags are:

* Teant - customer or client (UNIQUE per platform instance)
* Cloud - [aws | azure | openstack]
* Project - customer specific project name (UNIQUE per tenant)
* Domain - development, production, etc
* Application - cassandra, prostgres, kafka, etc 

Some examples:

Within the AWS master account for datanexus, return all postgres hosts for the tenant CustomerXYZ:

    AWS_PROFILE=datanexus ansible-playbook -e "tag_Application_postgresql:&tag_Tenant_CustomerXYZ" --private-key=aws_postgres_customer_development_private_key.pem --user=centos site.yml    

Within the AWS master account for datanexus, return all cassandra hosts:

    AWS_PROFILE=datanexus ansible-playbook -e "tag_Application_cassandra" --private-key=aws_postgres_customer_development_private_key.pem --user=centos site.yml    

Within the AWS master account for datanexus, return all development cassandra hosts for project coolstuff:

    AWS_PROFILE=datanexus ansible-playbook -e "tag_Application_cassandra:&tag_Domain_development:&tag_Project_coolstuff" --private-key=aws_postgres_customer_development_private_key.pem --user=centos site.yml    

Disregard all dynamic lookups and specify two hosts manually, such as for use within Vagrant:

    AWS_PROFILE=datanexus ansible-playbook -e "{host_inventory: [10.0.1.1, 10.0.1.2]}" --private-key=aws_postgres_customer_development_private_key.pem --user=centos site.yml

License
-------

Apache

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
