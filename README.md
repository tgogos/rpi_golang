# Go_for_arm
How to install Go (golang) when dealing with arm architecture. Tests were done on a Raspberry Pi 2 with Raspbian Jessie.

##Start with go1.4.3
The general idea is that you first download the source and then compile it. But, for your convenience and to bypass this procedure, this git repository has already a binary tar, named `go1.4.3.linux-armv7.tar.gz`.

 - If you want to learn how this file was generated, continue reading the relative section below (*"go1.4.3.linux-armv7.tar.gz - how it was created"*).
 - If you want to proceed with the installation, continue with the following commands. 

```bash
rm -fr /usr/local/go
tar -xzf go1.4.3.linux-armv7.tar.gz -C /usr/local
export PATH=/usr/local/go/bin:$PATH
go version #test it works
```

##Continue with a newer version (optional)
```bash
rm -fr $HOME/go1.4
mkdir -p $HOME/go1.4
tar -xzf go1.4.3.linux-armv7.tar.gz -C $HOME/go1.4 --strip-components=1

rm -fr /usr/local/go
wget https://storage.googleapis.com/golang/go1.5.2.src.tar.gz
tar -xz -C /usr/local -f go1.5.2.src.tar.gz

cd /usr/local/go/src
time GOROOT_BOOTSTRAP=/home/pi/go1.4 ./make.bash
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
