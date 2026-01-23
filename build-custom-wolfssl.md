# Building Custom WolfSSL Library

## Dependencies

```bash
sudo apt update && \\
sudo apt install automake autoconf libtool-bin checkinstall
```

## Download WolfSSL Source Code

```bash
wget https://github.com/wolfSSL/wolfssl/archive/refs/tags/v5.8.4-stable.tar.gz && \\
tar -xzvf v5.8.4-stable.tar.gz && \\
cd wolfssl-5.8.4-stable
```

## Configure Build Options

```bash
./autogen.sh
```

```bash
./configure --prefix=/usr/local --enable-cryptonly --enable-sha --enable-sha512 \
    --enable-aes --enable-aesctr --enable-rsa --enable-pkcs7 --enable-pkcs11 \
    --enable-pkcs12 --enable-keygen --disable-md5 --disable-sha3 \
    --disable-dh --disable-ecc --disable-examples
```

```bash
sudo checkinstall
```

> Note: During the `checkinstall` process, you will be prompted to enter package information. You can accept the defaults or customize them as needed.

Sample:

```txt
Should I create a default set of package docs?  [y]: y
...

This package will be built according to these values:

0 -  Maintainer: [ root@kali-wsl ]
1 -  Summary: [  ]
2 -  Name:    [  ]
3 -  Version: [  ]
4 -  Release: [ 1 ]
5 -  License: [ GPL ]
6 -  Group:   [ checkinstall ]
7 -  Architecture: [ amd64 ]
8 -  Source location: [ wolfssl-5.8.4-stable ]
9 -  Alternate source location: [  ]
10 - Requires: [  ]
11 - Recommends: [  ]
12 - Suggests: [  ]
13 - Provides: [  ]
14 - Conflicts: [  ]
15 - Replaces: [  ]
16 - Prerequires: [  ]

Enter a number to change any of them or press ENTER to continue:
```

When the customization is complete, press `ENTER` to start the local build and installation process.

```txt
**********************************************************************

 Done. The new package has been installed and saved to

 /tmp/wolfssl-build/wolfssl-5.8.4-stable/wolfssl-semo_5.8.4-stable_amd64.deb

 You can remove it from your system anytime using:

      dpkg -r wolfssl-semo

**********************************************************************
```

## Update Library Cache

```bash
sudo ldconfig && \\
ldconfig -p | grep wolfssl
```

## Package Distribution & Re-installation

The generated `.deb` package can be found in the output path shown at the end of the `checkinstall` process. You can distribute this package and install it on other systems using:

```bash
sudo dpkg -i /path/to/wolfssl-semo_5.8.4-stable_amd64.deb
```

> *Note: Replace `/path/to/` with the actual path where the `.deb` package is located. This will install the custom WolfSSL library with the specified configurations on the target system.*
