# confluent.variables

Below are the supported variables for the role confluent.variables

***

### jolokia_enabled

Boolean to enable Jolokia Agent installation and configuration on all components

Default:  true

***

### jolokia_jar_path

Full path to download the Jolokia Agent Jar

Default:  /opt/jolokia/jolokia.jar

***

### jolokia_auth_mode

Authentication Mode for Jolokia Agent. Possible values: none, basic. If selecting basic, you must set jolokia_user and jolokia_password

Default:  none

***

### jolokia_user

Username for Jolokia Agent when using Basic Auth

Default:  admin

***

### jolokia_password

Password for Jolokia Agent when using Basic Auth

Default:  password

***

### jmxexporter_enabled

Boolean to enable Prometheus Exporter Agent installation and configuration on all components

Default:  false

***

### jmxexporter_jar_path

Full path to download the Prometheus Exporter Agent Jar

Default:  /opt/prometheus/jmx_prometheus_javaagent.jar

***

### fips_enabled

Boolean to have cp-ansible configure components with FIPS security settings

Default:  false

***

### custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration across all components

Default:  true

***

### kerberos_configure

Boolean to configure Kerberos krb5.conf file, must also set kerberos.realm, keberos.kdc_hostname, kerberos.admin_hostname, where kerberos is a dictionary

Default:  true

***

### confluent_server_enabled

Boolean to install commercially licensed confluent-server instead of community version: confluent-kafka

Default:  true

***

### health_checks_enabled

Boolean to enable health checks on all components

Default:  true

***

### zookeeper_health_checks_enabled

Boolean to enable health checks on Zookeeper

Default:  "{{health_checks_enabled}}"

***

### kafka_broker_health_checks_enabled

Boolean to enable health checks on Kafka

Default:  "{{health_checks_enabled}}"

***

### schema_registry_health_checks_enabled

Boolean to enable health checks on Schema Registry

Default:  "{{health_checks_enabled}}"

***

### kafka_connect_health_checks_enabled

Boolean to enable health checks on Kafka Connect

Default:  "{{health_checks_enabled}}"

***

### kafka_rest_health_checks_enabled

Boolean to enable health checks on Rest Proxy

Default:  "{{health_checks_enabled}}"

***

### ksql_health_checks_enabled

Boolean to enable health checks on ksqlDB

Default:  "{{health_checks_enabled}}"

***

### control_center_health_checks_enabled

Boolean to enable health checks on Control Center

Default:  "{{health_checks_enabled}}"

***

### monitoring_interceptors_enabled

Boolean to configure Monitoring Interceptors on ksqlDB, Rest Proxy, and Connect. Defaults to true if Control Center in inventory. Enable if you wish to have monitoring interceptors to report to a centralized monitoring cluster.

Default:  "{{ 'control_center' in groups }}"

***

### installation_method

The method of installation. Valid values are "package" or "archive". If "archive" is selected then services will not be installed via the use of yum or apt, but will instead be installed via expanding the target .tar.gz file from the Confluent archive into the path defined by `archive_destination_path`. Configuration files are also kept in this directory structure instead of `/etc`. SystemD service units are copied from the ardhive for each target service and overrides are created pointing at the new paths. The "package" installation method is the default behavior that utilizes yum/apt.

Default:  "package"

***

### archive_destination_path

The path the downloaded archive is expanded into. Using the default with a `confluent_package_version` of *5.5.1* results in the following installation path `/opt/confluent/confluent-5.5.1/` that contains directories such as `bin` and `share`, but may be overridden usinf the `binary_base_path` property.

Default:  "/opt/confluent"

***

### archive_config_base_path

If the installation_method is 'archive' then this will be the base path for the configuration files, otherwise configuration files are in the default /etc locations. For example, configuration files may be placed in `/opt/confluent/etc` using this variable.

Default:  "{{ archive_destination_path }}"

***

### confluent_cli_download_enabled

Boolean to have cp-ansible download the Confluent CLI

Default:  "{{rbac_enabled or secrets_protection_enabled}}"

***

### confluent_cli_path

Full path on hosts to install the Confluent CLI

Default:  /usr/local/bin/confluent

***

### sasl_protocol

SASL Mechanism to set on all Kafka Listeners. Configures all components to use that mechanism for authentication. Possible options none, kerberos, plain, scram

Default:  none

***

### ssl_enabled

Boolean to configure components with TLS Encryption. Also manages Java Keystore creation

Default:  false

***

### ssl_mutual_auth_enabled

Boolean to enable mTLS Authentication on all components. Configures all components to use mTLS for authentication into Kafka

Default:  false

***

### self_signed

Boolean to create Keystores with Self Signed Certificates, defaults to true. Alternatively can use ssl_provided_keystore_and_truststore or ssl_custom_certs

Default:  "{{ false if ssl_provided_keystore_and_truststore|bool or ssl_custom_certs|bool else true }}"

***

### regenerate_ca

Boolean to have reruns of all.yml regenerate the certificate authority used for self signed certs

Default:  true

***

### regenerate_keystore_and_truststore

Boolean to have reruns of all.yml recreate Keystores

Default:  true

***

### ssl_provided_keystore_and_truststore

Boolean for TLS Encryption option to provide own Host Keystores.

Default:  false

***

### ssl_keystore_filepath

Full path to host specific keystore on ansible control node. Used with ssl_provided_keystore_and_truststore: true. May set per host, or use inventory_hostname variable eg "/tmp/certs/{{inventory_hostname}}-keystore.jks"

Default:  ""

***

### ssl_keystore_key_password

Keystore Key Password for host specific keystore. Used with ssl_provided_keystore_and_truststore: true. May set per host if keystores have unique passwords

Default:  ""

***

### ssl_keystore_store_password

Keystore Password for host specific keystore. Used with ssl_provided_keystore_and_truststore: true. May set per host if keystores have unique passwords

