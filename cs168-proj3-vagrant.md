# Vagrant-based SSH+shared folder setup

I'm posting this because it took me some time to set up SSH and shared folder access, and I wanted to share how I finally did it in case it can help anyone else. While I don't think the actions here are particular destructive, please _follow only at your own risk and if you feel fairly confident with doing these kinds of things_. (Instructors, feel free to delete this post if you feel it's not appropriate for here.)

I kept getting SSH errors when following the instructions in the specs. I ended up using [Vagrant](http://vagrantup.com/), a command-line tool that, among other things, can be used to configure VirtualBox VMs. Vagrant is really nice because I can put all my VM settings into [a config file (`Vagrantfile`)](http://notepad.cc/share/itO7K8M8M0) and Vagrant can set everything up.

Here's what my setup looks like: [proj3_w_vagrant.tar](https://d1b10bmlvqabco.cloudfront.net/attach/hz9lw7aquvu2r9/h6fbvopj5tg5xp/i24h1qmyu2jp/proj3_w_vagrant.tar)

This file untars into a `proj3` directory, ~~which contains the original project files~~ [Note: The files are from a previous semester; make sure you update this folder with your project files from this semester], plus two things: a `Vagrantfile` and a `bin/setup-vagrant` script. When set up using the instructions below, your VM will be modified in the following ways:

*   You can SSH into the machine with `ssh cs168@172.16.122.2` or `vagrant ssh`.
*   The files in `proj3` in the VM can be accessed/edited in the `proj3` directory on your host computer, and vice versa.

Setup:

1.  [Download](http://inst.eecs.berkeley.edu/~cs168/fa14/class.html) and import the VM into VirtualBox if you haven't already done so. If you already made changes to the files in your VM, back up those changes to somewhere outside of the `proj3` folder. Probably the best way to do this is to just rename `proj3` to something else.
2.  Install [Vagrant](http://vagrantup.com/). On Mac: `brew install Caskroom/cask/vagrant`
3.  Download and untar the tar file somewhere, and `cd` into the folder.
4.  Type `VBoxManage list vms` and copy your VM UUID (the thing in braces, but excluding the braces) of your `cs168proj3` VM.
5.  Type `bin/setup-vagrant <paste UUID here>`. This will apply the proper SSH and shared folder settings to the VM and start it up.
6.  If you had changes you backed up in step 1, you can restore them now.

At this point your VM is set up and you no longer have to use Vagrant (you can go back to starting/stopping the machine with VirtualBox). But you can continue to use Vagrant, with these added benefits:

*   ~~the VM can run in the background ("headless mode"), using less CPU~~  
    This is no longer true; the VirtualBox GUI lets you start VMs in headless mode now
*   `vagrant ssh` won't ask you for a password
*   If you move your `proj3` directory, your shared folder setup will break, but it will be fixed the next time you `vagrant up`

Important Vagrant commands (make sure you're `cd`'d into directory with the `Vagrantfile`):

*   `vagrant up` to start up the VM
*   `vagrant ssh` to SSH into the VM
*   `vagrant halt` to shut down the VM

Hope this is helpful.

---

Original post:

![Original post](https://cloud.githubusercontent.com/assets/1570168/10903318/4d3017d6-81bd-11e5-952f-898870f2abb1.png)