<!---
Copryight 2016 floragunn GmbH
-->

# Installation

## General

The basic installation procedure is to:

1. Stop Elasticsearch.
2. Install SearchGuard, as explained below.
3. Generate TLS certificates.
4. Configure the certificates in elasticsearch.yml.
5. Restart Elasticsearch.
6. Initialise Search Guard by running sgadmin.

## Ensure that you Java Virtual Machine is supported

* We support only OpenJDK 7/8 or Oracle JVM 7/8.
* There is **no** support for IBM VM or any other vendor than OpenJDK/Oracle JVM

## Get the version of Search Guard that matches Elasticsearch

You need to install the Search Guard version that matches your Elasticsearch Version. For example, a plugin built for ES 5.4.1 will not run on ES 5.4.2 and vice versa.

In order to find the correct Search Guard and Search Guard SSL version for your Elasticsearch installation, please refer to our [version matrix](https://github.com/floragunncom/search-guard/wiki) in the github repository. This matrix will be kept up-to-date with each release.

If you use the enterprise features, please make sure that also the versions of these modules match.

## Installing the plugin(s)

Search Guard can be installed like any other Elasticsearch plugin. **Replace the version number** in the following examples with the version suitable for your Elasticsearch installation.

Make sure to install the plugins with the same user you run Elasticsearch. For example, if you installed Elasticsearch using the official Debian packages, it is executed with user `elasticsearch`.

**Search Guard 5**

For Search Guard 5, you only need to install one plugin, namely Search Guard. The SSL layer is bundled with the main plugin.

Change to the directory of your Elasticsearch installation and type:

```
bin/elasticsearch-plugin install -b com.floragunn:search-guard-5:5.4.2-13
```

After the installation you should see a folder called "search-guard-5" in the plugin directory of your Elasticsearch installation.

**Search Guard 2**

For Search Guard 2, you need to install Search Guard SSL first and after that Search Guard itself. Change to the directory of your Elasticsearch installation and type:

```
bin/plugin install -b com.floragunn/search-guard-ssl/2.4.5.21
bin/plugin install -b com.floragunn/search-guard-2/2.4.5.13
```
After the installation you should see a folder called "search-guard-2" in the plugin directory of your Elasticsearch installation.

### Offline installation

If you are behind a firewall and need to perform an offline installation, follow these steps:

**Search Guard 5**

* Download the [Search Guard 5 version matching your Elasticsearch version](https://github.com/floragunncom/search-guard/wiki) from Maven Central:
  * [All versions of Search Guard 5](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22search-guard-5%22) 
  * Download the **zip file** of the Search Guard plugin
* Change to the directory of your Elasticsearch installation and type:

```
bin/elasticsearch-plugin install -b file:///path/to/search-guard-5-<version>.zip
```
**Search Guard 2**

* Download the Search Guard SSL and Search Guard plugins [version matching your Elasticsearch version](https://github.com/floragunncom/search-guard/wiki) from Maven Central:
  * [All versions of Search Guard 2 SSL](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22search-guard-ssl%22) 
  * [All versions of Search Guard 2](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22search-guard-2%22) 

  * Download the **zip files** of Search Guard plugins
* Change to the directory of your Elasticsearch installation and type:

```
bin/plugin install -b file:///location/of/search-guard-ssl-<version>.zip
bin/plugin install -b file:///location/of/search-guard-2-<version>.zip
```

## Additional permissions dialogue


Since ES 2.2, you will see the following warning message when installating Search Guard and/or Search Guard SSL. For some ES versions, you need to actively confirm it by pressing 'y':

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@     WARNING: plugin requires additional permissions     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
* java.lang.RuntimePermission accessClassInPackage.sun.misc
* java.lang.RuntimePermission getClassLoader
* java.lang.RuntimePermission loadLibrary.*
* java.lang.reflect.ReflectPermission suppressAccessChecks
* java.security.SecurityPermission getProperty.ssl.KeyManagerFactory.algorithm
See http://docs.oracle.com/javase/8/docs/technotes/guides/security/permissions.html
for descriptions of what these permissions allow and the associated risks.
```

## Installing enterprise modules

If you want to use any of the enterprise modules, download the respective jar file and place it in the folder 

* `<ES installation directory>/plugins/search-guard-5`

or

* `<ES installation directory>/plugins/search-guard-2`


Each module lives in its own github repository. You can either download the repository and build the jar files yourself via a simple ```mvn install``` command. Or you can choose to download the jar file(s) (**choose jar file(s) with dependencies**) directly from Maven.

#### LDAP- and Active Directory Authentication/Authorisation:
[All versions on maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22dlic-search-guard-authbackend-ldap%22)

[https://github.com/floragunncom/search-guard-authbackend-ldap](https://github.com/floragunncom/search-guard-authbackend-ldap)

[LDAP and Active Directory documentation](ldap.md)

#### Kerberos/SPNEGO Authentication/Authorisation:
[All versions on maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22dlic-search-guard-auth-http-kerberos%22)

[https://github.com/floragunncom/search-guard-auth-http-kerberos](https://github.com/floragunncom/search-guard-auth-http-kerberos)

[Kerberos/SPNEGO documentation](kerberos.md)

#### JWT Authentication/Authorisation:
[All versions on maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22dlic-search-guard-auth-http-jwt%22)

[https://github.com/floragunncom/search-guard-authbackend-jwt](https://github.com/floragunncom/search-guard-authbackend-jwt)

[JSON Web token documentation](jwt.md)

#### Document- and field level security:
[All versions on maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22dlic-search-guard-module-dlsfls%22)

[https://github.com/floragunncom/search-guard-module-dlsfls](https://github.com/floragunncom/search-guard-module-dlsfls)

[Document and field level security documentation](dlsfls.md)

#### Audit logging:
[All versions on maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22dlic-search-guard-module-auditlog%22)

[https://github.com/floragunncom/search-guard-module-auditlog](https://github.com/floragunncom/search-guard-module-auditlog)

[Audit Logging documentation](auditlogging.md)

#### REST management API:
[All versions on maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.floragunn%22%20AND%20a%3A%22dlic-search-guard-rest-api%22)

[https://github.com/floragunncom/search-guard-rest-api](https://github.com/floragunncom/search-guard-rest-api)

[REST management API documentation](managementapi.md)

#### Kibana multi tenancy module:
[All versions on maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22dlic-search-guard-module-kibana-multitenancy%22)

[https://github.com/floragunncom/search-guard-module-kibana-multitenancy](https://github.com/floragunncom/search-guard-module-kibana-multitenancy)

[Kibana Multitenancy documentation](multitenancy.md)

Most of these modules require additional configuration settings. Please see the respective sections of this document for further information.

## Expert settings

**WARNING: Only use the following instructions if you know what you are doing. If you set wrong values this could be a security risk or make Search Guard stop working! In most cases, you do not need to change the default settings.**

### Search Guard index name

Search Guard stores all configuration information in a specially secured index. By default, this index is named `searchguard`. You can change this index name with the following configuration key:

```
searchguard.config_index_name: searchguard
```

### Server certificate OID

All certificates used by the nodes on transport level need to have the `oid` field set to a specific value. By default, this is `1.2.3.4.5.5`.

This oid value is checked by Search Guard to identify if an incoming request comes from a trusted node in the cluster or not. In the former case, all actions are allowed, in the latter case, privilege checks apply. Plus, the oid is also checked whenever a node wants to join the cluster. This prohibits a malicious attacker from joinng the cluster by using a client certificate.

You can change the oid value with this confguration key:

```
searchguard.cert.oid: '1.2.3.4.5.5'
```

For other ways to identify nodes, please check the chapter on [TLS node certificates](tls_node_certificates.md).

## Compatibility


### Compatibility with other plugins

If you have other plugins like kopf installed, please check the compatibility with Search Guard.

As a rule of thumb, if a plugin is compatible with Shield, it is also compatible with Search Guard. Specifically:

If the plugin talks to Elasticsearch using REST and you have REST TLS enabled, the plugin must also support TLS.

If the plugin talks to Elasticsearch on the transport layer, you need to be able to add the Search Guard SSL plugin and its configuration settings to the transport client. You can read more about using transport clients with a Search Guard secured cluster [in this blog post](https://floragunn.com/searchguard-elasicsearch-transport-clients/).

#### Compatible plugins and tools

The following plugins and tools have been tested for compatibility with Search Guard:

* Kibana (with the Search Guard Kibana plugin installed)
* Logstash
* Beats
* Curator
* [Kibi](https://siren.solutions/kibi/)
* [syslog-ng](https://syslog-ng.org/) 
* Kopf / [Cerebro](https://github.com/lmenezes/cerebro)
* [Grafana](https://grafana.com/)
* ES-Hadoop / Spark
* [Elastalert](https://github.com/Yelp/elastalert)

#### Incompatible plugins and tools

* [Graylog](https://www.graylog.org/)
* [JDBC Importer](https://github.com/jprante/elasticsearch-jdbc)
