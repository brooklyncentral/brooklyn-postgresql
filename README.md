# PostgreSQL

PostgreSQL is a powerful, open source object-relational database system. It has more than 15 years of active development
and a proven architecture that has earned it a strong reputation for reliability, data integrity, and correctness.
It runs on all major operating systems, including Linux, UNIX (AIX, BSD, HP-UX, SGI IRIX, macOS, Solaris, Tru64),
and Windows. It is fully ACID compliant, has full support for foreign keys, joins, views, triggers, and stored procedures
(in multiple languages). It includes most SQL:2008 data types, including INTEGER, NUMERIC, BOOLEAN, CHAR, VARCHAR, DATE,
INTERVAL, and TIMESTAMP. It also supports storage of binary large objects, including pictures, sounds, or video.
It has native programming interfaces for C/C++, Java, .Net, Perl, Python, Ruby, Tcl, ODBC, among others.

## Basic Config

The PostgreSQL blueprint is set up to provide two entities by default:
- one basic PostgreSQL node
- one scalable hot standby HA cluster

which are configurable via the following config keys:

| Config Key                             | Description                                                           | Default         |
|----------------------------------------|-----------------------------------------------------------------------|-----------------|
| postgresql.initial.command             | Initial command to execute after PostgreSQL has been installed        |                 |
| postgresql.config.admin.username       | PostgreSQL username for the admin user                                | admin           |
| postgresql.config.admin.password       | PostgreSQL password for the admin user                                | Pa55w0rd        |
| postgresql.config.maxConnections       | Maximum number of simultaneous connections to the PostgreSQL database |                 |
| postgresql.config.http.port            | Port that PostgreSQL will listen for incoming connections             | 5432            |
| postgresql.config.replication.username | PostgreSQL username for the replication user                          | repuser         |
| postgresql.config.replication.password | PostgreSQL password for the replication user                          | repuserPa55w0rd |

## Usage

To use a PostgreSQL node on an Apache brooklyn entity, include the `postgresql-node` entity:

```yaml
  - type: postgresql-node
    id: postgresql 
```

For a fully hot standby HA cluster, include the `postgresql-ha` entity:

```yaml
  - type: postgresql-ha
    id: postgresql-ha
    brooklyn.config:
      cluster.initial.size: 3
```

## Future development

The blueprint is currently fully functional but the following things probably require further input:

- The failover procedure for the HA cluster is not implemented.
- More configuration should be pulled out into `brooklyn.parameters` for the PostgreSQL Node.
