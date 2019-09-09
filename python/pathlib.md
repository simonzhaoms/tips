# Unify Path Manipulation with `pathlib`#

## Table of Content ##

* [Comparison](#comparison)
* [`pathlib`](#pathlib)
* [Reference](#reference)


## Comparison ##

### Error Prone ###

```python
dir_path = 'data/test/'
file_path = dir_path + 'raw.txt'                  # 'data/test/raw.txt'
file_name = file_path.split('/')[-1]              # 'raw.txt'
dir_path = file_path.rsplit('/', maxsplit=1)[0]   # 'data/test'
file_ext = file_name.split('.')[-1]               # 'txt'
file_stem = file_name.rsplit('.', maxsplit=1)[0]  # 'raw'
if os.path.exists(file_path):
    with open(file_path) as f:
        print(f.read())
```

### Old Way with `os.path` ###

```python
import os
dir_path = os.path.join('data', 'test')
file_path = os.path.join(dir_path, 'raw.txt')     # 'data/test/raw.txt'
file_name = os.path.basename(file_path)           # 'raw.txt'
dir_path = os.path.dirname(file_path)             # 'data/test'
file_ext = file_name.split('.')[-1]               # 'txt'
file_stem = file_name.rsplit('.', maxsplit=1)[0]  # 'raw'
if os.path.exists(file_path):
    with open(file_path) as f:
        print(f.read())
```

### New Way with `pathlib` ###

```python
from pathlib import Path
dir_path = Path('data/test')
file_path = dir_path / 'raw.txt'  # 'data/test/raw.txt'
file_name = file_path.name        # 'raw.txt'
file_name = file_path.parts[-1]   # 'raw.txt'
dir_path = file_path.parent       # Path('data/test')
file_ext = file_path.suffix       # '.txt'
file_stem = file_path.stem        # 'raw'
if file_path.exists():
    with open(file_path) as f:    # ==> with file_path.open() as f:
        print(f.read())
```

## `pathlib` ##

```python
from pathlib import Path

# Create path from string
a = Path('data/test/raw.txt')

# Existing path
a = Path.cwd()   # Current working directory
a = Path.home()  # Home directory: '~'

# Create path from parts
a = Path.home() / 'data' / 'test' / 'raw.txt'
a = Path.home().joinpath('data', 'test', 'raw.txt')  # Equivalent to the above
b = a.parent.parent / 'train' / 'raw.txt'  # 'data/train/raw.txt'

# Create new path from old one
b = a.with_suffix('.py')  # 'data/test/raw.py'

# Read file
with a.open() as f:
    print(f.read())
# Or directly handle file opening and closing internally by Path's method
print(a.read_text())

# Move raw.txt to raw.py
a.replace(a.with_suffix('.py'))

# Remove file
a.unlink()

# Remove dir
a.parent.rmdir()

# Iterate through files
d = [f for f in Path.cwd().iterdir()]      # Similar results of shell command `ls` without '.' and '..'
d = [f for f in Path.cwd().glob('*.py')]   # ls *.py
d = [f for f in Path.cwd().rglob('*.py')]  # find . -name *.py
```


## Reference ##

* [Python 3's pathlib Module: Taming the File System](https://realpython.com/python-pathlib/)
