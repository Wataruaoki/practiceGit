[cythonのサイト](http://docs.cython.org/en/latest/src/quickstart/build.html) を理解するための個人的メモ

## Building Cython code

pythonのコードとは異なり, cythonのコードはコンパイルする必要があります. これには2つの段階があります.

- `.pyx`ファイルが, pythonの拡張モジュールとしてのコードを保持した状態でCythonにより`.c`ファイルにコンパイルされる.

- コンパイルされた`.c`ファイルが, CコンパイラによりPythonから直接`import`可能な`.so`ファイル(もしくはWindowsでは`.pyd`)にコンパイルされる.
Distutils や setuptoolがこの役割を担っている. けれども, ある場合においてはCythonはこれらを呼び出すことができる.

Cython + Distutils/setuptoolによるビルドの過程を十分に理解するために, 
[Pythonモジュールのディストリビューション](https://docs.python.org/3/distributing/index.html)についてもっと読んでおいておくと良いでしょう.