Default:  ""

***

### ssl_truststore_filepath

Full path to host specific truststore on ansible control node. Used with ssl_provided_keystore_and_truststore: true. Can share same keystore for all components if it contains all ca certs used to sign host certificates

Default:  ""

***

### ssl_truststore_password

Keystore Password for host specific truststore. Used with ssl_provided_keystore_and_truststore: true

Default:  ""

***

### ssl_truststore_ca_cert_alias

Keystore alias for ca certificate

Default:  ""

***

### ssl_custom_certs

Boolean for TLS Encryption option to provide own Host Certificates. Must also set ssl_ca_cert_filepath, ssl_signed_cert_filepath, ssl_key_filepath, ssl_key_password

Default:  false

***

### ssl_ca_cert_filepath

Full path to CA Certificate Bundle on ansible control node. Used with ssl_custom_certs: true

Default:  ""

***

### ssl_signed_cert_filepath

Full path to host specific signed cert on ansible control node. Used with ssl_custom_certs: true. May set per host, or use inventory_hostname variable eg "/tmp/certs/{{inventory_hostname}}-signed.crt"

Default:  ""

***

### ssl_key_filepath

Full path to host specific key on ansible control node. Used with ssl_custom_certs: true. May set per host, or use inventory_hostname variable eg "/tmp/certs/{{inventory_hostname}}-key.pem"

Default:  ""

***

### ssl_key_password

Password to host specific key. Do not set if key does not require password. Used with ssl_custom_certs: true.

Default:  ""

***

### ssl_custom_certs_remote_src

Boolean stating certs and keys are already on hosts. Used with ssl_custom_certs: true.

Default:  false

***

### zookeeper_user

Only use to customize Linux User Zookeeper Service runs with. User must exist on host.

Default:  "{{zookeeper_default_user}}"

***

### zookeeper_group

Only use to customize Linux Group Zookeeper Service user belongs to. Group must exist on host.

Default:  "{{zookeeper_default_group}}"

***

### zookeeper_ssl_enabled

Boolean to configure zookeeper with TLS Encryption. Also manages Java Keystore creation

Default:  "{{ssl_enabled}}"

***

### zookeeper_ssl_mutual_auth_enabled

Boolean to enable mTLS Authentication on Zookeeper (Server to Server and Client to Server). Configures kafka to authenticate with mTLS.

Default:  "{{ssl_mutual_auth_enabled}}"

***

### zookeeper_client_port

Port for Kafka to Zookeeper connections. NOTE- 2181 will be configured for zk health checks

Default:  "{{'2182' if zookeeper_ssl_enabled|bool else '2181'}}"

***

### zookeeper_sasl_protocol

SASL Mechanism for Zookeeper Server to Server and Server to Client Authentication. Options are none, kerberos, digest. Server to server auth only working for digest-md5

Default:  "{{sasl_protocol if sasl_protocol == 'kerberos' else 'none'}}"

***

### zookeeper_jolokia_enabled

Boolean to enable Jolokia Agent installation and configuration on zookeeper

Default:  "{{jolokia_enabled}}"

***

### zookeeper_jolokia_port

Port to expose jolokia metrics. Beware of port collisions if colocating components on same host

Default:  7770

***

### zookeeper_jolokia_ssl_enabled

Boolean to enable TLS encryption on Zookeeper jolokia metrics

Default:  "{{ zookeeper_ssl_enabled }}"

***

### zookeeper_jolokia_config

Path on Zookeeper host for Jolokia Configuration file

Default:  "{{ archive_config_base_path if installation_method == 'archive' else '' }}/etc/kafka/zookeeper_jolokia.properties"

***

### zookeeper_jolokia_auth_mode

Authentication Mode for Zookeeper's Jolokia Agent. Possible values: none, basic. If selecting basic, you must set zookeeper_jolokia_user and zookeeper_jolokia_password

Default:  "{{jolokia_auth_mode}}"

***

### zookeeper_jolokia_user

Username for Zookeeper's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_user}}"

***

### zookeeper_jolokia_password

Password for Zookeeper's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_password}}"

***

### zookeeper_jmxexporter_enabled

Boolean to enable Prometheus Exporter Agent installation and configuration on zookeeper

Default:  "{{jmxexporter_enabled}}"

***

### zookeeper_jmxexporter_port

Port to expose prometheus metrics. Beware of port collisions if colocating components on same host

Default:  8079

***

### zookeeper_peer_port

Zookeeper peer port

Default:  2888

***

### zookeeper_leader_port

Zookeeper leader port

Default:  3888

***

### zookeeper_copy_files

Use to copy files from control node to zookeeper hosts. Set to list of dictionaries with keys: source_path (full path of file on control node) and destination_path (full path to copy file to)

Default:  []

***

### zookeeper_custom_properties

Use to set custom zookeeper properties. This variable is a dictionary. Put values true/false in quotation marks to perserve case. NOTE- zookeeper.properties is deprecated.

Default:  "{{ zookeeper.properties }}"

***

### kafka_broker_configure_multiple_listeners

Boolean to configure more than one kafka listener. Defaults to true. NOTE- kafka_broker_configure_additional_brokers is deprecated

Default:  "{{kafka_broker_configure_additional_brokers}}"

***

### kafka_broker_user

Only use to customize Linux User Kafka Service runs with. User must exist on host.

Default:  "{{kafka_broker_default_user}}"

***

### kafka_broker_group

Only use to customize Linux Group Kafka Service user belongs to. Group must exist on host.

Default:  "{{kafka_broker_default_group}}"

***

### kafka_broker_jolokia_enabled

Boolean to enable Jolokia Agent installation and configuration on kafka

Default:  "{{jolokia_enabled}}"

***

### kafka_broker_jolokia_port

Port to expose kafka jolokia metrics. Beware of port collisions if colocating components on same host

