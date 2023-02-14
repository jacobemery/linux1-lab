# Managing Linux Services
## Follow these steps to learn the basics of managing services in the Linux terminal.
If you need to learn (or refresh your memory) about the basics of navigating the Linux terminal first, return to [step 4](./4_navigate.md).
* One of the many uses for a Linux server is running services.
* With Linux on IBM zSystems, these services are highly-available at the hardware level. Always ready for what you throw at them.
* That's right! This whole time you've been running Linux on IBM zSystems, and you would've barely known it.
* Don't believe me? Run the `unamme` (short for 'Unix name') command, with the `-i` option to see the hardware platform:
```
uname -i
```
* As you can see, Linux is running on `s390x` the architecture of IBM zSystems. Pretty cool, eh? It's the same as Linux on any other hardware.

## Installing Packages
* The beauty of this server is that it can become anything we want it to be!
* One fun thing it can become is a web server. Just like any website you would go to on the world-wide-web, this server can expose files for other people all over the world to view.
* Let's go through the steps together.
* First, we need to install some software - in this case we need `httpd`, which stands for Hyper-Text Transfer Protocol daemon. This http is the same one that you see at the beginning of website URLs (Uniform Resource Locators). More than likely it will have an -s at the end too for 'secure', like https://www.ibm.com.
* Let's install the `httpd` package using the `dnf` (short for 'dandified yum', not worth explaining) command:
```
dnf install httpd
```
* Uh oh! Looks like we got a message that tells us we have to use administrative privileges to do that.
* To manage services, a lot of the time you have to be a user with administrative privileges. Luckily, `linux1` is already one such user. 
* Let's test out your super powers. Run the same command but with `sudo` (short for 'super-user do') to run it with elevated privileges.
```
sudo dnf install httpd
```
* You'll then see a summary of the packages that will be installed, and be prompted to confirm or deny their installation:
```
Updating Subscription Management repositories.
.
.
.
Total download size: 2.0 M
Installed size: 5.6 M
Is this ok [y/N]: 
```
* Type `y` and then hit the Enter key to install httpd and the packages it depends on.
```
Downloading Packages:
.
.
.
Complete!
```
* You now have the software installed to allow this server to become a web server!

## Checking Status
* The 'd' at the end of httpd refers to the 'daemon' (process) that keeps the web server up and running.
* Let's see all the processes that are currently running on your server by running the `top` (for the 'top' processes consuming CPU) command:
```
top
```
* There's probably not a lot running, so you're system's resources are not being used up.
* Check out the information on this screen, what helpful information do you see?
* Press `q` to quit out of this screen when you're finished.
* Even though we've installed the software for httpd, we have not yet started its process.
* Use the `systemctl` command to check on the status of httpd:
```
sudo systemctl status httpd
```
* Press `q` to quit out of this screen, just like with `top`.
* <b>Pro Tip!</b> If you forget to type `sudo` before your command and hit Enter and it yells at you, just yell right back at it with the following to re-run the previous command with super-user privileges:
```
sudo !!
```
* So it appears that httpd is inactive, according to systemctl (short for 'system control').
## Starting and Enabling Services
* To start the httpd service, again use the `systemctl` command.
```
sudo systemctl start httpd
```
* And make sure it worked by checking its status again.
* <b>Pro Tip!</b> Use the `up arrow key` to recall previous commands. Scroll through them with the up and down arrow keys and hit Enter when you find the right one.
* So httpd should now be started, according to systemctl.
* One thing before we move on, when services are started, they do not start back up after a reboot unless they are also `enabled`.
* To enable a service, again use systemctl.
* But before we do that. It's getting old use `sudo` every time isn't it? 
* In a production server, it is best practice to use sudo every time.
* But this is a sandbox server, so we can be a little more carefree, and maybe learn some tough lessons along the way...
* Become the `root` user by executing the following command:
```
sudo -i
```
* `WARNING`: Becoming the `root` user is very dangerous for the integrity and security of the server because they have access to all commands. Tread carefully.
* You'll notice that your command prompt has changed from a `$`, which indicates you are a regular user, to a `#`, which indicates you are the root user:
```
[root@test1234 ~]#
```
* Sometimes people will use this as an indicator of the privilege level needed to run a given command.
* The root user also has a different home `~` directory than regular users. Try running the `pwd` command to see where the root user's home is.
```
pwd
```
* With your new powers, you can now run the systemctl command without `sudo`:
```
systemctl enable httpd
```
* If you again recall the systemctl status command with the up arrow key, you should now see that httpd is active AND enabled:
```
httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Sat 2023-02-11 21:36:18 EST; 9min ago
```
## Firewall
* Now that you have started your web server, you would think your website would be ready to be visited in a web browser. But hold your horses, there's one more step left.
* Before we can visit the site, we need to tell the server to allow http traffic through the firewall.
* The service `firewalld` helps us easily manage firewall rules.
* Let's get the `firewalld` service started <i>and</i> enabled. We can achieve this with one command, like this:
```
systemctl enable firewalld --now
```
* The service firewalld should now be started <i>and</i> enabled on your system. You can double-check it with systemctl status.
* Now that we have firewalld running, we can easily allow http traffic (default port 80).
* To do this we'll need to use the `firewall-cmd` command:
```
firewall-cmd --zone=public --add-port=80/tcp --permanent
```
* Reload the firewall to make this change go into effect:
```
firewall-cmd --reload
```
* Ok now you should be able to visit your website!
## Visit Your Website
* Type in your server's IP address in a web browser and see if you can visit the website.
```
http://<ip-address>
```
i.e.
```
http://148.100.77.96
```
* Make sure to type in 'http' not 'https', sometimes web browsers will automatically switch it to 'https'. If this happens, use Firefox.
* If you forgot your IP address, run the following command or get it from [here](https://linuxone.cloud.marist.edu/#/instance):
```
ip a
```
* You'll see something like the following. You are looking for the value after 'inet' in the 'enc1000' section. In this case `148.100.77.96`:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
3: enc1000: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 02:b1:01:69:5a:04 brd ff:ff:ff:ff:ff:ff
    inet 148.100.77.96/22 brd 148.100.79.255 scope global noprefixroute enc1000
       valid_lft forever preferred_lft forever
    inet6 fe80::b1:1ff:fe69:5a04/64 scope link 
       valid_lft forever preferred_lft forever
```
* If you see the `Red Hat Enterprise Linux Test Page`, you have successfully completed this section!

## Review
If you made it this far, nice work!! This section was a lot tougher than the first. Hopefully it wasn't too difficult. And now you have the beginnings of a website! You'll customize it further in the next section, but first let's review the commands you learned in this section:
* `uname` for basic system information
* `dnf` to install packages
* `top` to see resource usage and processes
* `systemctl` to manage system services
* `sudo` to run commands with administrative privileges
* `firewall-cmd` to manage firewall rules
* `ip` to see IP addresses and other network info

## You are now ready to move on to [step 6](./6_website.md), where you will customize your website!
