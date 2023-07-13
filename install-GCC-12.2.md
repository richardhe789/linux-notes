# Install gcc version 12.2.0 (GCC) on Centos 7

##1. Creat destination
```
# pwd
/usr/local
# mkdir gcc-12.2.0
```

## 2. Download GCC and create build obj directory
```
$ cd tmp
$ wget http://mirrors.concertpass.com/gcc/releases/gcc-12.2.0/gcc-12.2.0.tar.gz
$ tar -xzf gcc-12.2.0.tar.gz
$ mkdir gcc-objdir
$ cd gcc-objdir
```

## 3. Get GCC dependency gmp
```
$ /bin/yumdownloader gmp gmp-devel

$ ls *.rpm
gmp-6.0.0-15.x86_64.rpm gmp-devel-6.0.0-15.x86_64.rpm

$ rpm2cpio gmp-6.0.0-15.x86_64.rpm | cpio -idmv
$ rpm2cpio gmp-devel-6.0.0-15.x86_64.rpm | cpio -idmv

# mv usr /usr/local/gcc-12.2.0/gmp
```

## 4. Get GCC dependency mpfr
```
$ /bin/yumdownloader mpfr mpfr-devel

$ ls *.rpm
mpfr-3.1.1-4.x86_64.rpm mpfr-devel-3.1.1-4.x86_64.rpm

$ rpm2cpio mpfr-3.1.1-4.x86_64.rpm | cpio -idmv
$ rpm2cpio mpfr-devel-3.1.1-4.x86_64.rpm | cpio -idmv

# mv usr /usr/local/gcc-12.2.0/mpfr
```
## 5. Get GCC dependency mpc
```
$ /bin/yumdownloader libmpc libmpc-devel

$ ls *.rpm
libmpc-1.0.1-3.x86_64.rpm libmpc-devel-1.0.1-3.x86_64.rpm

$ rpm2cpio libmpc-1.0.1-3.x86_64.rpm | cpio -idmv
$ rpm2cpio libmpc-devel-1.0.1-3.x86_64.rpm | cpio -idmv

# mv usr /usr/local/gcc-12.2.0/mpc
```

## 6. Get GCC dependency isl
```
$ /bin/yumdownloader isl.x86_64 isl-devel.x86_64

$ ls *.rpm
isl-0.16.1-6.x86_64.rpm isl-devel-0.16.1-6.x86_64.rpm

$ rpm2cpio isl-0.16.1-6.x86_64.rpm | cpio -idmv
$ rpm2cpio isl-devel-0.16.1-6.x86_64.rpm | cpio -idmv

# mv usr /usr/local/gcc-12.2.0/isl
```
## 7. Configure
Run as regular user
```
$ cd tmp/gcc-objdir
$ ../gcc-12.2.0/configure \
--prefix=/usr/local/gcc-12.2.0 \
--with-gmp-include=/usr/local/gcc-12.2.0/gmp/include \
--with-gmp-lib=/usr/local/gcc-12.2.0/gmp/lib64 \
--with-mpfr-include=/usr/local/gcc-12.2.0/mpfr/include \
--with-mpfr-lib=/usr/local/gcc-12.2.0/mpfr/lib64 \
--with-mpc-include=/usr/local/gcc-12.2.0/mpc/include \
--with-mpc-lib=/usr/local/gcc-12.2.0/mpc/lib64 \
--with-isl-include=/usr/local/gcc-12.2.0/isl/include \
--with-isl-lib=/usr/local/gcc-12.2.0/isl/lib64 \
--disable-multilib
```

## 8. Compile
Run as regular user, it will take some time.
```
$ make -j8
```
## 9. Install
Run as root
```
# amke install
```

## 10. verify
```
$ /usr/local/gcc-12.2.0/bin/gcc -v
Target: x86_64-pc-linux-gnu
gcc version 12.2.0 (GCC)
```
## 11. Set env for gcc
```
setenv CC /usr/local/gcc-12.2.0/bin/gcc
setenv CXX /usr/local/gcc-12.2.0/bin/g++
setenv FC /usr/local/gcc-12.2.0/bin/gfortran
setenv F90 /usr/local/gcc-12.2.0/bin/gfortran
```
