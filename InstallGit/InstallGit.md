# How to install git on Linux Server
There are different ways of installing git on the linux machine. each of them has its advantage and disadvantge, for instance 
one of the easiest way of installing git is using the package manager, however, you might be installing a older version of the git which existed inside the repository.
## Install Git with Package Manager
Based on the operating system you're using, please follow the below instruction
### Redhat-based OS
```bash
dnf install git
```
### Debian-based OS
```bash
apt update && apt install git -y
```


# Install Git from its source
For compiling the source code, there are some dependecies to different package wich should be installed before starting this steps.
### Redhat-Based OS
```bash
sudo dnf groupinstall "Development Tools"
sudo dnf install \
  gcc-c++ \
  make \
  cmake \
  git \
  wget \
  curl \
  tar \
  unzip \
  bzip2 \
  patch \
  openssl-devel \
  libffi-devel \
  zlib-devel \
  bzip2-devel \
  xz-devel \
  ncurses-devel \
  readline-devel \
  sqlite-devel \
  libuuid-devel \
  libxml2-devel \
  libxslt-devel \
  libcurl-devel \
  expat-devel \
  glibc-devel \
  libtool \
  gettext \
  rpm-build \
  elfutils-libelf-devel

```
### Debian-Based OS
```bash
apt install build-essential libz-dev libssl-dev libcurl4-gnutls-dev libexpat1-dev gettext unzip cmake gcc

```
Please follow [this](https://www.kernel.org/pub/software/scm/git/) url to find the proper version that you're looking for.

you must download the tarbal version to your desired location, it could be **/opt** or wherever you want.
```bash
cd /opt && wget "the tar version you've copied from above URL"
```
Now you must unarchive it, it should be usually done with the below command.
```bash
tar -xvf git*.tar.gz
```
Change the current directory to the directory you've just unarchive it. with **cd** command.

now you must execute the below command .
```bash
make prefix=/usr/local all
```
NOTE: **prefix=** will define the location which app is going to compiled. you could modify it to your desired location if you want.
This process takes couple minouts based on the resource you have. be patient

Once the last execution ends, you must run the below command to install it.
```bash
make prefix=/usr/local install
```