# crosscompileOpensshArm
cross compile for openssh server for armvh


/////////////////////////
Activate env
/////////////////////////
```console
export CC=/opt/arm/arm-ca53-linux-gnueabihf-6.4/usr/bin/arm-ca53-linux-gnueabihf-gcc
export LD_LIBRARY_PATH=/opt/arm/arm-ca53-linux-gnueabihf-6.4/lib
export LV_LIBSSH_PATH=$(pwd)
```

/////////////////////////
Build Zlib:
/////////////////////////
```console
unzip zlib1211.zip
cd zlib-1.2.11
mkdir build-arm
./configure --prefix=$LV_LIBSSH_PATH/zlib-1.2.11/build-arm
make -j8
make -j8 install
```

/////////////////////////
Build OpenSSL:
/////////////////////////
```console
cd $LV_LIBSSH_PATH
tar xf openssl-1.1.0f.tar.gz
cd openssl-1.1.0f
mkdir build-arm
./Configure linux-armv4 shared --prefix=$LV_LIBSSH_PATH/openssl-1.1.0f/build-arm
make -j8
make -j8 install
```

/////////////////////////
Build OpenSSH:
/////////////////////////
```console
cd $LV_LIBSSH_PATH
tar xf openssh-8.8p1.tar.gz
cd openssh-8.8p1
mkdir build-arm
./configure --host=arm-ca53-linux-gnueabihf --with-libs --with-zlib=$LV_LIBSSH_PATH/zlib-1.2.11/build-arm --with-ssl-dir=$LV_LIBSSH_PATH/openssl-1.1.0f/build-arm --disable-etc-default-login --prefix=$LV_LIBSSH_PATH/openssh-8.8p1/build-arm
make -j8
make -j8 install
```


/////////////////////////
BUILD DROPBEAR
/////////////////////////
```console
tar xf dropbear-2020.81.tar.bz2
cd dropbear-2020.81
export CC=/opt/arm/arm-ca53-linux-gnueabihf-6.4/usr/bin/arm-ca53-linux-gnueabihf-gcc
export LD_LIBRARY_PATH=/opt/arm/arm-ca53-linux-gnueabihf-6.4/lib
mkdir build-arm
./configure --prefix=/home/ubuntu/dropbear-2020.81/build-arm --host=arm-ca53-linux-gnueabihf
make -j8
make -j8 install
```
