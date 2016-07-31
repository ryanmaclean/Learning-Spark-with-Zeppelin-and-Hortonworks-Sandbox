# Learning Spark with Zeppelin and Hortonworks Sandbox
Learning Spark with the Zeppelin notebook from the Hortonworks Sandbox VM

I've created this repo in order to catalog the differences between the setup I used and the one presented in the Eduonix [Learn Apache Spark from Scratch](https://www.eduonix.com/courses/Software-Development/Learn-Apache-Spark-from-Scratch-for-Beginners) course as I found it much simpler though Zeppelin may not have been in the sandbox at the time of course creation. 

## Getting Started 

### Install a Hypervisor 
You'll need to have either VMware (30 day trial) or Virtualbox environments installed already. If you don't have a preference, I'd suggest Virtualbox, though I've got examples for all 6 permutations regardless. 


#### Apple macOS
On macOS, this can be done via [Homebrew](http://brew.sh/):

```
brew install virtualbox
```

OR

```
brew install vmware-fusion
```

#### Microsoft Windows
On Windows, the excellent [Chocolatey](https://chocolatey.org/) comes to the rescue:

```
choco install virtualbox`
```

OR

```
choco install vmware-workstation
```

#### Ubuntu Linux LTS
On Ubuntu, things are slightly more complicated, but not insurmountable. 

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

This section really should not be needed, but at the time I took the course, the Hortonworks website refused to let me download the sandbox with anything other than Mozilla Firefox. This isn't a very large concern, but I'm hoping to help save you time before you try it in Chrome, then IE, then Safari on your Mac. 

Hortonworks download/survey link: http://hortonworks.com/products/sandbox/

### Start the VM

Once downloaded, you should be able to simply double click either the `vmdk` or `ova` you downloaded for your corresponding hypervisor in order to import it. 

Note that before starting the VM, I'd highly recommend setting your network adapter to `bridged mode` if your network environment allows it. 

Once started, you'll be met with a Hortonworks screen which will give you the IP address of the VM that we will use later on. 

![](vm_initial_screen.PNG)

### Connect to the Sandbox

At this point, you can either click into the VM or connect to it via SSH in order to change a few things. 

Note that in the course, there's a step for downloading Spark - this is no longer needed as the sandbox VM now includes it. 

### Change the SSH Password

In order to login, use the username `root` and the password `hadoop`. 

You'll be asked to change your password immediately: simply type in `hadoop` again, then your new password, and type it once more in order to confirm the new password. 

### Change the Ambari Password

This is an optional step, but highly recommended as Ambari is a fantastic way to manage the VM:

`ambari-admin-password-reset`

Then simply set a new admin password. 

### Open Zeppelin in Your Browser

Now take the IP address you got from the initial VM start screen and paste it into you browser and add `:9995` to the end, like so:

```
http://10.0.0.1:9995
```

Note, if the IP address given to you by the initial sandbox startup screen was 127.0.0.1 (as it was in my case), you can type:

```
ifconfig eth0 | grep 'inet addr:' | cut -d: -f2
```

## Using Zeppelin

This will only be a quick overview, as it's very similar to the `spark-shell` examples, but some attention needs to be given to file uploads as they are different than normal Zeppelin examples. 

### Using Data

The first thing to note is that you can simply run shell commands in Zeppelin using `%sh`. 


#### Downloading

For example, in order to download the first example from the intro:

```
%sh
wget http://www-stat.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data
```

Results in: 

```
--2016-07-31 21:30:17--  http://www-stat.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data
Resolving www-stat.stanford.edu... 171.67.216.22
Connecting to www-stat.stanford.edu|171.67.216.22|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: http://statistics.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data [following]
--2016-07-31 21:30:18--  http://statistics.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data
Resolving statistics.stanford.edu... 171.64.13.30
Connecting to statistics.stanford.edu|171.64.13.30|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://statistics.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data [following]
--2016-07-31 21:30:18--  https://statistics.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data
Connecting to statistics.stanford.edu|171.64.13.30|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: http://statweb.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data [following]
--2016-07-31 21:30:18--  http://statweb.stanford.edu/~tibs/ElemStatLearn/datasets/spam.data
Resolving statweb.stanford.edu... 171.67.24.34
Connecting to statweb.stanford.edu|171.67.24.34|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 698341 (682K)
Saving to: “spam.data”
     0K .......... .......... .......... .......... ..........  7%  798K 1s
    50K .......... .......... .......... .......... .......... 14% 1.56M 1s
   100K .......... .......... .......... .......... .......... 21% 1.61M 0s
   150K .......... .......... .......... .......... .......... 29% 42.2M 0s
   200K .......... .......... .......... .......... .......... 36% 1.57M 0s
   250K .......... .......... .......... .......... .......... 43% 1.65M 0s
   300K .......... .......... .......... .......... .......... 51% 24.8M 0s
   350K .......... .......... .......... .......... .......... 58% 42.5M 0s
   400K .......... .......... .......... .......... .......... 65% 1.71M 0s
   450K .......... .......... .......... .......... .......... 73% 23.2M 0s
   500K .......... .......... .......... .......... .......... 80% 50.3M 0s
   550K .......... .......... .......... .......... .......... 87% 1.70M 0s
   600K .......... .......... .......... .......... .......... 95% 26.6M 0s
   650K .......... .......... .......... .                    100% 51.5M=0.3s
2016-07-31 21:30:19 (2.64 MB/s) - “spam.data” saved [698341/698341]
```
