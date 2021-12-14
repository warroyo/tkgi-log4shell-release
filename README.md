# TKGI Log4shell

this implements the fix for  `CVE-2021-44228` in a bosh release so that bosh ressurector does not need to be turned off. the fix was taken from [here](https://community.pivotal.io/s/article/Workaround-instructions-to-address-CVE-2021-44228-in-Tanzu-Kubernetes-Grid-Integrated?language=en_US)



## Usage 

install on your tkgi bosh director, sit back and watch.

### Install

1. Open a shell prompt on a BOSH CLI with access to your PKS bosh director, such as Ops Manager.
2. Export your BOSH credentials to the enviornment.  These can be accessed via the Ops Manager GUI -> BOSH Director Tile -> Credentials Tab -> Bosh Commandline Credentials.

e.g.
```
export BOSH_CLIENT=ops_manager BOSH_CLIENT_SECRET=fakesecret BOSH_CA_CERT=/var/tempest/workspaces/default/root_ca_certificate  BOSH_ENVIRONMENT=10.0.0.10
```
3. Copy or clone this repository onto this BOSH CLI workstation and create+upload the BOSH release to the director

```
git clone https://github.com/warroyo/tkgi-log4shell-release && cd tkgi-log4shell-release
bosh create-release --force
bosh upload-release ./dev_releases/tkgi-log4shell/tkgi-log4shell-0+dev.1.yml

```
4. Configure the addon from this repo
```

bosh -n update-config --name=tkgi-log4shell --type=runtime ./addon.yml
```
