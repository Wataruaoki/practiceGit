[cythonのサイト](http://docs.cython.org/en/latest/src/quickstart/build.html) を理解するための個人的メモ1

英語及びmarkdownの練習も兼ねているのでそこはご承知を... 以下からが内容

***

## Building Cython code

pythonのコードとは異なり, cythonのコードはコンパイルする必要があります. これには2つの段階があります.

- `.pyx`ファイルが, pythonの拡張モジュールとしてのコードを保持した状態でCythonにより`.c`ファイルにコンパイルされる.

- コンパイルされた`.c`ファイルが, CコンパイラによりPythonから直接`import`可能な`.so`ファイル(もしくはWindowsでは`.pyd`)にコンパイルされる.
Distutils や setuptoolsがこの役割を担っている. けれども, ある場合においてはCythonはこれらを呼び出すことができる.

Cython + Distutils/setuptoolsによるbuildの過程を十分に理解するために, 
[PythonモジュールのDistribution](https://docs.python.org/3/distributing/index.html)についてもっと読んでおいておくと良いでしょう.


Cythonのコードをbuildする方法 :
- Distutils/setuptools の setup.py を記述する : これが通常推奨されている方法である.
- [Pyximport](http://docs.cython.org/en/latest/src/userguide/source_files_and_compilation.html#pyximport)を用いる方法 - まるで`.py`ファイルであるかのようににCythonの`.pyx`ファイルをimportする(distutilsを用いてコンパイルし, バックグランドでbuildを行う). この方法は前述のsetup.pyを記述する方法よりも簡単であるが, 柔軟な対応ができない. ゆえに, 編集ができるかのオプションが必要な場合のようなことがあれば, setup.pyを記述する必要があります
- `.pyx`ファイルを元に`.c`ファイルを作成するために手動で`cython`コマンドラインユーティリティーを実行し, そして手動で`.c`ファイルをコンパイルし, オブジェクトライブラリやPythonからimportに適したDLLを作成する.(このような手動のステップはデバックや研究が目的の場合がほとんどです)
- Jupyter Notebook や Sage Notebookを用いる方法, どちらもCythonコードがインラインで使用可能. この方法がCythonのコードを記述して, 動かすには一番簡単な方法です.
