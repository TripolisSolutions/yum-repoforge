yum-repoforge Cookbook
============

The yum-repoforge cookbook takes over management of the default
repositoryids used by repoforge. It allows attribute manipulation of
`rpmforge`, `rpmforge-extras`, and `rpmforge-testing`

Requirements
------------
* Chef 11 or higher
* yum cookbook version 3.0.0 or higher

Attributes
----------
The following attributes are set by default

``` ruby
default['yum']['rpmforge']['repositoryid'] = 'rpmforge'
default['yum']['rpmforge']['description'] = 'RHEL $releasever - RPMforge.net - dag'
default['yum']['rpmforge']['mirrorlist'] = 'http://mirrorlist.repoforge.org/el6/mirrors-rpmforge'
default['yum']['rpmforge']['enabled'] = true
default['yum']['rpmforge']['gpgcheck'] = true
default['yum']['rpmforge']['gpgkey'] = 'http://apt.sw.be/RPM-GPG-KEY.dag.txt'
```

``` ruby
default['yum']['rpmforge-extras']['repositoryid'] = 'rpmforge'
default['yum']['rpmforge-extras']['description'] = 'RHEL $releasever - RPMforge.net - extras'
default['yum']['rpmforge-extras']['mirrorlist'] = 'http://mirrorlist.repoforge.org/el6/mirrors-rpmforge-extras'
default['yum']['rpmforge-extras']['enabled'] = true
default['yum']['rpmforge-extras']['gpgcheck'] = true
default['yum']['rpmforge-extras']['gpgkey'] = 'http://apt.sw.be/RPM-GPG-KEY.dag.txt'
```

``` ruby
default['yum']['rpmforge-testing']['repositoryid'] = 'rpmforge-testing'
default['yum']['rpmforge-testing']['description'] = 'RHEL $releasever - RPMforge.net - testing'
default['yum']['rpmforge-testing']['mirrorlist'] = 'http://mirrorlist.repoforge.org/el6/mirrors-rpmforge-testing'
default['yum']['rpmforge-testing']['enabled'] = true
default['yum']['rpmforge-testing']['gpgcheck'] = true
default['yum']['rpmforge-testing']['gpgkey'] = 'http://apt.sw.be/RPM-GPG-KEY.dag.txt'
```

Recipes
-------
* default - Walks through node attributes and feeds a yum_resource
  parameters. The following is an example a resource generated by the
  recipe during compilation.

```ruby
  yum_repository 'rpmforge' do
    mirrorlist 'http://mirrorlist.repoforge.org/el6/mirrors-rpmforge'
    description 'RHEL $releasever - RPMforge.net - dag'
    enabled true
    gpgcheck true
    gpgkey 'http://apt.sw.be/RPM-GPG-KEY.dag.txt'
  end
```

Usage Example
-------------
To disable the CentOS Extras repository through a Role or Environment definition

```
default_attributes(
  :yum => {
    :rpmforge => {
      :enabled => {
        false
       }
     }
   }
 )
```

To enable the rpmforge repository with a wrapper cookbook, place
the following in a recipe:

```
node.default['yum']['rpmforge']['enabled'] = true

include_recipe 'yum-repoforge'
```

More Examples
-------------
Point the base and updates repositories at an internally hosted server.

```
node.default['yum']['rpmforge']['enabled'] = true
node.default['yum']['rpmforge']['mirrorlist'] = nil
node.default['yum']['rpmforge']['baseurl'] = 'https://internal.example.com/centos/6/os/x86_64'
node.default['yum']['rpmforge']['sslverify'] = false
include_recipe 'yum-repoforge'
```

License & Authors
-----------------
- Author:: Sean OMeara (<someara@opscode.com>)

```text
Copyright:: 2011-2013 Opscode, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
