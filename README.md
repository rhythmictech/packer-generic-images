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


