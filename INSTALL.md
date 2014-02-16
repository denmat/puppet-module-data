Installation:
=============

I needed to install the module-data patches into puppet gems with rvm and 3.x.x. The Rakefile has that in mind. The files are loaded into the correct place for the following gems:

 - hiera-puppet-helper
 - hiera
 - puppet

An example is the following:

```bash
  rake install_into_gemset[ruby-1.8.7-p374@puppet-3.3.1,puppet-3.4.2,hiera-1.3.1,hiera-puppet-helper-1.0.1]
```
