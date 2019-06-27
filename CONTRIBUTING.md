# Contributing
## Dependencies
* Packer
* Ansible

## Updating build targets
* Some reasons you may want to update the build targets:
  * Add additional build target
  * Change naming scheme

* We're using amazon-ebs builder, which is documented [here](https://www.packer.io/docs/builders/amazon-ebs.html).  
* Additional build targets can be added to the `builders` list.

## Updating provisioners
* Packer provisioners are documented [here](https://www.packer.io/docs/provisioners/index.html)
* The shell provisioner isn't ideal, but it's there if you need it. Generally the Ansible provisioner is preferred.
* It's ideal to use provisioners that are the same for both supported versions of Ubuntu, but if necessary you can use the `only` argument to target the specific builder(s) the provisioner applies to.