Default:  7771

***

### kafka_broker_jolokia_ssl_enabled

Boolean to enable TLS encryption on Kafka jolokia metrics

Default:  "{{ ssl_enabled }}"

***

### kafka_broker_jolokia_config

Path on Kafka host for Jolokia Configuration file

Default:  "{{ archive_config_base_path if installation_method == 'archive' else '' }}/etc/kafka/kafka_jolokia.properties"

***

### kafka_broker_jolokia_auth_mode

Authentication Mode for Kafka's Jolokia Agent. Possible values: none, basic. If selecting basic, you must set kafka_broker_jolokia_user and kafka_broker_jolokia_password

Default:  "{{jolokia_auth_mode}}"

***

### kafka_broker_jolokia_user

Username for Kafka's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_user}}"

***

### kafka_broker_jolokia_password

Password for Kafka's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_password}}"

***

### kafka_broker_jmxexporter_enabled

Boolean to enable Prometheus Exporter Agent installation and configuration on kafka

Default:  "{{jmxexporter_enabled}}"

***

### kafka_broker_jmxexporter_port

Port to expose prometheus metrics. Beware of port collisions if colocating components on same host

Default:  8080

***

### kafka_broker_copy_files

Use to copy files from control node to kafka hosts. Set to list of dictionaries with keys: source_path (full path of file on control node) and destination_path (full path to copy file to)

Default:  []

***

### kafka_broker_default_internal_replication_factor

Replication Factor for internal topics. Defaults to the minimum of the number of brokers and 3

Default:  "{{ [ groups['kafka_broker'] | default(['localhost']) | length, 3 ] | min }}"

***

### kafka_broker_metrics_reporter_enabled

Boolean to enable the kafka's metrics reporter. Defaults to true if Control Center in inventory. Enable if you wish to have metrics reported to a centralized monitoring cluster.

Default:  "{{ 'control_center' in groups }}"

***

### kafka_broker_custom_properties

Use to set custom kafka properties. This variable is a dictionary. Put values true/false in quotation marks to perserve case. NOTE- kafka_broker.properties is deprecated.

Default:  "{{ kafka_broker.properties }}"

***

### kafka_broker_rest_proxy_enabled

Boolean to enable the embedded rest proxy within Kafka. NOTE- Embedded Rest Proxy must be enabled if RBAC is enabled and Confluent Server must be enabled

Default:  "{{confluent_server_enabled}}"

***

### schema_registry_user

Only use to customize Linux User Schema Registry Service runs with. User must exist on host.

Default:  "{{schema_registry_default_user}}"

***

### schema_registry_group

Only use to customize Linux Group Schema Registry Service user belongs to. Group must exist on host.

Default:  "{{schema_registry_default_group}}"

***

### schema_registry_listener_port

Port Schema Registry API exposed over

Default:  8081

***

### schema_registry_ssl_enabled

Boolean to configure schema registry with TLS Encryption. Also manages Java Keystore creation

Default:  "{{ssl_enabled}}"

***

### schema_registry_ssl_mutual_auth_enabled

Boolean to enable mTLS Authentication on Schema Registry

Default:  "{{ ssl_mutual_auth_enabled }}"

***

### schema_registry_jolokia_enabled

Boolean to enable Jolokia Agent installation and configuration on schema registry

Default:  "{{jolokia_enabled}}"

***

### schema_registry_jolokia_port

Port to expose schema registry jolokia metrics. Beware of port collisions if colocating components on same host

Default:  7772

***

### schema_registry_jolokia_ssl_enabled

Boolean to enable TLS encryption on Schema Registry jolokia metrics

Default:  "{{ schema_registry_ssl_enabled }}"

***

### schema_registry_jolokia_config

Path on Schema Registry host for Jolokia Configuration file

Default:  "{{ archive_config_base_path if installation_method == 'archive' else '' }}/etc/schema-registry/schema_registry_jolokia.properties"

***

### schema_registry_jolokia_auth_mode

Authentication Mode for Schema Registry's Jolokia Agent. Possible values: none, basic. If selecting basic, you must set schema_registry_jolokia_user and schema_registry_jolokia_password

Default:  "{{jolokia_auth_mode}}"

***

### schema_registry_jolokia_user

Username for Schema Registry's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_user}}"

***

### schema_registry_jolokia_password

Password for Schema Registry's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_password}}"

***

### schema_registry_jmxexporter_enabled

Boolean to enable Prometheus Exporter Agent installation and configuration on schema registry

Default:  "{{jmxexporter_enabled}}"

***

### schema_registry_jmxexporter_port

Port to expose prometheus metrics. Beware of port collisions if colocating components on same host

Default:  8078

***

### schema_registry_copy_files

Use to copy files from control node to schema registry hosts. Set to list of dictionaries with keys: source_path (full path of file on control node) and destination_path (full path to copy file to)

Default:  []

***

### schema_registry_custom_properties

Use to set custom schema registry properties. This variable is a dictionary. Put values true/false in quotation marks to perserve case. NOTE- kafka_broker.properties is deprecated.

Default:  "{{ schema_registry.properties }}"

***

### kafka_rest_user

Only use to customize Linux User Rest Proxy Service runs with. User must exist on host.

Default:  "{{kafka_rest_default_user}}"

***

### kafka_rest_group

Only use to customize Linux Group Rest Proxy Service user belongs to. Group must exist on host.

Default:  "{{kafka_rest_default_group}}"

***

### kafka_rest_port

Port Rest Proxy API exposed over

Default:  8082

***

### kafka_rest_ssl_enabled

Boolean to configure Rest Proxy with TLS Encryption. Also manages Java Keystore creation

Default:  "{{ssl_enabled}}"

***

### kafka_rest_ssl_mutual_auth_enabled

Boolean to enable mTLS Authentication on Rest Proxy

Default:  "{{ ssl_mutual_auth_enabled }}"

