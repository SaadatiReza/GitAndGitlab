# Prerequisities
make sure that all the necessary packages are currently installed and upgraded to the latest version.
```bash
apt update && apt upgrade -y
apt install curl openssh-server perl ca-certificates
```
in the following URL, find the proper packages regarding to your environment, then download that inside your virtual machine.
[Gitlab](https://packages.gitlab.com/gitlab/gitlab-ce)
```bash
wget "copied URL"
```
Once the package has been downloaded to your local machine, you should install it using below command.
```bash
dpkg -i *.deb
```

you can check the status of each gitlab component using the below command.
```bash
gitlab-ctl status
#or
gitlab-ctl check
```
if you want to change any configuration, you could edit the **/etc/gitlab/gitlab.rb** then reconfigure the service as follows.
```bash
gitlab-ctl reconfigure
```

find the initiated password of root user at the following path.
```bash
cat /etc/gitlab/initial_root_password
```
be informed that the existed passowrd is valid in the first 24 hours.
