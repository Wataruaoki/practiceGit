[cythonのサイト](http://docs.cython.org/en/latest/src/quickstart/build.html) を理解するための個人的メモ

英語及びmarkdownの練習も兼ねているのでそこはご承知を... 以下からが内容

***

## Building Cython code

pythonのコードとは異なり, cythonのコードはコンパイルする必要があります. これには2つの段階があります.

- `.pyx`ファイルが, pythonの拡張モジュールとしてのコードを保持した状態でCythonにより`.c`ファイルにコンパイルされる.

- コンパイルされた`.c`ファイルが, CコンパイラによりPythonから直接`import`可能な`.so`ファイル(もしくはWindowsでは`.pyd`)にコンパイルされる.
Distutils や setuptoolsがこの役割を担っている. けれども, ある場合においてはCythonはこれらを呼び出すことができる.

Cython + Distutils/setuptoolsによるbuildの過程を十分に理解するために, 
[PythonモジュールのDistribution](https://docs.python.org/3/distributing/index.html)についてもっと読んでおいておくと良いでしょう.


Cythonのコードをbuildする方法はいくつか存在する :
- Distutils/setuptools の setup.py を書く : これが通常推奨されている方法である.
- [Pyximport](http://docs.cython.org/en/latest/src/userguide/source_files_and_compilation.html#pyximport)を用いる方法 - まるで'.py'ファイルであるかのようににCythonの'pyx'ファイルをimportする.(distutilsを用いてコンパイルし, バックグランドでbuildを行う)
- 
- 

Write a distutils/setuptools setup.py. This is the normal and recommended way.
Use Pyximport, importing Cython .pyx files as if they were .py files (using distutils to compile and build in the background). This method is easier than writing a setup.py, but is not very flexible. So you’ll need to write a setup.py if, for example, you need certain compilations options.
Run the cython command-line utility manually to produce the .c file from the .pyx file, then manually compiling the .c file into a shared object library or DLL suitable for import from Python. (These manual steps are mostly for debugging and experimentation.)
Use the [Jupyter] notebook or the [Sage] notebook, both of which allow Cython code inline. This is the easiest way to get started writing Cython code and running it.
