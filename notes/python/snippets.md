# Python Snippets

## Show dependant packages

```
$ python3.8 -m pip list | cut -d' ' -f1 | while read pkg; echo $pkg; do apt-cache rdepends --installed $pkg; done
```

### Install `pip` for Python 2

```
$ curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
$ python2 get-pip.py
```