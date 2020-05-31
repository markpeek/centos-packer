# Sample packer templates for CentOS7

## Prerequisites
- Install packer from [here](https://www.packer.io/downloads)
- Install govc from [here](https://github.com/vmware/govmomi/releases)


### Check versions
```
$ packer --version
1.5.6
$ govc version
govc 0.22.1
```

### Setup govc credentials in environment
```
# Set govc variables in your environment to be lazy with commandline args (edit these with your credentials)

export GOVC_URL="vcenter.example.com"
export GOVC_USERNAME='administrator@vsphere.local'
export GOVC_PASSWORD='vmware'
export GOVC_INSECURE=1
export GOVC_DATACENTER="datacenter"
export GOVC_DATASTORE="Datastore"
export GOVC_NETWORK="VM Network"
export GOVC_FOLDER=""
export GOVC_RESOURCE_POOL=""
```

### Download ISO from the internet and upload to vcenter
```
# Download a minimal ISO file
curl -O http://centos.s.uw.edu/centos/7.8.2003/isos/x86_64/CentOS-7-x86_64-Minimal-2003.iso

# Now upload using govc to make it faster to boot packer
govc datastore.upload CentOS-7-x86_64-Minimal-2003.iso /isos/CentOS-7-x86_64-Minimal-2003.iso

```

### Run packer - suggest rena
```
cp vars.json local.json
# edit local.json with credentials

packer build -var-file=local.json centos.json
```


### Export template to OVF
```
govc export.ovf -vm centos7 centos7.ovf
```