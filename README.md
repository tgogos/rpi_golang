# How to install Go on Raspberry Pi 3
## Test environment
 - Raspberry Pi 3
 - Host OS: Raspbian Jessie Lite image (downloaded [2016-09-23-raspbian-jessie-lite.zip](http://director.downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2016-09-28/2016-09-23-raspbian-jessie-lite.zip) from the official site)

# #1 Without Go Version Manager (gvm)

## Start with go1.4.3
The general idea is that you first download the source and then compile it. But, for your convenience and to bypass this procedure, this git repository has already a binary tar, named `go1.4.3.linux-armv7.tar.gz`.

 - If you want to learn how this file was generated, continue reading the relative section below (*"go1.4.3.linux-armv7.tar.gz - how it was created"*).
 - If you want to proceed with the installation, continue with the following commands. 

```bash
rm -rf /usr/local/go
git clone https://github.com/tgogos/rpi_golang.git # (current repository)
cd rpi_golang/
tar -xzf go1.4.3.linux-armv7.tar.gz -C /usr/local
export PATH=/usr/local/go/bin:$PATH
echo "export PATH=/usr/local/go/bin:$PATH" >> /root/.bashrc
go version #test it works
```

## Continue with a newer version (optional)
```bash
rm -fr $HOME/go1.4
mkdir -p $HOME/go1.4
tar -xzf go1.4.3.linux-armv7.tar.gz -C $HOME/go1.4 --strip-components=1

rm -fr /usr/local/go
wget https://dl.google.com/go/go1.10.3.src.tar.gz
tar -xz -C /usr/local -f go1.10.3.src.tar.gz

cd /usr/local/go/src
time GOROOT_BOOTSTRAP=/root/go1.4 ./make.bash
go version #test that the new version is printed out
```



---

## go1.4.3.linux-armv7.tar.gz - how it was created
The following information comes from this source: [http://blog.hypriot.com/post/how-to-compile-go-on-arm/](http://blog.hypriot.com/post/how-to-compile-go-on-arm/)
### Step-1 Downloaded and compiled the source code
```bash
wget https://storage.googleapis.com/golang/go1.4.3.src.tar.gz
rm -rf /usr/local/go
tar -xz -C /usr/local -f go1.4.3.src.tar.gz
cd /usr/local/go/src
time ./make.bash
```

### Step-2 Created the binary tar for further use
```bash
tar -czf ~/go1.4.3.linux-armv7.tar.gz -C /usr/local go
tar --numeric-owner -czf ~/go1.4.3.linux-armv7.tar.gz -C /usr/local go
```


# #2 With Go Version Manager (gvm)
[https://github.com/moovweb/gvm](https://github.com/moovweb/gvm)

```bash
sudo apt-get install curl git make binutils bison gcc build-essential
# install gvm
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
source /home/pi/.gvm/scripts/gvm

# install go
gvm install go1.4 
gvm use go1.4 
export GOROOT_BOOTSTRAP=$GOROOT 
gvm install go1.7
gvm use go1.7 --default
```



# Configuration of $PATH, $GOPATH variables
From the ["Getting Started"](https://golang.org/doc/install) page of [golang.org](https://golang.org/):

> Add `/usr/local/go/bin` to the PATH environment variable.
> You can do this by adding this line to your `/etc/profile` (for a system-wide installation)
> or `$HOME/.profile`: 

```bash
export PATH=$PATH:/usr/local/go/bin
```

Most of the times that I have used a combination of Go and Beego framework, I add the following lines:

```bash
export PATH=$PATH:/usr/local/go/bin
export GOPATH=$HOME/go

# and for the `bee` tool:
export PATH=$PATH:$GOPATH/bin
```
