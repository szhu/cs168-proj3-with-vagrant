cs168-proj3-with-vagrant
========================

Are you working on CS 168 Project 3 and would rather edit files on your host computer rather than inside your VM? This thing can help you with that, by using Vagrant to set up Virtualbox shared folders.

![](https://cloud.githubusercontent.com/assets/1570168/11029867/cef940b0-867e-11e5-8a19-30ec04718098.gif)


Setup
-----

1.  Some prerequisites before we begin (in the host computer):

    1.  Download this repo, and `cd` into it.
    2.  Make sure [Vagrant](<https://www.vagrantup.com/>) is installed.  
        On Mac: `brew install Caskroom/cask/vagrant`

2.  In your cs168proj3 VM:

    1.  Make sure it is running.
    2.  `mv public public-bak`  
        ![](https://cloud.githubusercontent.com/assets/1570168/11029544/8e5abce8-867c-11e5-9b6e-3141bc44ca0a.gif)
    3.  Turn it off.

3.  In your host computer:

    1.  `VBoxManage list vms`
    2.  You should see the following line, with the `x`'s being variable:  
        `"cs168proj3" {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}`
    3.  Copy the `x`-string (this is your VM's UUID)
    4.  `bin/setup-vagrant xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`  
        (Replacing the `x`-string with actual UUID from above)

    ![](https://cloud.githubusercontent.com/assets/1570168/11030016/06d2b10a-8680-11e5-87f8-36f5a909f45f.gif)

That's it!


Usage
-----

Once you have completed setup, you do not have to use Vagrant anymore. You can `ssh cs168@172.16.122.2` into the VM, just as before.

However, if continue to use Vagrant, you get the following benefits:
-   The VM by default runs in the background ("headless mode"), using less CPU. If you need to use the GUI (i.e., to run Wireshark), open VirtualBox and click "Show" for the VM.
-   `vagrant ssh` won't ask you for a password.
-   If you move your `proj3` directory in your host, your shared folder setup will break and the files will become inaccessible inside the VM. This will be fixed the next time you `vagrant up`.

Vagrant command reference (make sure you're `cd`'d into directory with the `Vagrantfile`):
-   `vagrant up` to start up the VM
-   `vagrant ssh` to SSH into the VM
-   `vagrant halt` to shut down the VM. Add `-f` to force shutdown.
-   `vagrant reload` to restart the VM. Add `-f` to force shutdown.


Deets
-----

Here's what the setup process does:
-   Tells Vagrant which VirtualBox VM to use with this folder.
-   Tells VirtualBox to take a snapshot (backup) of the VM in case anything goes
    wrong.
-   Sets up a VirtualBox shared folder linking this directory with
    `/home/cs168/public` in the VM.
-   Moves files from `/home/cs168/public-bak` into `/home/cs168/public`. Because
    `/home/cs168/public` is now a shared folder, this actually moves the files
    into the host computer, although they are visible from the VM too.

More
----

Something not working? Please open an issue! Include screenshots please.

Created by (@szhu) for CS 168 Fall 2014. [Here's the original
post.](<https://cloud.githubusercontent.com/assets/1570168/10903318/4d3017d6-81bd-11e5-952f-898870f2abb1.png>)