***

### kafka_rest_jolokia_enabled

Boolean to enable Jolokia Agent installation and configuration on Rest Proxy

Default:  "{{jolokia_enabled}}"

***

### kafka_rest_jolokia_port

Port to expose Rest Proxy jolokia metrics. Beware of port collisions if colocating components on same host

Default:  7775

***

### kafka_rest_jolokia_ssl_enabled

Boolean to enable TLS encryption on Rest Proxy jolokia metrics

Default:  "{{ kafka_rest_ssl_enabled }}"

***

### kafka_rest_jolokia_config

Path on Rest Proxy host for Jolokia Configuration file

Default:  "{{ archive_config_base_path if installation_method == 'archive' else '' }}/etc/kafka-rest/kafka_rest_jolokia.properties"

***

### kafka_rest_jolokia_auth_mode

Authentication Mode for Rest Proxy's Jolokia Agent. Possible values: none, basic. If selecting basic, you must set schema_registry_jolokia_user and schema_registry_jolokia_password

Default:  "{{jolokia_auth_mode}}"

***

### kafka_rest_jolokia_user

Username for Rest Proxy's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_user}}"

***

### kafka_rest_jolokia_password

Password for Rest Proxy's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_password}}"

***

### kafka_rest_jmxexporter_enabled

Boolean to enable Prometheus Exporter Agent installation and configuration on Rest Proxy

Default:  "{{jmxexporter_enabled}}"

***

### kafka_rest_jmxexporter_port

Port to expose prometheus metrics. Beware of port collisions if colocating components on same host

Default:  8075

***

### kafka_rest_copy_files

Use to copy files from control node to schema registry hosts. Set to list of dictionaries with keys: source_path (full path of file on control node) and destination_path (full path to copy file to)

Default:  []

***

### kafka_rest_custom_properties

Use to set custom Rest Proxy properties. This variable is a dictionary. Put values true/false in quotation marks to perserve case. NOTE- kafka_rest.properties is deprecated.

Default:  "{{ kafka_rest.properties }}"

***

### kafka_rest_monitoring_interceptors_enabled

Boolean to configure Monitoring Interceptors on Rest Proxy.

Default:  "{{ monitoring_interceptors_enabled }}"

***

### kafka_connect_user

Only use to customize Linux User Connect Service runs with. User must exist on host.

Default:  "{{kafka_connect_default_user}}"

***

### kafka_connect_group

Only use to customize Linux Group Connect Service user belongs to. Group must exist on host.

Default:  "{{kafka_connect_default_group}}"

***

### kafka_connect_rest_port

Port Connect API exposed over

Default:  8083

***

### kafka_connect_ssl_enabled

Boolean to configure Connect with TLS Encryption. Also manages Java Keystore creation

Default:  "{{ssl_enabled}}"

***

### kafka_connect_ssl_mutual_auth_enabled

Boolean to enable mTLS Authentication on Connect

Default:  "{{ ssl_mutual_auth_enabled }}"

***

### kafka_connect_jolokia_enabled

Boolean to enable Jolokia Agent installation and configuration on Connect

Default:  "{{jolokia_enabled}}"

***

### kafka_connect_jolokia_port

Port to expose Connect jolokia metrics. Beware of port collisions if colocating components on same host

Default:  7773

***

### kafka_connect_jolokia_ssl_enabled

Boolean to enable TLS encryption on Connect jolokia metrics

Default:  "{{ kafka_connect_ssl_enabled }}"

***

### kafka_connect_jolokia_config

Path on Connect host for Jolokia Configuration file

Default:  "{{ archive_config_base_path if installation_method == 'archive' else '' }}/etc/kafka/kafka_connect_jolokia.properties"

***

### kafka_connect_jolokia_auth_mode

Authentication Mode for Connect's Jolokia Agent. Possible values: none, basic. If selecting basic, you must set schema_registry_jolokia_user and schema_registry_jolokia_password

Default:  "{{jolokia_auth_mode}}"

***

### kafka_connect_jolokia_user

Username for Connect's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_user}}"

***

### kafka_connect_jolokia_password

Password for Connect's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_password}}"

***

### kafka_connect_jmxexporter_enabled

Boolean to enable Prometheus Exporter Agent installation and configuration on Connect

Default:  "{{jmxexporter_enabled}}"

***

### kafka_connect_jmxexporter_port

Port to expose connect prometheus metrics. Beware of port collisions if colocating components on same host

Default:  8077

***

### kafka_connect_copy_files

Use to copy files from control node to connect hosts. Set to list of dictionaries with keys: source_path (full path of file on control node) and destination_path (full path to copy file to)

Default:  []

***

### kafka_connect_group_id

Connect Service Group Id. Customize when configuring multiple connect clusters in same inventory

Default:  connect-cluster

***

### kafka_connect_default_internal_replication_factor

Replication Factor for connect internal topics. Defaults to the minimum of the number of brokers and 3

Default:  "{{ [ groups['kafka_broker'] | default(['localhost']) | length, 3 ] | min }}"

***

### kafka_connect_secret_registry_enabled

Boolean to enable and configure Connect Secret Registry

Default:  "{{rbac_enabled}}"

***

### kafka_connect_secret_registry_key

Connect Secret Registry Key

Default:  39ff95832750c0090d84ddf5344583832efe91ef

***

### kafka_connect_custom_properties

Use to set custom Connect properties. This variable is a dictionary. Put values true/false in quotation marks to perserve case. NOTE- kafka_connect.properties is deprecated.

Default:  "{{ kafka_connect.properties }}"

***

### kafka_connect_monitoring_interceptors_enabled

Boolean to configure Monitoring Interceptors on Connect.

Default:  "{{ monitoring_interceptors_enabled }}"

***

### ksql_user

Only use to customize Linux User ksqlDB Service runs with. User must exist on host.

