# How to run [Heritrix](https://github.com/internetarchive/heritrix3)

This follows the getting started documentation [here](https://heritrix.readthedocs.io/en/latest/getting-started.html)

## Download
All of the versions are listed [here](https://repo1.maven.org/maven2/org/archive/heritrix/heritrix/3.4.0-20220727/) as of writing this, heritrix-3.4.0-20220727-dist.zip is the latest file

* Download it
```bash
curl https://repo1.maven.org/maven2/org/archive/heritrix/heritrix/3.4.0-20220727/heritrix-3.4.0-20220727-dist.zip -o heritrix-3.4.0-20220727-dist.zip
```
To unzip it you can use unzip
* Install it
```bash
sudo apt install unzip
```
* Unzip it
```bash
unzip heritrix-3.4.0-20220727-dist.zip
```

## Install
To "install" it you need to mark the file in /home/user/heritrix-3.4.0-20220727-dist/bin/heritrix as runnable
```bash
chmod u+x /home/user/heritrix-3.4.0-20220727-dist/bin/heritrix
```

## Run
To run it locally (only the machine running this can access the webpage)
```bash
/home/user/heritrix-3.4.0-20220727-dist/bin/heritrix -a login:password -p 8443
```
If you want anyone to be able to access the webpage use the following command
```bash
/home/user/heritrix-3.4.0-20220727-dist/bin/heritrix -a login:password -p 8443 -b 0.0.0.0
```
