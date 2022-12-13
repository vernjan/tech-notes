# Managing Dependencies

- `usr/lib/python3.x/` is **Python Standard Library**
- **system-wide packages** for all Python 3 versions are in
    - `usr/lib/python3/dist-packages`
    - `/usr/local/lib/python3/dist-packages`
    - installed with `apt`
- **local packages** specific for each Python version are in
    - `$HOME/.local/lib/python3.x/site-packages`
    - installed with `pip`

## Using `pip` or `venv` with multiple Python versions

- `pip` and `venv` are just Python modules:
  ```
  $ python2.7 -m pip install
  $ python3.8 -m pip install
  $ python3.10 -m venv venv
  ```
- for Python 2, use `virtualenv` module

## venv

```
$ python3.x -m venv venv
$ source venv/bin/activate
$ (venv) ..
```

- pre-installed since 3.3
- must-have for managing multiple projects
- a lightweight copy of Python environment
    - **binaries** (or just symlinks)
    - **site packages** (i.e. dependencies)
        - may or may not include system-wide packages (option `--system-site-packages`)
    - `pyenv.cfg`
    - links standard lib (doesn't copy by default)
- venv modifies
    - `PATH` to use the venv binaries
    - command prompt (`venv`)
- it's possible to use **venvs with absolute path**, no activation is needed
    - useful for scripts
- uses `ensurepip` to bootstrap `pip`

## virtualenv

- more powerful than `venv`
- doesn't come pre-installed with Python
- use for Python 2 or if you need something more advanced

## Debugging

- Print `sys.prefix` - must point to venv home
  ```
  >>> print(sys.prefix)
  /tmp/my-venv
  ```
- Print `sys.path` - must point to the correct site-packages

  ```
  >>> print(sys.path)
  ['', '/usr/lib/python310.zip', '/usr/lib/python3.10', '/usr/lib/python3.10/lib-dynload', '/tmp/honza-venv/lib/python3.10/site-packages']
  ```