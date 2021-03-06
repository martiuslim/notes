# Linux
General notes for Linux distros, in particular `Fedora`.

### Useful Applications
- [Visual Studio Code for Fedora](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions)
- [Telegram Desktop](https://desktop.telegram.org/)
- [Slack for Linux](https://slack.com/downloads/linux)
- [Spotify for Fedora](https://fedoraproject.org/wiki/Spotify)

## Installing & Updating Packages using DNF [Link](http://dnf.readthedocs.io/en/latest/)
In Fedora, `dnf` has been the default package manager since version 22. It stands for `dandified yum` or the next generation version of the `Yellowdog Updater, Modified` or `yum`. 

The documentation for `dnf` commands can be [found here](http://dnf.readthedocs.io/en/latest/command_ref.html). Some of the common commands are `install`, `check-update`, `upgrade`.

To install packages while automatically bypassing the prompts, you may use the `-y` or `--assumeyes` to answer yes to all questions. For example, `dnf install -y <package>`.

## Bash Scripting
Scripts are basically just a series of commands in a plain text file and are useful for automating tasks so that you don't have to type them manually. In short, what's important is that you can put anything you can run normally on the command line into a script and it will do the exact same thing and vice versa.

Here's an example of a simple `Hello World` script in a file named `hello-script`.

```
#!/bin/bash
# Sample 'Hello World' Script

echo Hello World!
```

Line 1 contains what is known as the `shebang` or `#!`. This is followed by the path to the interpreter/ program (in this case, it is `bash`) that will execute the following lines in the script file. The `shebang` must be the very first line in the file. 

In order to run this script, we need to ensure that the script file has the `execute` permission set as it is generally not set by default for safety reasons. We can do this using the `chmod` command. [Click here to learn more about `chmod`](https://www.tutorialspoint.com/unix_commands/chmod.htm).

One example is `700` where the owner has full read, write and execute permissions for the file. You can then run `chmod 700 hello-script`.

You may now run your script with `./hello-script`.

## Time Synchronization when dual-booting
You may run into issues with the system clock when dual-booting Linux with Windows (either from a separate partition or off a flash-drive). For example, your system clock may be correct on your Linux side, but when you boot back into Windows, you may find that your system clock is not synchronized and may be behind time. 

This is a common issue and a great answer can be [found here](https://askubuntu.com/questions/169376/clock-time-is-off-on-dual-boot). 

Solution: open a terminal (on your Linux) and execute the following command
`timedatectl set-local-rtc 1`.

## scp (Secure Copy) [Link](https://linux.die.net/man/1/scp)
You may use `scp` to securely transfer files between hosts. It uses the same authentication and provides the same security as `ssh`.

Some useful flags:
- `-i`: to provide your ssh key for authentication
- `-v`: to show the full debug logs as scp will be silent otherwise.

### Transferring files to remote host (Uploading)
The general syntax is as follows:  
`scp -i <path_to_ssh_keyfile> <path_to_file_to_upload> <user>@<host>:<directory_to_upload>`

Example:  
`scp -i ~/.ssh/privatekey file-to-upload root@ip-addr:home`

### Transferring files from remote host (Downloading)
The general syntax is as follows:  
`scp -i <path_to_ssh_keyfile> <user>@<host>:<path_to_file_to_download> <directory_to_download>`

Example:  
`scp -i ~/.ssh/privatekey root@ip-addr:home/file-to-download home`
