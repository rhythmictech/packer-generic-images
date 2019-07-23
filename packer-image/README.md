# Packer Image 
Builds an Ubuntu AMI with Packer installed 

## Getting Started
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
