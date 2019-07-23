# Base Images 

## Getting Started 

Build all three images with the below command: 
```
packer build packer.json
```

You can also specify which images you'd like to build with the `-only` flag,
using the builder's `"name"` to specify which image to build. 
```
# i.e. only build Ubuntu v16: 
$ packer build -only xenial-amazon-ebs packer.json
```