Default:  "{{ksql_default_user}}"

***

### ksql_group

Only use to customize Linux Group ksqlDB Service user belongs to. Group must exist on host.

Default:  "{{ksql_default_group}}"

***

### ksql_listener_port

Port ksqlDB API exposed over

Default:  8088

***

### ksql_ssl_enabled

Boolean to configure ksqlDB with TLS Encryption. Also manages Java Keystore creation

Default:  "{{ssl_enabled}}"

***

### ksql_ssl_mutual_auth_enabled

Boolean to enable mTLS Authentication on ksqlDB

Default:  "{{ ssl_mutual_auth_enabled }}"

***

### ksql_jolokia_enabled

Boolean to enable Jolokia Agent installation and configuration on ksqlDB

Default:  "{{jolokia_enabled}}"

***

### ksql_jolokia_port

Port to expose ksqlDB jolokia metrics. Beware of port collisions if colocating components on same host

Default:  7774

***

### ksql_jolokia_ssl_enabled

Boolean to enable TLS encryption on ksqlDB jolokia metrics

Default:  "{{ ksql_ssl_enabled }}"

***

### ksql_jolokia_config

Path on ksqlDB host for Jolokia Configuration file

Default:  "{{ archive_config_base_path if installation_method == 'archive' else '' }}{{(confluent_package_version is version('5.5.0', '>=')) | ternary('/etc/ksqldb/ksql_jolokia.properties' , '/etc/ksql/ksql_jolokia.properties')}}"

***

### ksql_jolokia_auth_mode

Authentication Mode for ksqlDB's Jolokia Agent. Possible values: none, basic. If selecting basic, you must set schema_registry_jolokia_user and schema_registry_jolokia_password

Default:  "{{jolokia_auth_mode}}"

***

### ksql_jolokia_user

Username for ksqlDB's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_user}}"

***

### ksql_jolokia_password

Password for ksqlDB's Jolokia Agent when using Basic Auth

Default:  "{{jolokia_password}}"

***

### ksql_jmxexporter_enabled

Boolean to enable Prometheus Exporter Agent installation and configuration on ksqlDB

Default:  "{{jmxexporter_enabled}}"

***

### ksql_jmxexporter_port

Port to expose ksqlDB prometheus metrics. Beware of port collisions if colocating components on same host

Default:  8076

***

### ksql_copy_files

Use to copy files from control node to ksqlDB hosts. Set to list of dictionaries with keys: source_path (full path of file on control node) and destination_path (full path to copy file to)

Default:  []

***

### ksql_default_internal_replication_factor

Replication Factor for ksqlDB internal topics. Defaults to the minimum of the number of brokers and 3

Default:  "{{ [ groups['kafka_broker'] | default(['localhost']) | length, 3 ] | min }}"

***

### ksql_service_id

ksqlDB Service ID. Use when configuring multiple ksqldb clusters in the same inventory file.

Default:  default_

***

### ksql_custom_properties

Use to set custom ksqlDB properties. This variable is a dictionary. Put values true/false in quotation marks to perserve case. NOTE- ksql.properties is deprecated.

Default:  "{{ ksql.properties }}"

***

### ksql_monitoring_interceptors_enabled

Boolean to configure Monitoring Interceptors on ksqlDB.

Default:  "{{ monitoring_interceptors_enabled }}"

***

### control_center_user

Only use to customize Linux User Control Center Service runs with. User must exist on host.

Default:  "{{control_center_default_user}}"

***

### control_center_group

Only use to customize Linux Group Control Center Service user belongs to. Group must exist on host.

Default:  "{{control_center_default_group}}"

***

### control_center_port

Port Control Center exposed over

Default:  9021

***

### control_center_listener_hostname

Interface on host for Control Center to listen on

Default:  "0.0.0.0"

***

### control_center_ssl_enabled

Boolean to configure Control Center with TLS Encryption. Also manages Java Keystore creation

Default:  "{{ssl_enabled}}"

***

### control_center_copy_files

Use to copy files from control node to Control Center hosts. Set to list of dictionaries with keys: source_path (full path of file on control node) and destination_path (full path to copy file to)

Default:  []

***

### control_center_default_internal_replication_factor

Replication Factor for Control Center internal topics. Defaults to the minimum of the number of brokers and 3

Default:  "{{ [ groups['kafka_broker'] | default(['localhost']) | length, 3 ] | min }}"

***

### control_center_custom_properties

Use to set custom Control Center properties. This variable is a dictionary. Put values true/false in quotation marks to perserve case. NOTE- control_center.properties is deprecated.

Default:  "{{ control_center.properties }}"

***

### rbac_enabled

Boolean to configure Confluent Platform with RBAC enabled. Creates Rolebindings for all components to function

Default:  false

***

### mds_port

Port to expose MDS Server API on

Default:  8090

***

### kafka_broker_rest_ssl_enabled

Boolean to configure TLS encryption on the Broker Rest endpoint. NOTE- mds_ssl_enabled is now deprecated

Default:  "{{mds_ssl_enabled}}"

***

### mds_super_user

LDAP User which will be granted super user permissions to create role bindings in the MDS

Default:  mds

***

### mds_super_user_password

Password to mds_super_user LDAP User

Default:  password

***

### kafka_broker_ldap_user

LDAP User for Kafkas Embedded Rest Service to authenticate as

Default:  "{{mds_super_user}}"

***

### kafka_broker_ldap_password

Password to kafka_broker_ldap_user LDAP User

Default:  "{{mds_super_user_password}}"

***

### schema_registry_ldap_user

LDAP User for Schema Registry to authenticate as

Default:  schema-registry

***

### schema_registry_ldap_password

Password to schema_registry_ldap_user LDAP User

Default:  password

***

### kafka_connect_ldap_user

LDAP User for Connect to authenticate as

Default:  connect

***

### kafka_connect_ldap_password

