# Modules

## Modules

- module is a Python file (e.g. `my_mod.py`) on **sys.path**:
    - directory from which the input script was run, or the current directory if the interpreter is being run interactively
    - list of directories contained in the `PYTHONPATH` environment variable, if it is set
    - An installation-dependent list of directories configured at the time Python is installed
- **module types**
    - written in Python itself
    - built-in module (e.g.`itertools`)
    - written in C and loaded dynamically at run-time (e.g. `re`)
- `dir()` - list of names in the current local scope
- `dir(object)` - list of names for the given object (module, class, ..)
- `my_mod.__file__` - module file (not available for built-in modules)

## Packages

- folder with Python files (modules)
- `__init__.py` - invoked when importing the package or a module from the package

### Import

- module is initialized the first time it is imported (like `static` blocks in Java)
- **dynamic imports** - imports can be anywhere in the code
  ```python3
  if visual_mode:
      import draw_visual as draw
  else:
      import draw_textual as draw
  ```
- handling import errors - `except ImportError:`

#### import MODULE [as ALIAS]

- imports the module/package namespace (private symbol table)
  ```python3
  import foo.bar
  foo.bar.x  # OK, foo.bar was imported
  dir()  # .., foo
  ```

#### from MODULE import OBJECT [as ALIAS]

- directly imports the given object name into the current namespace (like `static import` in Java)
  ```python3
  from foo.bar import x
  x  # OK, foo.bar.x was imported
  dir()  # .., x
  ```

#### from MODULE/PACKAGE import *

- **module** - directly imports all the names from the given module except for names starting with `_`
    - similar to packages, what's imported can be changed by defining `__all__` variable
- **package** - by default does nothing
    - define `__all__` in `__init__.py` and define what `*` should import
- risk of overwriting already defined names
