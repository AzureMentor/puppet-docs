---
layout: default
built_from_commit: 30034e39d725e0107d5e961eaf5cf0866534282b
title: 'Resource Type: k5login'
canonical: "/puppet/latest/types/k5login.html"
---

> **NOTE:** This page was generated from the Puppet source code on 2018-08-28 06:48:02 -0700

k5login
-----

* [Attributes](#k5login-attributes)
* [Providers](#k5login-providers)

<h3 id="k5login-description">Description</h3>

Manage the `.k5login` file for a user.  Specify the full path to
the `.k5login` file as the name, and an array of principals as the
`principals` attribute.

<h3 id="k5login-attributes">Attributes</h3>

<pre><code>k5login { 'resource title':
  <a href="#k5login-attribute-path">path</a>       =&gt; <em># <strong>(namevar)</strong> The path to the `.k5login` file to manage.  Must </em>
  <a href="#k5login-attribute-ensure">ensure</a>     =&gt; <em># The basic property that the resource should be...</em>
  <a href="#k5login-attribute-mode">mode</a>       =&gt; <em># The desired permissions mode of the `.k5login...</em>
  <a href="#k5login-attribute-principals">principals</a> =&gt; <em># The principals present in the `.k5login` file...</em>
  <a href="#k5login-attribute-provider">provider</a>   =&gt; <em># The specific backend to use for this `k5login...</em>
  <a href="#k5login-attribute-selrange">selrange</a>   =&gt; <em># What the SELinux range component of the context...</em>
  <a href="#k5login-attribute-selrole">selrole</a>    =&gt; <em># What the SELinux role component of the context...</em>
  <a href="#k5login-attribute-seltype">seltype</a>    =&gt; <em># What the SELinux type component of the context...</em>
  <a href="#k5login-attribute-seluser">seluser</a>    =&gt; <em># What the SELinux user component of the context...</em>
  # ...plus any applicable <a href="{{puppet}}/metaparameter.html">metaparameters</a>.
}</code></pre>

<h4 id="k5login-attribute-path">path</h4>

_(**Namevar:** If omitted, this attribute's value defaults to the resource's title.)_

The path to the `.k5login` file to manage.  Must be fully qualified.

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-ensure">ensure</h4>

_(**Property:** This attribute represents concrete state on the target system.)_

The basic property that the resource should be in.

Default: `present`

Allowed values:

* `present`
* `absent`

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-mode">mode</h4>

_(**Property:** This attribute represents concrete state on the target system.)_

The desired permissions mode of the `.k5login` file. Defaults to `644`.

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-principals">principals</h4>

_(**Property:** This attribute represents concrete state on the target system.)_

The principals present in the `.k5login` file. This should be specified as an array.

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-provider">provider</h4>

The specific backend to use for this `k5login`
resource. You will seldom need to specify this --- Puppet will usually
discover the appropriate provider for your platform.

Available providers are:

* [`k5login`](#k5login-provider-k5login)

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-selrange">selrange</h4>

_(**Property:** This attribute represents concrete state on the target system.)_

What the SELinux range component of the context of the file should be.
Any valid SELinux range component is accepted.  For example `s0` or
`SystemHigh`.  If not specified it defaults to the value returned by
matchpathcon for the file, if any exists.  Only valid on systems with
SELinux support enabled and that have support for MCS (Multi-Category
Security).

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-selrole">selrole</h4>

_(**Property:** This attribute represents concrete state on the target system.)_

What the SELinux role component of the context of the file should be.
Any valid SELinux role component is accepted.  For example `role_r`.
If not specified it defaults to the value returned by matchpathcon for
the file, if any exists.  Only valid on systems with SELinux support
enabled.

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-seltype">seltype</h4>

_(**Property:** This attribute represents concrete state on the target system.)_

What the SELinux type component of the context of the file should be.
Any valid SELinux type component is accepted.  For example `tmp_t`.
If not specified it defaults to the value returned by matchpathcon for
the file, if any exists.  Only valid on systems with SELinux support
enabled.

([↑ Back to k5login attributes](#k5login-attributes))

<h4 id="k5login-attribute-seluser">seluser</h4>

_(**Property:** This attribute represents concrete state on the target system.)_

What the SELinux user component of the context of the file should be.
Any valid SELinux user component is accepted.  For example `user_u`.
If not specified it defaults to the value returned by matchpathcon for
the file, if any exists.  Only valid on systems with SELinux support
enabled.

([↑ Back to k5login attributes](#k5login-attributes))


<h3 id="k5login-providers">Providers</h3>

<h4 id="k5login-provider-k5login">k5login</h4>

The k5login provider is the only provider for the k5login
type.




> **NOTE:** This page was generated from the Puppet source code on 2018-08-28 06:48:02 -0700