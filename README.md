# packer-generic-images
Generic Packer images starting with AWS

## About 
Generic CIS-compliant base AMIs in three delicious flavours:
- Ubuntu Bionic Beaver (v18)
- Ubuntu Xenial (v16)
- Amazon Linux 2 

## Getting Started 
1. Install the [prerequisites](#prerequisites) from their website or using your package manager
1. Add the approprate [user variables](#adding-user-variables) for your circumstance
1. [Build the AMI](#build-the-ami) in your AWS account with `packer`

### Prerequisites 
- [packer](https://packer.io/)
- [ansible](https://www.ansible.com/)
- [aws account](https://aws.amazon.com/)

### Adding user variables 
There are multiple ways of [authentication with the amazon builder](https://www.packer.io/docs/builders/amazon.html), 
any of which will work. 

### Build the AMI 
Running the below command should produce like output (squashed for readability)
```
$ packer build packer.json
amazon-ebs output will be in this color.

==> amazon-ebs: Prevalidating AMI Name: packer_ubuntu_bionic_builder_1563903230
    amazon-ebs: Found Image ID: ami-026c8acd92718196b
==> amazon-ebs: Creating temporary keypair: packer_5d3744ff-bb38-668c-6314-ba596b50b246
==> amazon-ebs: Creating temporary security group for this instance: packer_5d374501-704d-e9ab-ce0e-d61e85d7a198
==> amazon-ebs: Authorizing access to port 22 from [0.0.0.0/0] in the temporary security groups...
==> amazon-ebs: Launching a source AWS instance...

...

==> Builds finished. The artifacts of successful builds are:
--> amazon-ebs: AMIs were created:
us-east-1: ami-01308454f3364cf58


```

The resulting ami (`ami-01308454f3364cf58` in this case) will be available in your aws account. 
The default region set in this packer file is `us-east-1`.


You can also specify which images you'd like to build with the `-only` flag,
using the builder's `"name"` to specify which image to build. 
```
# i.e. only build Ubuntu v16: 
$ packer build -only xenial-amazon-ebs packer.json
```


## Debugging known issues :heart:

Here are some common errors and their work-arounds 

### `fatal: [default]: FAILED! => {"changed": false, "msg": "yum lockfile is held by another process"}`
Occasionally ansible will get a little antsy and try to run one command before another has released it's hold on `yum`. 

The work around is to
- Just run it again (sometimes this will work)
- Run it with the `-debug` flag. This will give the process time to release `yum`

### `too many authentication failure. Disconnected`
When Ansible connects to the instance Packer is using to build your AMI it uses SSH. 
By default SSH tries offer all the SSH keys it is aware of. 
The host will only accept so many failures untill it gets fed up and disallows your connection. 
Read more about [the specific issue with packer](https://github.com/hashicorp/packer/issues/5065) 
or the [more general issue with SSH](https://superuser.com/questions/187779/too-many-authentication-failures-for-username).

The work-around is to tell packer to tell ansible to only use the specified keys with an environmental variable. 
You can run the below command: 
```
ANSIBLE_SSH_ARGS="-o IdentitiesOnly=yes" packer build packer.json
```