Password to kafka_connect_ldap_user LDAP User

Default:  password

***

### ksql_ldap_user

LDAP User for ksqlDB to authenticate as

Default:  ksql

***

### ksql_ldap_password

Password to ksql_ldap_user LDAP User

Default:  password

***

### kafka_rest_ldap_user

LDAP User for Rest Proxy to authenticate as

Default:  kafka-rest

***

### kafka_rest_ldap_password

Password to kafka_rest_ldap_user LDAP User

Default:  password

***

### control_center_ldap_user

LDAP User for Control Center to authenticate as

Default:  control-center

***

### control_center_ldap_password

Password to control_center_ldap_user LDAP User

Default:  password

***

### external_mds_enabled

Boolean to describe if kafka group should be configured with an External MDS Kafka Cluster. If set to true, you must also set mds_broker_bootstrap_servers, mds_broker_listener, kafka_broker_rest_ssl_enabled

Default:  false

***

### mds_broker_bootstrap_servers

Kafka hosts and listener ports on the Kafka Cluster acting as an external MDS Server. mds_broker_listener dictionary must describe its security settings. Must be configured if external_mds_enabled: true

Default:  localhost:9092

***

### mds_broker_listener

Listener Dictionary that describes how kafka clusters connect to MDS Kafka cluster. Make sure it contains the keys: ssl_enabled, ssl_mutual_auth_enabled, sasl_protocol

Default: 

***

### mds_bootstrap_server_urls

Comma separated urls for mds servers. Only set if external_mds_enabled: true

Default:  "{{mds_http_protocol}}://{{ groups['kafka_broker'] | default(['localhost']) | join(':' + mds_port|string + ',' + mds_http_protocol + '://') }}:{{mds_port}}"

***

### rbac_component_additional_system_admins

List of users to be granted system admin Role Bindings across all components

Default:  []

***

### kafka_broker_additional_system_admins

List of users to be granted system admin Role Bindings on the Kafka Cluster

Default:  "{{rbac_component_additional_system_admins}}"

***

### schema_registry_additional_system_admins

List of users to be granted system admin Role Bindings on the Schema Registry Cluster

Default:  "{{rbac_component_additional_system_admins}}"

***

### ksql_additional_system_admins

List of users to be granted system admin Role Bindings on the ksqlDB Cluster

Default:  "{{rbac_component_additional_system_admins}}"

***

### kafka_connect_additional_system_admins

List of users to be granted system admin Role Bindings on the Connect Cluster

Default:  "{{rbac_component_additional_system_admins}}"

***

### control_center_additional_system_admins

List of users to be granted system admin Role Bindings on the Control Center Cluster

Default:  "{{rbac_component_additional_system_admins}}"

***

### secrets_protection_enabled

Boolean to enable secrets protection on all components except Rest Proxy

Default:  false

***

### secrets_protection_masterkey

Masterkey generated by the Confluent Secret CLI. If empty and secrets protection is enabled, then a master key will be randomly generated.

Default:  ""

***

### secrets_protection_security_file

Security file generated by the Confluent Secret CLI. If empty and secrets protection is enabled, then a security file will be randomly generated.

Default:  generated_ssl_files/security.properties

***

### kafka_broker_secrets_protection_enabled

Boolean to enable secrets protection in Kafka broker.

Default:  "{{secrets_protection_enabled}}"

***

### kafka_broker_secrets_protection_encrypt_passwords

Boolean to encrypt all properties containing 'password' for Kafka.

Default:  "{{kafka_broker_secrets_protection_enabled}}"

***

### kafka_broker_secrets_protection_encrypt_properties

List of Kafka properties to encrypt. Can be used in addition to kafka_broker_secrets_protection_encrypt_passwords.

Default:  []

***

### schema_registry_secrets_protection_enabled

Boolean to enable secrets protection in schema registry.

Default:  "{{secrets_protection_enabled}}"

***

### schema_registry_secrets_protection_encrypt_passwords

Boolean to encrypt all properties containing 'password' for Schema Registry.

Default:  "{{schema_registry_secrets_protection_enabled}}"

***

### schema_registry_secrets_protection_encrypt_properties

List of Schema Registry properties to encrypt. Can be used in addition to schema_registry_secrets_protection_encrypt_passwords.

Default:  []

***

### kafka_connect_secrets_protection_enabled

Boolean to enable secrets protection in Connect.

Default:  "{{secrets_protection_enabled}}"

***

### kafka_connect_secrets_protection_encrypt_passwords

Boolean to encrypt all properties containing 'password' for Connect.

Default:  "{{kafka_connect_secrets_protection_enabled}}"

***

### kafka_connect_secrets_protection_encrypt_properties

List of Connect properties to encrypt. Can be used in addition to kafka_connect_secrets_protection_encrypt_passwords.

Default:  []

***

### kafka_rest_secrets_protection_enabled

Boolean to enable secrets protection in Rest Proxy.

Default:  "{{secrets_protection_enabled}}"

***

### kafka_rest_secrets_protection_encrypt_passwords

Boolean to encrypt all properties containing 'password' for Rest Proxy.

Default:  "{{kafka_rest_secrets_protection_enabled}}"

***

### kafka_rest_secrets_protection_encrypt_properties

List of Rest Proxy properties to encrypt. Can be used in addition to kafka_rest_secrets_protection_encrypt_passwords.

Default:  []

***

### ksql_secrets_protection_enabled

Boolean to enable secrets protection in KSQL.

Default:  "{{secrets_protection_enabled}}"

***

### ksql_secrets_protection_encrypt_passwords

Boolean to encrypt all properties containing 'password' for KSQL.

Default:  "{{ksql_secrets_protection_enabled}}"

***

### ksql_secrets_protection_encrypt_properties

List of KSQL properties to encrypt. Can be used in addition to ksql_secrets_protection_encrypt_passwords.

