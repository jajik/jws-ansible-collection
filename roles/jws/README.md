middleware_automation.jws.jws
==================================================

This role contains the ansible playbook to setup JWS.


Dependency
--------------
- middleware_automation.redhat_csp_download
    - This collection is required to download resources from RedHat Customer Portal.
    - Documentation to collection can be found at <https://github.com/ansible-middleware/redhat-csp-download>

<!--start argument_specs-->
Role Defaults
-------------

| Variable | Description | Default |
|:---------|:------------|:--------|
|`tomcat_apps_to_remove`| Comma separated list of apps to undeploy | `docs,ROOT,examples` |
|`tomcat_install_method`| Installation method | `local_zipfiles` |
|`tomcat_rpm`| Installation RPM version | `jws5` |
|`jws_rhn_server_zipfile_url`| Customer Portal URL for installation archive | `https://access.redhat.com/jbossnetwork/restricted/softwareDownload.html?softwareId=90341` |
|`jws_native_zipfile_url`| Customer Portal URL for installation archive, native variant | `https://access.redhat.com/jbossnetwork/restricted/softwareDownload.html?softwareId=90361` |
|`tomcat_user`| posix user account for service | `tomcat` |
|`tomcat_group`| posix group for service | `tomcat` |
|`tomcat_home`| Target installation directory | `/opt/jws-5.4/tomcat` |
|`tomcat_catalina_base`| Tomcat catalina base env variable | `{{ lookup('env','CATALINA_BASE') }}` |
|`tomcat_conf_properties`| Path for tomcat configuration | `./conf/catalina.properties` |
|`tomcat_conf_policy`| Path for tomcat policy configuration | `./conf/catalina.policy` |
|`tomcat_conf_loggging`| Path for logging configuration | `./conf/logging.properties` |
|`tomcat_conf_context`| Relative path to context.xml | `./conf/context.xml` |
|`tomcat_conf_server`| Relative path to server.xml | `./conf/server.xml` |
|`tomcat_conf_web`| Relative path to web.xml | `./conf/web.xml` |
|`tomcat_conf_templates_context`| Template to use for context.xml | `templates/context.xml.j2` |
|`tomcat_conf_templates_server`| Template to use for server.xml | `templates/server.xml.j2` |
|`tomcat_conf_templates_web`| Template to use for web.xml | `templates/web.xml.j2` |
|`tomcat_shutdown_port`| Tomcat shutdown port | `8005` |
|`tomcat_listen_http_port`| Tomcat http listen port | `8080` |
|`tomcat_listen_http_bind_address`| Service bind address | `localhost` |
|`tomcat_listen_http_enabled`| Enable listening on http port | `yes` |
|`tomcat_listen_https_port`| Enable listening on https port | `8443` |
|`tomcat_listen_ajp_enabled`| Enable listening on ajp port | `False` |
|`tomcat_listen_ajp_address`| Bind address for ajp | `::1` |
|`tomcat_listen_ajp_port`| Tomcat ajp listen port | `8009` |
|`tomcat_listen_ajp_secretRequired`| Enable loading secret from vault | `True` |
|`tomcat_listen_ajp_secret`| Passphrase for vault secret | `secret` |
|`tomcat_vault_name`| Path to tomcat keysore | `vault.keystore` |
|`tomcat_vault_enable`| Enable value | `False` |
|`tomcat_vault_alias`| Alias for loading from vault | `my_vault` |
|`tomcat_vault_storepass`| Tomcat keystore password | `123456` |
|`tomcat_vault_iteration`| TODO document argument | `44` |
|`tomcat_vault_salt`| Salt for encrypting tomcat vault | `1234abcd` |
|`tomcat_vault_properties`| Relative path to vault.properties | `/conf/vault.properties` |
|`tomcat_modcluster_enable`| Enable mod_cluster module | `False` |
|`tomcat_modcluster_ip`| Bind address for mod_cluster | `127.0.0.1` |
|`tomcat_modcluster_port`| mod_cluster port | `6666` |
|`tomcat_modcluster_connector_port`| mod_cluster connector port | `6666` |
|`tomcat_modcluster_advertise`| Enable mod_cluster advertising | `false` |
|`tomcat_modcluster_stickySession`| Enable mod_cluster sticky sessions | `true` |
|`tomcat_modcluster_stickySessionForce`| Force use of sticky sessions | `false` |
|`tomcat_modcluster_stickySessionRemove`| Remove sticky session from cookies | `true` |
|`tomcat_systemd_enabled`| Enable tomcat systemd unit | `False` |
|`tomcat_systemd_script_interpreter`| Interpreter for systemd unit | `bash` |
|`tomcat_systemd_script_shebang`| Customize sysVinit script sheband | `#!/bin/{{ tomcat_systemd_script_interpreter }}` |
|`tomcat_service_name`| Name for the systemd unit | `tomcat.service` |
|`tomcat_service_conf`| Absolute path to tomcat.conf | `{{ tomcat_home }}/conf/tomcat.conf` |
|`tomcat_service_script`| Tomcat sysVinit script | `{{ tomcat_home }}/bin/systemd-service.sh` |
|`tomcat_service_systemd`| Tomcat systemd unit | `/usr/lib/systemd/system/tomcat.service` |
|`tomcat_service_systemd_pidfile`| Absolute path to tomcat PIDfile | `{{ tomcat_home }}/tomcat.pidfile` |
|`tomcat_service_systemd_type`| Systemd unit type | `simple` |



Role Variables
--------------

* No required variables.
<!--end argument_specs-->


Example Playbooks
--------------
'''
---
- hosts: all
  tasks:
    - name: "Include tomcat"
      include_role:
        name: "jws"
'''
