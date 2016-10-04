# Go_for_arm
how to install Go (golang) when dealing with arm architecture


### Download and compile the source code
```
wget https://storage.googleapis.com/golang/go1.4.3.src.tar.gz
rm -rf /usr/local/go
tar -xz -C /usr/local -f go1.4.3.src.tar.gz
cd /usr/local/go/src
time ./make.bash
```

### Create a binary tar for further use (and avoid downloading/compiling again)