Default:  []

***

### control_center_secrets_protection_enabled

Boolean to enable secrets protection in Control Center.

Default:  "{{secrets_protection_enabled}}"

***

### control_center_secrets_protection_encrypt_passwords

Boolean to encrypt all properties containing 'password' for Control Center.

Default:  "{{control_center_secrets_protection_enabled}}"

***

### control_center_secrets_protection_encrypt_properties

List of Control Center properties to encrypt. Can be used in addition to control_center_secrets_protection_encrypt_passwords.

Default:  []

***

### telemetry_enabled

Boolean to configure Telemetry. Must also set telemetry_api_key and telemetry_api_secret

Default:  false

***

### telemetry_api_key

API Key used by Telemetry. Mandatory variable for Telemetry

Default:  ""

***

### telemetry_api_secret

API Secret used by Telemetry. Mandatory variable for Telemetry

Default:  ""

***

### telemetry_proxy_url

Proxy URL used by Telemetry. Only set if using a Proxy Server

Default:  ""

***

### telemetry_proxy_username

Username for Proxy Server used by Telemetry. Only set if Proxy Server requires authentication

Default:  ""

***

### telemetry_proxy_password

Password for Proxy Server used by Telemetry. Only set if Proxy Server requires authentication

Default:  ""

***

### kafka_broker_telemetry_enabled

Boolean to configure Telemetry on Kafka. Must also set telemetry_api_key and telemetry_api_secret

Default:  "{{telemetry_enabled}}"

***

### kafka_broker_telemetry_ansible_labels_enabled

Boolean to send cp-ansible Telemetry Metrics from Kafka. Currently only sends cp-ansible version data

Default:  "{{kafka_broker_telemetry_enabled}}"

***

### schema_registry_telemetry_enabled

Boolean to configure Telemetry on Schema Registry. Must also set telemetry_api_key and telemetry_api_secret

Default:  "{{telemetry_enabled}}"

***

### schema_registry_telemetry_ansible_labels_enabled

Boolean to send cp-ansible Telemetry Metrics from Schema Registry. Currently only sends cp-ansible version data

Default:  "{{schema_registry_telemetry_enabled}}"

***

### kafka_connect_telemetry_enabled

Boolean to configure Telemetry on Connect. Must also set telemetry_api_key and telemetry_api_secret

Default:  "{{telemetry_enabled}}"

***

### kafka_connect_telemetry_ansible_labels_enabled

Boolean to send cp-ansible Telemetry Metrics from Connect. Currently only sends cp-ansible version data

Default:  "{{kafka_connect_telemetry_enabled}}"

***

### kafka_rest_telemetry_enabled

Boolean to configure Telemetry on Rest Proxy. Must also set telemetry_api_key and telemetry_api_secret

Default:  "{{telemetry_enabled}}"

***

### kafka_rest_telemetry_ansible_labels_enabled

Boolean to send cp-ansible Telemetry Metrics from Rest Proxy. Currently only sends cp-ansible version data

Default:  "{{kafka_rest_telemetry_enabled}}"

***

### ksql_telemetry_enabled

Boolean to configure Telemetry on ksqlDB. Must also set telemetry_api_key and telemetry_api_secret

Default:  "{{telemetry_enabled}}"

***

### ksql_telemetry_ansible_labels_enabled

Boolean to send cp-ansible Telemetry Metrics from ksqlDB. Currently only sends cp-ansible version data

Default:  "{{ksql_telemetry_enabled}}"

***

### control_center_telemetry_enabled

Boolean to configure Telemetry on Control Center. Must also set telemetry_api_key and telemetry_api_secret

Default:  "{{telemetry_enabled}}"

***

### control_center_telemetry_ansible_labels_enabled

Boolean to send cp-ansible Telemetry Metrics from Control Center. Currently only sends cp-ansible version data

Default:  "{{control_center_telemetry_enabled}}"

***

### mds_health_check_user

User for authenticated MDS Health Check. Only relevant if rbac_enabled: true.

Default:  "{{mds_super_user}}"

***

### mds_health_check_password

Password for authenticated MDS Health Check. Only relevant if rbac_enabled: true.

Default:  "{{mds_super_user_password}}"

***

### kafka_broker_rest_health_check_user

User for authenticated Kafka Admin API Health Check. Set if using customized security like Basic Auth.

Default:  "{{mds_super_user}}"

***

### kafka_broker_rest_health_check_password

Password for authenticated Kafka Admin API Health Check. Set if using customized security like Basic Auth.

Default:  "{{mds_super_user_password}}"

***

### schema_registry_health_check_user

User for authenticated Schema Registry Health Check. Set if using customized security like Basic Auth.

Default:  "{{schema_registry_ldap_user}}"

***

### schema_registry_health_check_password

Password for authenticated Schema Registry Health Check. Set if using customized security like Basic Auth.

Default:  "{{schema_registry_ldap_password}}"

***

### kafka_connect_health_check_user

User for authenticated Connect Health Check. Set if using customized security like Basic Auth.

Default:  "{{kafka_connect_ldap_user}}"

***

### kafka_connect_health_check_password

Password for authenticated Connect Health Check. Set if using customized security like Basic Auth.

Default:  "{{kafka_connect_ldap_password}}"

***

### ksql_health_check_user

User for authenticated ksqlDB Health Check. Set if using customized security like Basic Auth.

Default:  "{{ksql_ldap_user}}"

***

### ksql_health_check_password

Password for authenticated ksqlDB Health Check. Set if using customized security like Basic Auth.

Default:  "{{ksql_ldap_password}}"

***

### kafka_rest_health_check_user

User for authenticated Rest Proxy Health Check. Set if using customized security like Basic Auth.

Default:  "{{kafka_rest_ldap_user}}"

***

### kafka_rest_health_check_password

Password for authenticated Rest Proxy Health Check. Set if using customized security like Basic Auth.

