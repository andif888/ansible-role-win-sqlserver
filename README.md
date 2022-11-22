# ansible-role-win-sqlserver

Ansible Role to install SQL Server on Windows

## Table of content

- [Default Variables](#default-variables)
  - [ps_tools_download_url](#ps_tools_download_url)
  - [ps_tools_filename_zip](#ps_tools_filename_zip)
  - [sql_server_already_installed_path](#sql_server_already_installed_path)
  - [sql_server_collation](#sql_server_collation)
  - [sql_server_dir_backup](#sql_server_dir_backup)
  - [sql_server_dir_install_data](#sql_server_dir_install_data)
  - [sql_server_dir_temp_db](#sql_server_dir_temp_db)
  - [sql_server_dir_user_db](#sql_server_dir_user_db)
  - [sql_server_dir_user_log](#sql_server_dir_user_log)
  - [sql_server_extract_dir](#sql_server_extract_dir)
  - [sql_server_install_configuration_file_path](#sql_server_install_configuration_file_path)
  - [sql_server_install_configuration_template](#sql_server_install_configuration_template)
  - [sql_server_install_features](#sql_server_install_features)
  - [sql_server_instance_name](#sql_server_instance_name)
  - [sql_server_iso_file_path](#sql_server_iso_file_path)
  - [sql_server_iso_url](#sql_server_iso_url)
  - [sql_server_iso_url_validate_certs](#sql_server_iso_url_validate_certs)
  - [sql_server_sa_password](#sql_server_sa_password)
  - [sql_server_sysadminaccounts](#sql_server_sysadminaccounts)
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

### sql_server_sa_password

SQL Server sa password

#### Default value

```YAML
sql_server_sa_password: SomePassw0rd!
```

### sql_server_sysadminaccounts

SQL Server Sysadmin account

#### Default value

```YAML
sql_server_sysadminaccounts: BUILTIN\Administrators
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


## Dependencies

None.

## License

license (GPLv2, CC-BY, etc)

## Author

andif888
