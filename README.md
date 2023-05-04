# ansible-role-win-sqlserver

Ansible Role to install SQL Server on Windows

## Table of content

- [Default Variables](#default-variables)
  - [ps_tools_download_url](#ps_tools_download_url)
  - [ps_tools_filename_zip](#ps_tools_filename_zip)
  - [sql_server_already_installed_path](#sql_server_already_installed_path)
  - [sql_server_change_sysadmin_role_file_sql_script_file_path](#sql_server_change_sysadmin_role_file_sql_script_file_path)
  - [sql_server_change_sysadmin_role_file_sql_template](#sql_server_change_sysadmin_role_file_sql_template)
  - [sql_server_collation](#sql_server_collation)
  - [sql_server_dir_backup](#sql_server_dir_backup)
  - [sql_server_dir_install_data](#sql_server_dir_install_data)
  - [sql_server_dir_temp_db](#sql_server_dir_temp_db)
  - [sql_server_dir_temp_db_on_emphemeral_disk](#sql_server_dir_temp_db_on_emphemeral_disk)
  - [sql_server_dir_user_db](#sql_server_dir_user_db)
  - [sql_server_dir_user_log](#sql_server_dir_user_log)
  - [sql_server_enable_clr](#sql_server_enable_clr)
  - [sql_server_enable_smo_dmo_xps](#sql_server_enable_smo_dmo_xps)
  - [sql_server_enable_xp_cmdshell](#sql_server_enable_xp_cmdshell)
  - [sql_server_extract_dir](#sql_server_extract_dir)
  - [sql_server_install_configuration_file_path](#sql_server_install_configuration_file_path)
  - [sql_server_install_configuration_template](#sql_server_install_configuration_template)
  - [sql_server_install_features](#sql_server_install_features)
  - [sql_server_instance_name](#sql_server_instance_name)
  - [sql_server_iso_file_path](#sql_server_iso_file_path)
  - [sql_server_iso_url](#sql_server_iso_url)
  - [sql_server_iso_url_validate_certs](#sql_server_iso_url_validate_certs)
  - [sql_server_max_degree_of_parallelism](#sql_server_max_degree_of_parallelism)
  - [sql_server_max_memory](#sql_server_max_memory)
  - [sql_server_min_memory](#sql_server_min_memory)
  - [sql_server_sa_password](#sql_server_sa_password)
  - [sql_server_sp_configure_settings_enabled](#sql_server_sp_configure_settings_enabled)
  - [sql_server_sp_configure_settings_file_sql_script_file_path](#sql_server_sp_configure_settings_file_sql_script_file_path)
  - [sql_server_sp_configure_settings_file_sql_template](#sql_server_sp_configure_settings_file_sql_template)
  - [sql_server_sysadmin_sql_accounts](#sql_server_sysadmin_sql_accounts)
  - [sql_server_sysadmin_windows_accounts](#sql_server_sysadmin_windows_accounts)
  - [sql_server_sysadminaccounts](#sql_server_sysadminaccounts)
  - [sql_server_tempdb_file_count](#sql_server_tempdb_file_count)
  - [sql_server_update_enabled](#sql_server_update_enabled)
  - [sql_server_use_microsoft_update](#sql_server_use_microsoft_update)
  - [sql_server_version_major_path_prefix](#sql_server_version_major_path_prefix)
  - [sql_server_windows_firewall_port](#sql_server_windows_firewall_port)
  - [sql_server_windows_firewall_rule_name](#sql_server_windows_firewall_rule_name)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### ps_tools_download_url

Download URL for PSTools.

PSEXEC needs to be used to execute the SQL Server Installer

#### Default value

```YAML
ps_tools_download_url: https://download.sysinternals.com/files/PSTools.zip
```

### ps_tools_filename_zip

PSTools Package file name

#### Default value

```YAML
ps_tools_filename_zip: PSTools.zip
```

### sql_server_already_installed_path

Path to check if SQL Server is already installed

#### Default value

```YAML
sql_server_already_installed_path: '{{ sql_server_dir_install_data }}\{{ sql_server_version_major_path_prefix
  }}.{{ sql_server_instance_name }}\MSSQL\DATA'
```

### sql_server_change_sysadmin_role_file_sql_script_file_path

Local path to save template file to add accounts to sysadmin group. Get automatically removed afterwards

#### Default value

```YAML
sql_server_change_sysadmin_role_file_sql_script_file_path: '{{ ansible_env.SystemRoot
  }}\sqlcmd_add_adaccount_to_sysadmin.sql'
```

### sql_server_change_sysadmin_role_file_sql_template

Template file to add accounts to sysadmin group

#### Default value

```YAML
sql_server_change_sysadmin_role_file_sql_template: '{{ role_path }}/templates/sqlcmd_add_account_to_sysadmin.sql.j2'
```

### sql_server_collation

SQL Server Collation

#### Default value

```YAML
sql_server_collation: SQL_Latin1_General_CP1_CI_AS
```

### sql_server_dir_backup

Directory for SQL Server Backups

Note: To use this variable you need to uncomment them in templates/sql_server_configuration_file_std...

#### Default value

```YAML
sql_server_dir_backup: '{{ sql_server_dir_install_data }}\{{ sql_server_version_major_path_prefix
  }}.{{ sql_server_instance_name }}\MSSQL\Backup'
```

### sql_server_dir_install_data

Installation directory

#### Default value

```YAML
sql_server_dir_install_data: C:\Program Files\Microsoft SQL Server
```

### sql_server_dir_temp_db

Directory for SQL Server TempDB

Note: To use this variable you need to uncomment them in templates/sql_server_configuration_file_std...

#### Default value

```YAML
sql_server_dir_temp_db: '{{ sql_server_dir_install_data }}\{{ sql_server_version_major_path_prefix
  }}.{{ sql_server_instance_name }}\MSSQL\DATA'
```

### sql_server_dir_temp_db_on_emphemeral_disk

Set this to true if using azure temporary disk for TempDB

#### Default value

```YAML
sql_server_dir_temp_db_on_emphemeral_disk: false
```

### sql_server_dir_user_db

Directory for SQL Server User DBs

Note: To use this variable you need to uncomment them in templates/sql_server_configuration_file_std...

#### Default value

```YAML
sql_server_dir_user_db: '{{ sql_server_dir_install_data }}\{{ sql_server_version_major_path_prefix
  }}.{{ sql_server_instance_name }}\MSSQL\DATA'
```

### sql_server_dir_user_log

Directory for SQL Server Database Logfiles

Note: To use this variable you need to uncomment them in templates/sql_server_configuration_file_std...

#### Default value

```YAML
sql_server_dir_user_log: '{{ sql_server_dir_install_data }}\{{ sql_server_version_major_path_prefix
  }}.{{ sql_server_instance_name }}\MSSQL\DATA'
```

### sql_server_enable_clr

Advanced setting - clr enabled

#### Default value

```YAML
sql_server_enable_clr: false
```

### sql_server_enable_smo_dmo_xps

Advanced setting - SMO and DMO XPs

#### Default value

```YAML
sql_server_enable_smo_dmo_xps: true
```

### sql_server_enable_xp_cmdshell

Advanced setting - xp_cmdshell

#### Default value

```YAML
sql_server_enable_xp_cmdshell: false
```

### sql_server_extract_dir

Extract directory for installation files

#### Default value

```YAML
sql_server_extract_dir: C:\windows\temp\sqlextract
```

### sql_server_install_configuration_file_path

Resulting path for sql_server_configuration_file.ini

#### Default value

```YAML
sql_server_install_configuration_file_path: '{{ sql_server_extract_dir }}\sql_server_configuration_file.ini'
```

### sql_server_install_configuration_template

Path to template for sql_server_configuration_file

#### Default value

```YAML
sql_server_install_configuration_template: templates/sql_server_configuration_file_{{
  sql_server_version_major_path_prefix }}_ini.j2
```

### sql_server_install_features

SQL Server Features to be installed

#### Default value

```YAML
sql_server_install_features: SQLENGINE,REPLICATION,FULLTEXT
```

### sql_server_instance_name

SQL Server Instance Name

#### Default value

```YAML
sql_server_instance_name: MSSQLSERVER
```

### sql_server_iso_file_path

Resulting file path after SQL Server ISO is downloaded

#### Default value

```YAML
sql_server_iso_file_path: '{{ sql_server_extract_dir }}\sql_server.iso'
```

### sql_server_iso_url

SQL Server ISO Download URL

#### Default value

```YAML
sql_server_iso_url: http://localhost:9000/en_sql_server_2019_standard_x64_dvd_814b57aa.iso
```

### sql_server_iso_url_validate_certs

Validate SSL certs when downloading files

#### Default value

```YAML
sql_server_iso_url_validate_certs: yes
```

### sql_server_max_degree_of_parallelism

Advanced setting - max degree of parallelism

#### Default value

```YAML
sql_server_max_degree_of_parallelism: "{{ '8' if (ansible_processor_vcpus >= 8) else\
  \ '2' if (ansible_processor_vcpus <= 2) else '4' }}"
```

### sql_server_max_memory

Advanced setting - maximum memory

#### Default value

```YAML
sql_server_max_memory: '{{ (ansible_memtotal_mb|int) - (((ansible_memtotal_mb|int)
  * 0.1)|int) }}'
```

### sql_server_min_memory

Advanced setting - minimum memory

#### Default value

```YAML
sql_server_min_memory: '{{ (ansible_memtotal_mb|int) - (((ansible_memtotal_mb|int)
  * 0.1)|int) }}'
```

### sql_server_sa_password

SQL Server sa password

#### Default value

```YAML
sql_server_sa_password: SomePassw0rd!
```

### sql_server_sp_configure_settings_enabled

Enable feature to set advanced configuration settings

#### Default value

```YAML
sql_server_sp_configure_settings_enabled: false
```

### sql_server_sp_configure_settings_file_sql_script_file_path

Local path to save template file for setting advanced configuration settings.

#### Default value

```YAML
sql_server_sp_configure_settings_file_sql_script_file_path: '{{ ansible_env.SystemRoot
  }}\sqlcmd_sp_configure_settings.sql'
```

### sql_server_sp_configure_settings_file_sql_template

Template file to use for setting advanced configuration settings

#### Default value

```YAML
sql_server_sp_configure_settings_file_sql_template: '{{ role_path }}/templates/sqlcmd_sp_configure_settings.sql.j2'
```

### sql_server_sysadmin_sql_accounts

List of sql accounts to add to sysadmin role

#### Default value

```YAML
sql_server_sysadmin_sql_accounts: []
```

#### Example usage

```YAML
sql_server_sysadmin_sql_accounts:
  - { name: "someadmin", password: "somepassword" }
  - { name: "otheradmin", password: "otherpassword" }
```

### sql_server_sysadmin_windows_accounts

List of windows accounts to add to sysadmin role

#### Default value

```YAML
sql_server_sysadmin_windows_accounts: []
```

#### Example usage

```YAML
sql_server_sysadmin_windows_accounts:
  - DOMAIN\user1
  - DOMAIN\group1
```

### sql_server_sysadminaccounts

SQL Server Sysadmin account

#### Default value

```YAML
sql_server_sysadminaccounts: BUILTIN\Administrators
```

### sql_server_tempdb_file_count

Specifies the number of tempdb data files to be added by setup. This value can be increased up to the number of cores.

#### Default value

```YAML
sql_server_tempdb_file_count: 1
```

### sql_server_update_enabled

Enable Updates

#### Default value

```YAML
sql_server_update_enabled: false
```

### sql_server_use_microsoft_update

Use Microsoft Updates

#### Default value

```YAML
sql_server_use_microsoft_update: false
```

### sql_server_version_major_path_prefix

Path prefix dependent on SQL Server version.

MSSQL11=SQL Server 2012

MSSQL12=SQL Server 2014

MSSQL15=SQL Server 2019

#### Default value

```YAML
sql_server_version_major_path_prefix: MSSQL15
```

### sql_server_windows_firewall_port

SQL Server Firewall port

#### Default value

```YAML
sql_server_windows_firewall_port: 1433
```

### sql_server_windows_firewall_rule_name

SQL Server Firewall Rule name

#### Default value

```YAML
sql_server_windows_firewall_rule_name: '{{ sql_server_instance_name }}'
```

## Discovered Tags

**_firewall_**

**_sql-server-sp-configure-settings_**

**_sql-server-sysadmin-role_**


## Dependencies

None.

## License

license (GPLv2, CC-BY, etc)

## Author

andif888
