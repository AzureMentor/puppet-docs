---
layout: default
title: "Command line usage"
---

[priority_lookup]: ./lookup_types.html#priority-default
[hash_lookup]: ./lookup_types.html#hash-merge
[array_lookup]: ./lookup_types.html#array-merge

{% partial ./_hiera_deprecation.md %}
>
> The Hiera 3 command-line interface is deprecated and **does not work** with Hiera 5. Use the `puppet lookup` command-line interface instead, because it works with Hiera 3, 4, and 5.

Hiera provides a command line tool that's useful for verifying that your hierarchy is constructed correctly and that your data sources are returning the values you expect. You'll typically run the Hiera command line tool on a Puppet master, making up the facts agents would normally provide the Puppet master using a variety of [fact sources](#fact-sources).

> **Note:** Sometimes it's more convenient to use `puppet apply -e "notice(hiera('<KEY>'))"` instead. Running a tiny manifest like this will make all of Puppet's facts available for interpolation, and you can use external facts to override any fact values you need.

## Invocation

The simplest Hiera command takes a single argument --- the key to look up --- and will look up the key's value using the static [data sources](./data_sources.html) in the [hierarchy](./hierarchy.html).

```
$ hiera ntp_server
```

A more standard invocation will provide a set of variables for Hiera to use, so that it can also use its dynamic [data sources](./data_sources.html):

```
$ hiera ntp_server --yaml web01.example.com.yaml
```

## Configuration file location

The Hiera command line tool looks for its configuration in `/etc/puppetlabs/puppet/hiera.yaml`. You can use the `--config` argument to specify a different configuration file. See the documentation on Hiera's [configuration file](./configuring.html#location) for details about this file.

### Order of arguments

Hiera is sensitive to the position of its command-line arguments:

-   The first value is always the key to look up.
-   The first argument after the key that does not include an equals sign (`=`) becomes the default value, which Hiera will return if no key is found. Without a default value and in the absence of a matching key from the hierarchy, Hiera returns `nil`.
-   Remaining arguments should be `variable=value` pairs.
-   **Options** may be placed anywhere.

### Options

Hiera accepts the following command line options:

Argument                              | Use
--------------------------------------|----------------------------------------------------
`-V`, `--version`                     | Version information
`-c`, `--config FILE`                 | Specify an alternate configuration file location
`-d`, `--debug`                       | Show debugging information
`-a`, `--array`                       | Return all values as a flattened array of unique values
`-h`, `--hash`                        | Return all hash values as a merged hash
`-j`, `--json FILE`                   | JSON file to load scope from
`-y`, `--yaml FILE`                   | YAML file to load scope from
`-m`, `--mcollective IDENTITY`        | Use facts from a node (via mcollective) as scope

## Fact sources

When used from Puppet, Hiera automatically receives all of the facts it needs. On the command line, you'll need to manually pass it those facts.

You'll typically run the Hiera command line tool on your Puppet master node, where it will expect the facts to be either:

-   Included on the command line as variables (such as `::operatingsystem=Debian`)
-   Given as a [YAML or JSON scope file](#json-and-yaml-scopes)
-   Retrieved on the fly from [MCollective](#mcollective) data

Descriptions of these choices are below.

### Command line variables

Hiera accepts facts from the command line in the form of `variable=value` pairs, such as `hiera ntp_server ::osfamily=Debian clientcert="web01.example.com"`. Variables on the command line must be specified in a way that matches how they appear in `hiera.yaml`, including the leading `::` for facts and other top-scope variables. Variable values must be strings and must be quoted if they contain spaces.

This is useful if the values you're testing only rely on a few facts. It can become unwieldy if your hierarchy is large or you need to test values for many nodes at once. In these cases, you should use one of the other options below.

### JSON and YAML scopes

Rather than passing a list of variables to Hiera as command line arguments, you can use JSON and YAML files. You can construct these files yourself, or use a YAML file retrieved from Puppet's cache or generated with `facter --yaml`.

Given this command using command-line variable assignments:

```
$ hiera ntp_server osfamily=Debian timezone=CST
```

> **Note:** For Puppet, [facts are top-scope variables](/puppet/latest/reference/lang_variables.html#facts-and-built-in-variables), so their [fully-qualified](/puppet/latest/reference/lang_scope.html#accessing-out-of-scope-variables) form is `$::fact_name`. When called from within Puppet, Hiera will correctly interpolate `%{::fact_name}`. However, Facter's command-line output doesn't follow this convention --- top-level facts are simply called `fact_name`. That means you'll run into trouble in this section if you have `%{::fact_name}` in your hierarchy.

The following YAML and JSON examples provide equivalent results:

#### Example YAML scope

`$ hiera ntp_server -y facts.yaml`

``` yaml
# facts.yaml
---
"::osfamily": Debian
"::timezone": CST
```

#### Example JSON scope

`$ hiera ntp_server -j facts.json`

``` javascript
// facts.json
{
  "::osfamily" : "Debian",
  "::timezone" : "CST"
}
```

### MCollective

> **Deprecation Note:** As of Puppet agent 5.5.4, MCollective is deprecated and will be removed in a future version of Puppet agent. If you use MCollective with Puppet Enterprise, consider [moving from MCollective to Puppet orchestrator](/docs/pe/2018.1/migrating_from_mcollective_to_orchestrator.html). If you use MCollective with open source Puppet, consider migrating MCollective agents and filters using tools like [Bolt](/docs/bolt/) and PuppetDB's [Puppet Query Language](/docs/puppetdb/latest/api/query/tutorial-pql.html).

If you're using Hiera from a user account that is allowed to issue MCollective commands, you can ask any node running MCollective to send you its facts. Hiera will then use those facts to drive the lookup.

To do this, use the `-m` or `--mcollective` flag and give it the name of an MCollective node as an argument:

```
$ hiera ntp_server -m balancer01.example.com
```

Note that you must be running the Hiera command from a user account that is authorized and configured to send MCollective commands, and is also able to read the Hiera configuration and data files.

## Lookup types

By default, the Hiera command line tool will use a [priority lookup][priority_lookup], which returns a single value --- the first value found in the hierarchy. There are two other lookup types available: array merge and hash merge.

### Array merge

An array merge lookup assembles a value by merging every value it finds in the hierarchy into a flattened array of unique values. [See "Array Merge Lookup"][array_lookup] for more details.

Use the `--array` option to do an array merge lookup.

If any of the values found in the data sources are hashes, the `--array` option will cause Hiera to return an error.

### Hash

A hash merge lookup assembles a value by merging the top-level keys of each hash it finds in the hierarchy into a single hash. [See "Hash Merge Lookup"][hash_lookup] for more details.

Use the `--hash` option to do a hash merge lookup.

If any of the values found in the data sources are strings or arrays, the `--hash` option will cause Hiera to return an error.
