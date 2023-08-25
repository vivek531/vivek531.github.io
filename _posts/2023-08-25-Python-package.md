---
layout: post
title: "Python packages"
date: 2023-07-15
---

module - python file
package - collection of files

python -m module == python module.py
python -m package == python __main__.py (__main__.py file in package directory)

One advantage of using -m is that it allows you to call all modules/files that are in your Python path, including those that are built into Python. One example is calling antigravity:
$ python -m antigravity

If you want to run a built-in module without -m, then you’ll need to first look up where it’s stored on your system and then call it with its full path.

build systems

1. https://setuptools.pypa.io/en/latest/userguide/quickstart.html

three ways to provide configuration files

1. setup.py
2. setup.cfg
3. pyproject.toml



