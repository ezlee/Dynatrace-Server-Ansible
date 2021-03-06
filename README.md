# Dynatrace-Server-Ansible

This Ansible role installs and configures the Dynatrace Server of the [Dynatrace Application Monitoring](http://www.dynatrace.com/en/products/application-monitoring.html) solution.

## Download

The role is available via:

- [Ansible Galaxy](https://galaxy.ansible.com/Dynatrace/Dynatrace-Server)
- [GitHub](https://github.com/Dynatrace/Dynatrace-Server-Ansible)

## Description

This role downloads and installs the most recent version of the Dynatrace Server from [http://downloads.dynatracesaas.com](http://downloads.dynatracesaas.com). Alternatively, you can place the installer artifact as `dynatrace-server-linux-x86.jar` in the role's `files` directory from where it will be picked up during the installation. The default file name and URL can be overridden via the `dynatrace_server_linux_installer_file_name` and `dynatrace_server_linux_installer_file_url` attributes, respectively. Please refer to `defaults/main.yml` for a list of supported attributes.

## Role Variables

As defined in ```defaults/main.yml```:

| Name                                          | Default                                                               | Description
|-----------------------------------------------|-----------------------------------------------------------------------|------------
| *dynatrace_server_linux_install_dir*          | /opt                                                                  | The Dynatrace Server will be installed into the directory *$dynatrace_server_linux_install_dir*/dynatrace-*$major*-*$minor*-*$rev*, where *$major*, *$minor* and *$rev* are given by the installer. A symbolic link to the actual installation directory will be created in *$dynatrace_server_linux_install_dir*/dynatrace.
| *dynatrace_server_linux_installer_file_name*  | dynatrace-server-linux-x86.jar                                        | The file name of the Dynatrace installer in the role's ```files``` directory.
| *dynatrace_server_linux_installer_file_url*   | http://downloads.dynatracesaas.com/6.3/dynatrace-server-linux-x86.jar | A HTTP, HTTPS or FTP URL to the Dynatrace installer in the form (http\|https\|ftp)://[user[:pass]]@host.domain[:port]/path.
| *dynatrace_server_collector_port*             | 6698                                                                  | The port where the server shall listen for Collectors. Use either ```6698``` (non-SSL) or ```6699``` (SSL).
| *dynatrace_server_do_pwh_connection*          | no                                                                    | Whether a connection to an existing Performance Warehouse (database) shall be established, or not. **Note**: requires Dynatrace >= v6.2.
| *dynatrace_server_pwh_connection_hostname*    | localhost                                                             |
| *dynatrace_server_pwh_connection_port*        | 5432                                                                  |
| *dynatrace_server_pwh_connection_dbms*        | postgresql                                                            | The DBMS type of the Performance Warehouse. Possible values are ```embedded``` (not suitable for production systems), ```db2```, ```oracle```, ```postgresql```, ```sqlazure```, ```sqlserver```
| *dynatrace_server_pwh_connection_database*    | dynatrace                                                             |
| *dynatrace_server_pwh_connection_username*    | dynatrace                                                             |
| *dynatrace_server_pwh_connection_password*    | dynatrace                                                             |
| *dynatrace_server_owner*                      | dynatrace                                                             | The system user that owns the Dynatrace installation.
| *dynatrace_server_group*                      | dynatrace                                                             | The system user's group that owns the Dynatrace installation.
| *dynatrace_server_role_name*                  | Dynatrace.Dynatrace-Server                                            | The actual name of this role in an [Ansible Playbook's](http://docs.ansible.com/playbooks.html) ```roles``` directory.

## Example Playbook

```
- hosts: all
  roles:
    - role: Dynatrace.Dynatrace-Server
      dynatrace_server_do_pwh_connection: yes
```

## Testing

We use [Test Kitchen](http://kitchen.ci) to automatically test our automated deployments with [Serverspec](http://serverspec.org) and [RSpec](http://rspec.info/):

1) Install Test Kitchen and its dependencies from within the project's directory:

```
gem install bundler
bundle install
```

2) Run all tests

```
kitchen test
```

By default, we run our tests inside [Docker](https://www.docker.com/) containers as this considerably speeds up testing time (see `.kitchen.yml`).

## Additional Resources

### Blogs

- [How to Automate Enterprise Application Monitoring with Ansible](http://apmblog.dynatrace.com/2015/03/04/how-to-automate-enterprise-application-monitoring-with-ansible/)
- [How to Automate Enterprise Application Monitoring with Ansible - Part II](http://apmblog.dynatrace.com/2015/04/23/how-to-automate-enterprise-application-monitoring-with-ansible-part-ii/)

### Presentations

- [Automated Deployments (of Dynatrace) with Ansible](http://www.slideshare.net/MartinEtmajer/automated-deployments-with-ansible)
- [Test-Driven Infrastructure with Ansible, Test Kitchen, Serverspec and RSpec](http://www.slideshare.net/MartinEtmajer/testing-ansible-roles-with-test-kitchen-serverspec-and-rspec-48185017)

## Problems? Questions? Suggestions?

This offering is [Dynatrace Community Supported](https://community.dynatrace.com/community/display/DL/Support+Levels#SupportLevels-Communitysupported/NotSupportedbyDynatrace(providedbyacommunitymember)). Feel free to share any problems, questions and suggestions with your peers on the Dynatrace Community's [Application Monitoring & UEM Forum](https://answers.dynatrace.com/spaces/146/index.html).

## License

Licensed under the MIT License. See the LICENSE file for details.
[![analytics](https://www.google-analytics.com/collect?v=1&t=pageview&_s=1&dl=https%3A%2F%2Fgithub.com%2FdynaTrace&dp=%2FDynatrace-Server-Ansible&dt=Dynatrace-Server-Ansible&_u=Dynatrace~&cid=github.com%2FdynaTrace&tid=UA-54510554-5&aip=1)]()
