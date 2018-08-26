[cythonのサイト](http://docs.cython.org/en/latest/src/quickstart/build.html) を理解するための個人的メモ

## Building Cython code

pythonのコードとは異なり, cythonのコードはコンパイルする必要があります. これには2つの段階があります.

- `.pyx`ファイルは, pythonの拡張モジュールとしてのコードを保持した状態でCythonによって `.c`ファイルにコンパイルされます
