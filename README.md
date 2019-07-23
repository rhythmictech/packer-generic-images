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

Build the AMI
```
packer build packer.json
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

