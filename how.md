#### [cythonのサイト](http://docs.cython.org/en/latest/src/quickstart/build.html) を理解するための個人的メモ1 

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



## Building a Cython module using distutils
```hello.pyx```ファイルに書かれた簡単な"hello world"スクリプトをイメージしてください

```python3
def say_hello_to(name):
    print("Hello %s!" % name)
```

次に対応する```setup.py```スクリプトについて

```python3
from distutils.core import setup
from Cython.Build import cythonize

setup(name='Hello world app',
      ext_modules=cythonize("hello.pyx"))
```

buildを行うために ```python setup.py build_ext --inplace```を実行してください.
すると pythonのコードにおいて,```from hello import say_hello_to``` と記述すれば, 好きなようにimportした関数が使えます


distutilsの代わりにsetuptoolsを用いる場合は, ```python setup.py install```の実行中におけるデフォルト動作では, 冷凍された```egg```ファイルができますが, ```pxd```ファイルと独立したパッケージとして使用しようとした場合, ```cimport```で動かないことに注意してください. このようなことを防ぐために ```setup()```において```zip_safe=False```を含めて記述する必要があります


## Using the Jupyter notebook

Cythonは[Jupyter notebook](http://jupyter.org)を用いてwebブラウザ上において対話的に, 便利に使うことができます. [Jupyter notebook](http://jupyter.org)をインストールするには, 例えば virtualenv を立ち上げて ```pip```を用います.

```
(venv)$ pip install jupyter
(venv)$ jupyter notebook
```


インストールガイドにあるようにCythonをインストールして, Cythonによる拡張を読み込んめば, Cythonが編集できるようになります :

```
%load_ext Cython
```

そして, セルの先頭で```%%cython```マーカーをつけてコンパイルを行います.

```python3
%%cython

cdef int a = 0
for i in range(10):
    a += i
print(a)
```


```--annotate```オプションを引き渡すことで Cythonコードの分析が表示できます.

```
%%cython --annotate
...
```

![aaaa](http://docs.cython.org/en/latest/_images/jupyter.png)


```%%cython```マジックコードについてもっと知りたい場合は次のリンクを参照してください  [Compiling with a Jupyter Notebook](http://docs.cython.org/en/latest/src/userguide/source_files_and_compilation.html#compiling-notebook)


## Using the Sage notebook

![aa](http://docs.cython.org/en/latest/_images/sage.png)

For users of the Sage math distribution, the Sage notebook allows transparently editing and compiling Cython code simply by typing %cython at the top of a cell and evaluate it. Variables and functions defined in a Cython cell imported into the running session.

