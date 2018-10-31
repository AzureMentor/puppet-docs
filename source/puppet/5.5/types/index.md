---
layout: default
built_from_commit: 30034e39d725e0107d5e961eaf5cf0866534282b
title: 'Resource Types: Index'
canonical: "/puppet/latest/types/index.html"
---

## List of Resource Types

* [augeas](./augeas.html)
* [computer](./computer.html)
* [cron](./cron.html)
* [exec](./exec.html)
* [file](./file.html)
* [filebucket](./filebucket.html)
* [group](./group.html)
* [host](./host.html)
* [interface](./interface.html)
* [k5login](./k5login.html)
* [macauthorization](./macauthorization.html)
* [mailalias](./mailalias.html)
* [maillist](./maillist.html)
* [mcx](./mcx.html)
* [mount](./mount.html)
* [nagios_command](./nagios_command.html)
* [nagios_contact](./nagios_contact.html)
* [nagios_contactgroup](./nagios_contactgroup.html)
* [nagios_host](./nagios_host.html)
* [nagios_hostdependency](./nagios_hostdependency.html)
* [nagios_hostescalation](./nagios_hostescalation.html)
* [nagios_hostextinfo](./nagios_hostextinfo.html)
* [nagios_hostgroup](./nagios_hostgroup.html)
* [nagios_service](./nagios_service.html)
* [nagios_servicedependency](./nagios_servicedependency.html)
* [nagios_serviceescalation](./nagios_serviceescalation.html)
* [nagios_serviceextinfo](./nagios_serviceextinfo.html)
* [nagios_servicegroup](./nagios_servicegroup.html)
* [nagios_timeperiod](./nagios_timeperiod.html)
* [notify](./notify.html)
* [package](./package.html)
* [resources](./resources.html)
* [router](./router.html)
* [schedule](./schedule.html)
* [scheduled_task](./scheduled_task.html)
* [selboolean](./selboolean.html)
* [selmodule](./selmodule.html)
* [service](./service.html)
* [ssh_authorized_key](./ssh_authorized_key.html)
* [sshkey](./sshkey.html)
* [stage](./stage.html)
* [tidy](./tidy.html)
* [user](./user.html)
* [vlan](./vlan.html)
* [yumrepo](./yumrepo.html)
* [zfs](./zfs.html)
* [zone](./zone.html)
* [zpool](./zpool.html)

## About resource types

### Built-in types and custom types

This is the documentation for the _built-in_ resource types and providers, keyed
to a specific Puppet version. (See sidebar.) Additional resource types can be
distributed in Puppet modules; you can find and install modules by browsing the
[Puppet Forge](http://forge.puppet.com). See each module's documentation for
information on how to use its custom resource types.

### Declaring resources

To manage resources on a target system, you should declare them in Puppet
manifests. For more details, see
[the resources page of the Puppet language reference.](/docs/puppet/latest/lang_resources.html)

You can also browse and manage resources interactively using the
`puppet resource` subcommand; run `puppet resource --help` for more information.

### Namevars and titles

All types have a special attribute called the _namevar_. This is the attribute
used to uniquely identify a resource on the target system.

Each resource has a specific namevar attribute, which is listed on this page in
each resource's reference. If you don't specify a value for the namevar, its
value defaults to the resource's _title_.

**Example of a title as a default namevar:**

```puppet
file { '/etc/passwd':
  owner => 'root',
  group => 'root',
  mode  => '0644',
}
```

In this code, `/etc/passwd` is the _title_ of the file resource.

The file type's namevar is `path`. Because we didn't provide a `path` value in
this example, the value defaults to the title, `/etc/passwd`.

**Example of a namevar:**

```puppet
file { 'passwords':
  path  => '/etc/passwd',
  owner => 'root',
  group => 'root',
  mode  => '0644',
```

This example is functionally similar to the previous example. Its `path`
namevar attribute has an explicitly set value separate from the title, so
its name is still `/etc/passwd`.

Other Puppet code can refer to this resource as `File['/etc/passwd']` to
declare relationships.

### Attributes, parameters, properties

The _attributes_ (sometimes called _parameters_) of a resource determine its
desired state. They either directly modify the system (internally, these are
called "properties") or they affect how the resource behaves (for instance,
adding a search path for `exec` resources or controlling directory recursion
on `file` resources).

### Providers

_Providers_ implement the same resource type on different kinds of systems.
They usually do this by calling out to external commands.

Although Puppet will automatically select an appropriate default provider, you
can override the default with the `provider` attribute. (For example, `package`
resources on Red Hat systems default to the `yum` provider, but you can specify
`provider => gem` to install Ruby libraries with the `gem` command.)

Providers often specify binaries that they require. Fully qualified binary
paths indicate that the binary must exist at that specific path, and
unqualified paths indicate that Puppet will search for the binary using the
shell path.

### Features

_Features_ are abilities that some providers might not support. Generally, a
feature corresponds to some allowed values for a resource attribute.

This is often the case with the `ensure` attribute. In most types, Puppet
doesn't create new resources when omitting `ensure` but still modifies existing
resources to match specifications in the manifest. However, in some types this
isn't always the case, or additional values provide more granular control. For
example, if a `package` provider supports the `purgeable` feature, you can
specify `ensure => purged` to delete configuration files installed by the
package.

Resource types define the set of features they can use, and providers can
declare which features they provide.

----------------