Default:  "{{kafka_rest_ldap_password}}"

***

### control_center_health_check_user

User for authenticated Control Center Health Check. Set if using customized security like Basic Auth.

Default:  "{{control_center_ldap_user}}"

***

### control_center_health_check_password

Password for authenticated Control Center Health Check. Set if using customized security like Basic Auth.

Default:  "{{control_center_ldap_password}}"

***

# confluent.common

Below are the supported variables for the role confluent.common

***

### repository_configuration

Configures package repositories on hosts. By default will configure confluent's deb/yum repositories. Possible options: none, confluent, custom. Must also set custom_yum_repofile_filepath or custom_apt_repo_filepath if using custom. Note: vars custom_apt_repo and custom_yum_repofile are deprecated

Default:  "{{'custom' if custom_apt_repo|bool or custom_yum_repofile else 'confluent'}}"

***

### custom_yum_repofile_filepath

Full path on control node to custom yum repo file, must also set repository_configuration to custom

Default:  ""

***

### custom_apt_repo_filepath

Full path on control node to custom apt repo file, must also set repository_configuration to custom

Default:  ""

***

### confluent_common_repository_baseurl

Base URL for Confluent's RPM and Debian Package Repositories

Default:  "https://packages.confluent.io"

***

### install_java

Boolean to have cp-ansible install Java on hosts

Default:  true

***

### redhat_java_package_name

Java Package to install on RHEL/Centos hosts. Possible values java-1.8.0-openjdk or java-11-openjdk

Default:  java-1.8.0-openjdk

***

### debian_java_package_name

Java Package to install on Debian hosts. Possible values openjdk-8-jdk or openjdk-11-jdk

Default:  openjdk-8-jdk

***

### ubuntu_java_package_name

Java Package to install on Ubuntu hosts. Possible values openjdk-8-jdk or openjdk-11-jdk

Default:  openjdk-8-jdk

***

### ubuntu_java_repository

Deb Repository to use for Java Installation

Default:  ppa:openjdk-r/ppa

***

### jolokia_version

Version of Jolokia Agent Jar to Download

Default:  1.6.2

***

### jolokia_jar_url

Full URL used for Jolokia Agent Jar Download

Default:  "http://search.maven.org/remotecontent?filepath=org/jolokia/jolokia-jvm/{{jolokia_version}}/jolokia-jvm-{{jolokia_version}}-agent.jar"

***

### jmxexporter_jar_url

Full URL used for Prometheus Exporter Jar Download

Default:  https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.12.0/jmx_prometheus_javaagent-0.12.0.jar

***

### confluent_archive_file_source

A path reference to a local archive file or URL. By default this is the URL from Confluent's repositories. In an ansible-pull deployment this could be set to a local file such as "~/.ansible/pull/{{inventory_hostname}}/{{confluent_archive_file_name}}".

Default:  "{{confluent_common_repository_baseurl}}/archive/{{confluent_repo_version}}/confluent-{{confluent_package_version}}.tar.gz"

***

### confluent_archive_file_remote

Set to true to indicate the archive file is remote (i.e. already on the target node) or a URL. Set to false if the archive file is on the control node.

Default:  true

***

# confluent.control_center

Below are the supported variables for the role confluent.control_center

***

### control_center_custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration

Default:  "{{ custom_log4j }}"

***

### control_center_custom_java_args

Custom Java Args to add to the Control Center Process

Default:  ""

***

### control_center_rocksdb_path

Full Path to the RocksDB Data Directory. If left as empty string, cp-ansible will not configure RocksDB

Default:  ""

***

# confluent.kafka_broker

Below are the supported variables for the role confluent.kafka_broker

***

### kafka_broker_custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration

Default:  "{{ custom_log4j }}"

***

### kafka_broker_custom_java_args

Custom Java Args to add to the Kafka Process

Default:  ""

***

# confluent.kafka_connect

Below are the supported variables for the role confluent.kafka_connect

***

### kafka_connect_custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration

Default:  "{{ custom_log4j }}"

***

### kafka_connect_custom_java_args

Custom Java Args to add to the Connect Process

Default:  ""

***

# confluent.kafka_rest

Below are the supported variables for the role confluent.kafka_rest

***

### kafka_rest_custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration

Default:  "{{ custom_log4j }}"

***

### kafka_rest_custom_java_args

Custom Java Args to add to the Rest Proxy Process

Default:  ""

***

# confluent.ksql

Below are the supported variables for the role confluent.ksql

***

### ksql_custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration

Default:  "{{ custom_log4j }}"

***

### ksql_custom_java_args

Custom Java Args to add to the ksqlDB Process

Default:  ""

***

### ksql_rocksdb_path

Full Path to the RocksDB Data Directory. If set as empty string, cp-ansible will not configure RocksDB

Default:  /tmp/ksqldb

***

# confluent.schema_registry

Below are the supported variables for the role confluent.schema_registry

***

### schema_registry_custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration

Default:  "{{ custom_log4j }}"

***

### schema_registry_custom_java_args

Custom Java Args to add to the Schema Registry Process

Default:  ""

***

# confluent.zookeeper

Below are the supported variables for the role confluent.zookeeper

***

### zookeeper_custom_log4j

Boolean to enable cp-ansible's Custom Log4j Configuration

Default:  "{{ custom_log4j }}"

***

### zookeeper_custom_java_args

Custom Java Args to add to the Zookeeper Process

Default:  ""

***

# confluent.ssl

Below are the supported variables for the role confluent.ssl

***

### ssl_key_algorithm

Key Algorithm used by keytool -genkeypair command when creating Keystores. Only used with self-signed certs

Default:  RSA

***

### ssl_key_size

Key Size used by keytool -genkeypair command when creating Keystores. Only used with self-signed certs

Default:  2048

***

