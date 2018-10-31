---
layout: default
title: "Puppet agent release notes"
---

[Puppet 6.0.2]: /docs/puppet/6.0/release_notes.html#puppet-602

[Facter 3.10.0]: /docs/facter/3.10/release_notes.html#facter-3100
[Facter 3.11.0]: /docs/facter/3.11/release_notes.html#facter-3110
[Facter 3.11.1]: /docs/facter/3.11/release_notes.html#facter-3111
[Facter 3.11.2]: /docs/facter/3.11/release_notes.html#facter-3112
[Facter 3.11.3]: /docs/facter/3.11/release_notes.html#facter-3113
[Facter 3.11.4]: /docs/facter/3.11/release_notes.html#facter-3114


[pxp-agent]: https://github.com/puppetlabs/pxp-agent

This page lists changes to the `puppet-agent` package. For details about changes to components in a `puppet-agent` release, follow the links to those components in the package release's notes.

The `puppet-agent` package's version numbers use the format X.Y.Z, where:

-   X must increase for major backward-incompatible changes
-   Y may increase for backward-compatible new functionality
-   Z may increase for bug fixes

The `puppet-agent` package installs the latest version of Puppet 5.

Also of interest: [About Agent](./about_agent.html) and the [Puppet 6.0.2][] release notes.

## Puppet agent 6.0.3

Released 23 October 2018.

This release contains a new feature.

### New features

- The eyaml executable of the vendored hiera-eyaml gem is now included in the `/opt/puppetlabs/puppet/bin` directory. [PA-2129](https://tickets.puppetlabs.com/browse/PA-2129)

## Puppet agent 6.0.2

Released 4 October 2018

This release addresses a regression bug. See the [Puppet 6.0.2][] release notes for information.

## Puppet agent 6.0.1

Release 2 October 2018

This release contains component updates.

### Component updates

- Resource API was updated to 1.6.0.
- `augeas_core` module was updated to 1.0.2.
- PXP agent was updated to 1.10.1.

## Puppet agent 6.0.0

Released 18 September 2018

This release includes new features, a deprecation, and a bug fix. 

### New features

- Boost was updated to version 1.67 in puppet-agent#master. yaml-cpp was updated to version 0.6.2. ([PA-2055](https://tickets.puppetlabs.com/browse/PA-2055))
- We have updated the version of OpenSSL used in puppet-agent to version 1.1.0h. ([PA-1941](https://tickets.puppetlabs.com/browse/PA-1941))
- The directory structure of Windows package installations has changed. The default installation directory is now `Drive:\Program Files\Puppet Labs\Puppet\puppet`. This directory is now where Facter, pxp-agent, Hiera and Ruby are installed. ([PA-1923](https://tickets.puppetlabs.com/browse/PA-1923))

### Deprecations

- We have removed MCollective as an agent component for Puppet Platform 6, and all other related files. See [Removing MCollective](/pe/2018.1/removing_mcollective.html) in the PE documentation for more information. If you use open source Puppet, we recommend that you migrate MCollective agents and filters using tools like [Bolt](/bolt/latest/bolt.html) and [PuppetDB’s Puppet Query Language](/puppetdb/6.0/index.html).([PA-1918](https://tickets.puppetlabs.com/browse/PA-1918))


### Bug fixes

- We have updated the vendored `semantic_puppet` gem in the `puppet-agent` package to the most recent version, 1.0.2. ([PA-1881](https://tickets.puppetlabs.com/browse/PA-1881))


