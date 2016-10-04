# Go_for_arm
how to install Go (golang) when dealing with arm architecture
```
rm -fr /usr/local/go
tar -xzf go1.4.3.linux-armv7.tar.gz -C /usr/local
export PATH=/usr/local/go/bin:$PATH
go version #test it works
```

## go1.4.3.linux-armv7.tar.gz - how it was created
The following inforamtion comes from this source: [http://blog.hypriot.com/post/how-to-compile-go-on-arm/](http://blog.hypriot.com/post/how-to-compile-go-on-arm/)
### Step-1 Downloaded and compiled the source code
```
wget https://storage.googleapis.com/golang/go1.4.3.src.tar.gz
rm -rf /usr/local/go
tar -xz -C /usr/local -f go1.4.3.src.tar.gz
cd /usr/local/go/src
time ./make.bash
```

### Step-2 Created the binary tar for further use
```
tar -czf ~/go1.4.3.linux-armv7.tar.gz -C /usr/local go
tar --numeric-owner -czf ~/go1.4.3.linux-armv7.tar.gz -C /usr/local go
```
