# Learning Spark with Zeppelin and Hortonworks Sandbox
Learning Spark with the Zeppelin notebook from the Hortonworks Sandbox VM

I've created this repo in order to catalog the differences between the setup I used and the one presented in the Eduonix Spark course as I found it much simpler though Zeppelin may not have been in the sandbox at the time of course creation. 

## Getting Started 

### Install a Hypervisor 
You'll need to have either VMware (30 day trial) or Virtualbox environments installed already. If you don't have a preference, I'd suggest Virtualbox, though I've got examples for all 6 permutations regardless. 

On macOS, this can be done via [Homebrew](http://brew.sh/):

```
brew install virtualbox
```

OR

```
brew install vmware-fusion
```

On Windows, the excellent [Chocolatey](https://chocolatey.org/) comes to the rescue:

```
choco install virtualbox`
```

OR

```
choco install vmware-workstation
```

On Ubuntu, things are slightly more complicated, but not insurmountable: 


Virtualbox:

```
sudo sh -c "echo 'deb http://download.virtualbox.org/virtualbox/debian '$(lsb_release -cs)' contrib non-free' > /etc/apt/sources.list.d/virtualbox.list" && \
wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -O- | sudo apt-key add - && \
sudo apt-get update && sudo apt-get install virtualbox-5.0
```

VMware Workstation:

```
sudo apt-cache search linux-headers-$(uname -r)
sudo apt-get install linux-headers-$(uname -r)
sudo apt-get install build-essential
cd
mkdir vmware
cd vmware
wget https://www.vmware.com/go/tryworkstation-linux-64
chmod +x *.bundle
./*.bundle
```

### Download the Hortonwork Sandbox VM

### Start the VM

### Connect to the Sandbox via SSH

### Change the SSH Password

### Change the Ambari Password

### Open Zeppelin in Your Browser
