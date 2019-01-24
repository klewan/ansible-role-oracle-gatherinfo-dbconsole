Ansible Role: oracle-gatherinfo-dbconsole
=========================================

This role automatically discovers Oracle DB Console services (both standalone and registered in Grid Infrastructure).

Collected information is stored in role's `oracle_gatherinfo_dbconsole_registered_services` and `oracle_gatherinfo_dbconsole_running_services` variables and global `oracle_dbconsole_registered_services` and `oracle_dbconsole_running_services` variables.

Sample output:

    "oracle_dbconsole_registered_services": [
        {
            "dbconsole_resource_name": "dbconsole.orcl",
            "oracle_home": "/u01/app/oracle/product/11.2.0.4/dbhome1",
            "oracle_hostname": "dbserver1.foo.com",
            "oracle_sid": "ORCL",
            "state": "ONLINE"
        }
    ]

    "oracle_dbconsole_running_services": [
        {
            "instance_name": "ORCL",
            "oracle_home": "/u01/app/oracle/product/11.2.0.4/dbhome1"
        }
    ]
	

Supported OS:
-------------
* RedHat
* CentOS
* OracleLinux

Requirements
------------

This role uses `oracle` role.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):


    # collect data about DB console services registered in GI OHAS
    oracle_gatherinfo_dbconsole_from_gi_registry: true

    # List describing DB console services registered in GI OHAS - Oracle High Availability Services (dynamically populated)
    oracle_gatherinfo_dbconsole_registered_services: []

    # e.g.:
    #oracle_gatherinfo_dbconsole_registered_services:
    #  dbconsole_resource_name: "dbconsole.orcl"
    #  oracle_home: "/u01/app/oracle/product/11.2.0.4/dbhome1"
    #  oracle_hostname: "dbserver1.foo.com"
    #  oracle_sid: "ORCL"
    #  state: "ONLINE"

    # collect data about active/running DB console services
    oracle_gatherinfo_dbconsole_running: true

    # List describing active/running DB console services
    oracle_gatherinfo_dbconsole_running_services: []

    # e.g.:
    #oracle_gatherinfo_dbconsole_running_services:
    #  instance_name: "ORCL"
    #  oracle_home: "/u01/app/oracle/product/11.2.0.4/dbhome1"

    # print collected information about dbconsole services
    oracle_gatherinfo_dbconsole_print_collected_data: true


Dependencies
------------

This role uses `oracle` role.

Example Playbook
----------------

    - name: Gather information about installed Oracle components
      hosts: ora-servers
      gather_facts: true
      become: true
      become_user: '{{ oracle_user }}'

      tasks:

      - import_role:
          name: oracle-gatherinfo-dbconsole
        tags:
          - oracle-gatherinfo-dbconsole
          - oracle-gatherinfo-allcomponents

		  
Inside `vars/main.yml` or `group_vars/..` or `host_vars/..`:
    
    #-------------------------------------------------------
    # overrides role 'oracle-gatherinfo-dbconsole' variables
    #-------------------------------------------------------

    # collect data about active/running DB console services
    oracle_gatherinfo_dbconsole_running: false
		
    # ... etc ...


License
-------

GPLv3 - GNU General Public License v3.0

Author Information
------------------

This role was created in 2018 by [Krzysztof Lewandowski](mailto:Krzysztof.Lewandowski@fastmail.fm).


