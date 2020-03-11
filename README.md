# desktop
playbook to setup a desktop on a centos 7/rhel 7 vm


## testing playbook on Mac OS using docker-compose

### Enable x11 support
Create a connection between the docker container that runs a graphical application and the X window system on our OS X host operating system
```bash
$ brew install socat
$ socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
```

Install the X window system for Mac OS x
```
$ brew install Xquartz
$ open -a Xquartz
```
A white terminal window will pop up. Now open up the preferences from the top menu and go to the last tab ‘security’. There we need to make sure the “allow connections from network clients” is checked “on”.

### Enable Audio in container
```
$ brew install pulseaudio
$ brew services start pulseaudio
```


### docker-compose
Check the docker-compose.yml using
```
$ DISPLAY=$(ipconfig getifaddr en0) docker-compose config 
```

Start the container
```
$ DISPLAY=$(ipconfig getifaddr en0) docker-compose up -d
```

### ansible 
First install te roles and then test the playbook
```
$ ansible-galaxy role install -r roles/requirements.yml -p ./roles
$ ansible-playbook -i devtop_1, -c docker site.yml -v
```
