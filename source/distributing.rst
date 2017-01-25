==================================
プロジェクトのパッケージングと配布
==================================

:Page Status: Complete
:Last Reviewed: 2015-09-08

このセクションでは、独自の Python プロジェクトを設定、パッケージ、配布
する方法の基本を説明する。:doc:`installing` のページの内容は既に熟知し
ていることを前提とする。

このセクションは Python プロジェクト開発のベストプラクティス全体を網羅
するものでは *ない* 。例えば、バージョン管理、文書化、テストのためのガ
イダンスや推奨ツールは提供しない。

詳細なリファレンスは :ref:`setuptools` ドキュメントの
`Building and Distributing Packages
<https://setuptools.readthedocs.io/en/latest/setuptools.html>`_ を見
よ。ただしそこにあるいくつかの勧告は内容が古くなっているかもしれない。
不整合な点があれば、Python Packaging User Guide の方を選択せよ。

.. contents:: Contents
   :local:


パッケージングと配布の要件
==========================

1. まず、:ref:`パッケージインストールの要件 <installing_requirements>`
   を満たしていることを確認する。

2. "twine" をインストール [1]_:

   ::

    pip install twine

   これはプロジェクトの :term:`distribution <Distribution Package>` を
   :term:`PyPI <Python Package Index (PyPI)>` にアップロードするために
   必要だ(:ref:`以下 <Uploading your Project to PyPI>` を参照)。


プロジェクトの設定
==================


初期ファイル
------------

setup.py
~~~~~~~~

最も重要なファイルは "setup.py" だ。これはプロジェクトのルートディレク
トリに置かれる。サンプルは `PyPA sample project
<https://github.com/pypa/sampleproject>`_ の `setup.py
<https://github.com/pypa/sampleproject/blob/master/setup.py>`_ を見よ。

"setup.py" は主に 2 つの機能を提供する:

1. プロジェクトのさまざまな側面の設定。 ``setup.py`` の第一の特徴は、
   グローバル関数 ``setup()`` の単一の呼び出しを含むことだ。この関数に
   渡すキーワード引数によって、プロジェクトの詳細が定義される。最も重
   要な引数群は:ref:`以下のセクション <setup() args>` で説明する。

2. パッケージングタスクに関連するさまざまなコマンドを実行するコマンド
   ラインインターフェース。コマンドの一覧を得るには、
   ``python setup.py --help-commands`` を実行する。


setup.cfg
~~~~~~~~~

"setup.cfg" は ``setup.py`` コマンドのデフォルトオプションを含む ini
ファイルだ。サンプルは `PyPA sample project
<https://github.com/pypa/sampleproject>`_ の `setup.cfg
<https://github.com/pypa/sampleproject/blob/master/setup.cfg>`_ を見
よ。


README.rst
~~~~~~~~~~

全てのプロジェクトはその目的を記した readme ファイルを含むべきだ。最も
一般的なフォーマットは `reStructuredText
<http://docutils.sourceforge.net/rst.html>`_ で、拡張子 "rst" を持つ
が、これは必須事項ではない。

サンプルは `PyPA sample project
<https://github.com/pypa/sampleproject>`_ の `README.rst
<https://github.com/pypa/sampleproject/blob/master/README.rst>`_ を見
よ。

MANIFEST.in
~~~~~~~~~~~

"MANIFEST.in" は ``python setup.py sdist (or bdist_wheel)`` が自動では
パッケージに含めないファイルを追加したい場合に必要だ。デフォルトでパッ
ケージに含まれるファイルのリストは、:ref:`distutils` ドキュメントの
`Specifying the files to distribute
<https://docs.python.org/3.4/distutils/sourcedist.html#specifying-the-files-to-distribute>`_
を見よ。

サンプルは `PyPA sample project
<https://github.com/pypa/sampleproject>`_ の `MANIFEST.in
<https://github.com/pypa/sampleproject/blob/master/MANIFEST.in>`_ を見
よ。


``MANIFEST.in`` ファイルの記述の詳細は、:ref:`distutils` ドキュメント
の `The MANIFEST.in template
<https://docs.python.org/2/distutils/sourcedist.html#the-manifest-in-template>`_
を見よ。


<your package>
~~~~~~~~~~~~~~

これは必須ではないが、プロジェクト内の Python モジュールとパッケージは
プロジェクトと同 :ref:`名 <setup() name>` もしくは非常に似た名前の単一
トップレベルパッケージ以下に置くのが最も一般的なやり方だ。

サンプルは `PyPA sample project
<https://github.com/pypa/sampleproject>`_ に含まれる `sample
<https://github.com/pypa/sampleproject/tree/master/sample>`_ パッケー
ジを見よ。


.. _`setup() args`:

setup() の引数
--------------

前述の通り、 ``setup.py`` の第一の特徴はグローバル関数 ``setup()`` へ
の単一の呼び出しを含むことだ。この関数へのキーワード引数によってプロ
ジェクトの詳細が定義される。

最も重要な引数群を以下で説明する。各コード片は `PyPA sample project
<https://github.com/pypa/sampleproject>`_ に含まれる `setup.py
<https://github.com/pypa/sampleproject/blob/master/setup.py>`_ からの
引用だ。


.. _`setup() name`:

name
~~~~

::

  name='sample',

これはプロジェクトの名前であり、:term:`PyPI <Python Package Index
(PyPI)>` 上での表示に使われる。使える文字の詳細は、:pep:`426` の
:pep:`name <426#name>` セクションを見よ。


version
~~~~~~~

::

  version='1.2.0',

これはプロジェクトの現在のバージョンだ。これによってユーザは最新版をイ
ンストールしているか判断でき、またユーザ自身のソフトウェアがどのバー
ジョンに対してテスト済みかを示せる。

プロジェクトを公開すると、:term:`PyPI <Python Package Index (PyPI)>`
上では各リリースについてバージョンが表示される。

バージョン番号を使ってユーザに互換性情報を伝える方法の詳細は、
:ref:`Choosing a versioning scheme` を見よ。

プロジェクトコード自体が実行時にバージョン番号へのアクセスを必要とする
場合、最も単純な方法は ``setup.py`` とコードの両方にバージョン番号を書
くことだ。値の重複を避けたいのであれば、方法はいくつかある。追加トピッ
クの「:ref:`Single sourcing the version` 」を見よ。


description
~~~~~~~~~~~

::

  description='A sample Python project',
  long_description=long_description,

プロジェクトの短い説明と長い説明だ。プロジェクトを公開すると、
:term:`PyPI <Python Package Index (PyPI)>` 上でこれらの値が表示され
る。


url
~~~

::

  url='https://github.com/pypa/sampleproject',


プロジェクトのホームページ URL を書く。


author
~~~~~~

::

  author='The Python Packaging Authority',
  author_email='pypa-dev@googlegroups.com',

作者に関する情報を書く。


license
~~~~~~~

::

  license='MIT',

ライセンスの種別を書く。


classifiers
~~~~~~~~~~~

::

  classifiers=[
      # How mature is this project? Common values are
      #   3 - Alpha
      #   4 - Beta
      #   5 - Production/Stable
      'Development Status :: 3 - Alpha',

      # Indicate who your project is intended for
      'Intended Audience :: Developers',
      'Topic :: Software Development :: Build Tools',

      # Pick your license as you wish (should match "license" above)
       'License :: OSI Approved :: MIT License',

      # Specify the Python versions you support here. In particular, ensure
      # that you indicate whether you support Python 2, Python 3 or both.
      'Programming Language :: Python :: 2',
      'Programming Language :: Python :: 2.6',
      'Programming Language :: Python :: 2.7',
      'Programming Language :: Python :: 3',
      'Programming Language :: Python :: 3.2',
      'Programming Language :: Python :: 3.3',
      'Programming Language :: Python :: 3.4',
  ],

プロジェクトの分類に使われる値のリストを書く。完全なリストは
https://pypi.python.org/pypi?%3Aaction=list_classifiers を見よ。


keywords
~~~~~~~~

::

  keywords='sample setuptools development',

プロジェクトを説明するキーワードのリスト。


packages
~~~~~~~~

::

  packages=find_packages(exclude=['contrib', 'docs', 'tests*']),


It's required to list the :term:`packages <Import Package>` to be included
in your project.  Although they can be listed manually,
``setuptools.find_packages`` finds them automatically.  Use the ``exclude``
keyword argument to omit packages that are not intended to be released and
installed.

プロジェクトに含まれる :term:`パッケージ <Import Package>` のリストを
得るために必要となる。手動でリストを書いてもよいが、
``setuptools.find_packages`` を使うと自動で探してくれる。 ``exclude``
キーワード引数を使うことで、リリース/インストールしたくないパッケージ
を除外できる。


install_requires
~~~~~~~~~~~~~~~~

::

 install_requires=['peppercorn'],

"install_requires" は、プロジェクトの実行のために最小限必要な依存関係
を指定するのに使う。:ref:`pip` がプロジェクトをインストールするとき、
この指定に従って依存パッケージがインストールされる。

"install_requires" の使用については、:ref:`install_requires vs
Requirements files` により詳しい情報がある。


.. _`Package Data`:

package_data
~~~~~~~~~~~~

::

 package_data={
     'sample': ['package_data.dat'],
 },


:term:`パッケージ <Import Package>` に追加のファイルをインストールしな
ければならないことがしばしばある。これらはパッケージの実装に深く関わる
データだったり、パッケージを使うプログラマの関心を引くようなドキュメン
トを含むテキストファイルだったりする。これらのファイルは "package
data" と呼ばれる。

"package_data" の値はパッケージ名から相対パス名群へのマッピングであ
り、指定されたファイルがパッケージへコピーされる。パスはパッケージを含
むディレクトリからの相対パスとして解釈される。

詳しくは、 `setuptools ドキュメント
<https://setuptools.readthedocs.io>`_ の `Including Data Files
<https://setuptools.readthedocs.io/en/latest/setuptools.html#including-data-files>`_
を見よ。


.. _`Data Files`:

data_files
~~~~~~~~~~

::

    data_files=[('my_data', ['data/data_file'])],

ほとんどの場合は :ref:`Package Data` 設定で事足りるが、場合によっては
:term:`パッケージ <Import Package>` の *外* にデータファイルを置く必要
があるかもしれない。 ``data_files`` ディレクティブはこれを可能にする。

シーケンス内の各 (directory, files) ペアでインストール先ディレクトリと
そこに置くファイル群を指定する。ディレクトリが相対パスの場合、
installation prefix (pure-Python :term:`distribution <Distribution
Package>` なら Python の sys.prefix, 拡張モジュールを含むなら
sys.exec_prefix) からの相対パスとして解釈される。各ファイル名はプロ
ジェクトの source distribution のトップにある ``setup.py`` からの相対
パスとして解釈される。

詳しくは、distutils の `Installing Additional Files
<http://docs.python.org/3.4/distutils/setupscript.html#installing-additional-files>`_
セクションを見よ。

.. note::

  :ref:`setuptools` は "data_files" に絶対パスを許しており、
  :term:`sdist <Source Distribution (or "sdist")>` からのインストール
  時は、pip はそれを絶対パスのまま扱う。しかし :term:`wheel`
  distribution からのインストール時はそうではない。Wheels は絶対パスを
  サポートしておらず、"site-packages" からの相対パスへのインストールと
  なる。この件に関する議論は `wheel Issue #92
  <https://bitbucket.org/pypa/wheel/issue/92>`_ を見よ。


scripts
~~~~~~~

``setup()`` は、予め作成されたスクリプトをインストールするための
`scripts
<http://docs.python.org/3.4/distutils/setupscript.html#installing-scripts>`_
キーワードをサポートしている。しかし、プラットフォーム間の互換性のため
に推奨されるアプローチは :ref:`console_scripts` エントリポイントを使う
ことだ(下記参照)。


entry_points
~~~~~~~~~~~~

::

  entry_points={
    ...
  },


このキーワードを使うと、プロジェクトまたは依存パッケージにより定義され
る名前付きエントリポイントとしてプロジェクトが提供するプラグインを指定
できる。

詳しくは、:ref:`setuptools` ドキュメントの `Dynamic Discovery of
Services and Plugins
<https://setuptools.readthedocs.io/en/latest/setuptools.html#dynamic-discovery-of-services-and-plugins>`_
セクションを見よ。

最もよく使われるエントリポイントは "console_scripts" だ(下記参照)。

.. _`console_scripts`:

console_scripts
***************

::

  entry_points={
      'console_scripts': [
          'sample=sample:main',
      ],
  },

スクリプトインターフェースを登録するには、"console_script"
`エントリポイント
<https://setuptools.readthedocs.io/en/latest/setuptools.html#dynamic-discovery-of-services-and-plugins>`_
を使う。これらのインターフェースを実際のスクリプトに変換する作業はツー
ルチェインが行ってくれる。[2]_ スクリプトは :term:`distribution
<Distribution Package>` のインストール中に生成される。

詳しくは、 `setuptools ドキュメント
<https://setuptools.readthedocs.io>`_ の `Automatic Script Creation
<https://setuptools.readthedocs.io/en/latest/setuptools.html#automatic-script-creation>`_
を見よ。

.. _`Choosing a versioning scheme`:

Versioning scheme の選択
------------------------

相互運用性のための標準準拠
~~~~~~~~~~~~~~~~~~~~~~~~~~

個々の Python プロジェクトは固有のニーズに基づいて異なる versioning
scheme を採用してよいが、それら全ては :pep:`440` で指定された
:pep:`public version scheme <440#public-version-identifiers>` に適合し
ていなければならない。これは ``pip`` や ``setuptools`` のようなツール/
ライブラリのサポートを得るためだ。

標準準拠バージョン番号の例をいくつか示す::

  1.2.0.dev1  # Development release
  1.2.0a1     # Alpha Release
  1.2.0b1     # Beta Release
  1.2.0rc1    # Release Candidate
  1.2.0       # Final Release
  1.2.0.post1 # Post Release
  15.10       # Date based release
  23          # Serial release

バージョン番号を付けるアプローチには歴史的なバリエーションがあり、これ
らによりよく対応するため、:pep:`440` は包括的な :pep:`バージョン正規化
<440#normalization>` 手法も定義している。これは個々のバージョン番号の
様々な書式を標準化された正規形にマップするものだ。

Scheme の選択肢
~~~~~~~~~~~~~~~

Semantic versioning (推奨)
**************************

新規プロジェクトでは、 `Semantic Versioning <http://semver.org>`_ に基
づく versioning scheme を推奨する。ただし、プレリリースとビルドメタ
データを扱う際は異なるアプローチが採用されている。

The essence of semantic versioning is a 3-part MAJOR.MINOR.MAINTENANCE numbering scheme,
where the project author increments:

Semantic versioning の本質は MAJOR.MINOR.MAINTENANCE の 3 パートからな
る番号付けであり、プロジェクト作者は以下の場合にそれぞれの番号をインク
リメントする:

1. MAJOR バージョンは、非互換な API 変更を行ったとき。
2. MINOR バージョンは、後方互換性のある機能追加を行ったとき。
3. MAINTENANCE バージョンは、後方互換性のあるバグ修正を行ったとき。

プロジェクト作者がこのアプローチを採用していれば、ユーザは
:pep:`"compatible release" <440#compatible-release>` specifier を利用できる。例えば
``name ~= X.Y`` とすることで、少なくともリリース X.Y が必要だが、後続
のリリースのうち MAJOR バージョンが一致する任意のものを許す、という指
定ができる。

Semantic versioning を採用する Python プロジェクトは、 `Semantic
Versioning 2.0.0 specification <http://semver.org>`_ の 1-8 項に従うべ
きだ。

Date based versioning
*********************

Semantic versioning は全てのプロジェクトに適した選択肢というわけではな
い。例えば、定期的な日時ベースのリリースサイクルを持つものや、機能を削
除するまでのリリース数を警告として提示する機能廃止プロセスを持つものに
は適さない。

Date based versioning の主な利点は、特定リリースの基本機能セットがどの
程度古いものかがバージョン番号を見ただけですぐわかることだ。

典型的な Date based プロジェクトのバージョン番号は YEAR.MONTH の形だ
(例えば、 ``12.04``, ``15.10``)。

Serial versioning
*****************

これは最も単純な versioning scheme であり、リリースごとにインクリメン
トされる単一の番号から成る。

Serial versioning は開発者にとっては管理が非常に容易だが、エンドユーザ
にとっては最も追跡しにくいものだ。なぜなら、serial version number は
API の後方互換性に関する情報をほとんど、または全く伝えないからだ。

Hybrid schemes
**************

上で挙げたものを組み合わせることも考えられる。例えば、date based
versioning と serial versioning を組み合わせて YEAR.SERIAL という方式
を作ることもできる。これはおおよそのリリース時期が容易にわかるが、年内
の特定のリリースサイクルでコミットするわけではない。

Pre-release versioning
~~~~~~~~~~~~~~~~~~~~~~

基本となる versioning scheme がどうであれ、ある最終リリースに対するプ
レリリースは以下のように公開される:

* 0 以上の dev リリース (".devN" サフィックスで示す)
* 0 以上の alpha リリース (".aN" サフィックスで示す)
* 0 以上の beta リリース (".bN" サフィックスで示す)
* 0 以上の release candidates (".rcN" サフィックスで示す)

``pip`` とその他のモダンな Python パッケージインストーラは、依存パッ
ケージをインストールする際はデフォルトでプレリリースを無視する。


Local version identifiers
~~~~~~~~~~~~~~~~~~~~~~~~~

Public version identifiers は、
:term:`PyPI <Python Package Index (PyPI)>` 経由での配布をサポートする
ために設計されたものだ。Python のソフトウェア配布ツールは、:pep:`local
version identifier <440#local-version-identifiers>` の概念もサポートし
ている。これは公開予定のないローカル開発ビルドや、再配布者によりメンテ
ナンスされる修正リリースを識別するのに使われる。

Local version identifier は
``<public version identifier>+<local version label>`` の形になる。例え
ば::

   1.2.0.dev1+hg.5.b11e5e6f0b0b  # 5th VCS commmit since 1.2.0.dev1 release
   1.2.1+fedora.4                # Package with downstream Fedora patches applied


「開発モード」での作業
======================

必須ではないが、作業中のプロジェクトを "editable" または "develop" と
呼ばれるモードでローカルにインストールするのが一般的だ。これにより、イ
ンストールしたプロジェクトをそのまま編集できる。

今プロジェクトのルートディレクトリにいるとしよう。以下を実行する:

::

 pip install -e .


いくぶん暗号的だが、 ``-e`` は ``--editable`` の短縮形で、 ``.`` はカ
レントディレクトリを指す。つまり、カレントディレクトリ(プロジェクト)を
editable モードでインストールするという意味だ。これは
"install_requires" で宣言された依存パッケージ、および
"console_scripts" で宣言されたスクリプトも全てインストールする。このと
きインストールされる依存パッケージは editable モードにはならない。

依存パッケージも editable モードでインストールしたいというのはよくある
ことだ。例えば、プロジェクトが "foo" と "bar" を必要としているが、
"bar" は VCS から editable モードでインストールしたいとしよう。その場
合、requirements ファイルは以下のように書ける::

  -e .
  -e git+https://somerepo/bar.git#egg=bar

1 行目はプロジェクトと依存パッケージ全てをインストールすると宣言してい
る。2 行目は依存パッケージ "bar" を PyPI からではなく VCS から取得する
ようにオーバーライドしている。Requirements ファイルの詳細は、pip ド
キュメントの :ref:`Requirements File <pip:Requirements Files>` セク
ションを見よ。VCS インストールの詳細は、pip ドキュメントの :ref:`VCS
Support <pip:VCS Support>` セクションを見よ。

最後に、依存パッケージを何もインストールしたくないなら、以下を実行する::

   pip install -e . --no-deps


詳しくは、 `setuptools ドキュメント
<https://setuptools.readthedocs.io>`_ の `Development Mode
<https://setuptools.readthedocs.io/en/latest/setuptools.html#development-mode>`_
を見よ。

.. _`Packaging Your Project`:

プロジェクトのパッケージング
============================

プロジェクトを :term:`PyPI <Python Package Index (PyPI)>` のような
:term:`Package Index` からインストール可能にするには、プロジェクトの
:term:`Distribution <Distribution Package>` (:term:`パッケージ
<Distribution Package>`)を作る必要がある。



Source Distributions
--------------------

最低でも、:term:`Source Distribution <Source Distribution (or
"sdist")>` は作る必要がある:

::

 python setup.py sdist


"Source distribution" はビルドされていない(つまり、:term:`Built
Distribution` ではない)。これを pip でインストールする際はビルドのス
テップが必要だ。たとえ distribution が pure Python (一切の拡張を含まな
い)であっても、 ``setup.py`` からインストールメタデータをビルドするス
テップが必要となる。


Wheels
------

プロジェクトの wheel も作るべきだ。Wheel は :term:`ビルド済みパッケー
ジ <Built Distribution>` であり、インストールに「ビルド」プロセスを必
要としない。Wheel があると、エンドユーザは source distribution より
ずっと高速にインストールができる。

プロジェクトが pure Python (一切のコンパイル済み拡張を含まない)で、
Python 2 と 3 の両方をネイティブにサポートするなら、:ref:`"Universal
Wheel" (以下のセクションを参照) <Universal Wheels>` と呼ばれるものを作
ることになる。

プロジェクトが pure Python で、Python 2 と 3 の片方しかネイティブにサ
ポートしないなら、:ref:`"Pure Python Wheel (以下のセクションを参照)
<Pure Python Wheels>` を作ることになる。

プロジェクトがコンパイル済み拡張を含むなら、:ref:`"Platform Wheel" (以
下のセクションを参照) <Platform Wheels>` と呼ばれるものを作ることにな
る。


.. _`Universal Wheels`:

Universal Wheels
~~~~~~~~~~~~~~~~

"Universal Wheels" は pure Python (一切のコンパイル済み拡張を含まない)
かつ Python 2 と 3 をサポートする wheels だ。この wheel はどの環境でも
:ref:`pip` でインストールできる。

Universal Wheel をビルドするには:

::

 python setup.py bdist_wheel --universal


"setup.cfg" で ``--universal`` フラグを恒久的に設定することもできる(サ
ンプル: `sampleproject/setup.cfg
<https://github.com/pypa/sampleproject/blob/master/setup.cfg>`_)

::

 [bdist_wheel]
 universal=1


``--universal`` 設定は以下の場合のみ使うこと:

1. プロジェクトが一切の修正なしで(つまり、2to3 を必要とせず) Python 2
   と 3 で動く
2. プロジェクトが C 拡張を一切含まない。

今のところ、 ``bdist_whell`` はこの設定が不適切に使われていても警告を
出さないので注意。

プロジェクトがオプションの C 拡張を含むなら、universal wheel を公開す
ることは勧められない。というのは、pip は source installation より
wheel を優先するため、拡張をビルドしなくなるからだ。


.. _`Pure Python Wheels`:

Pure Python Wheels
~~~~~~~~~~~~~~~~~~

"Universal" でない "Pure Python Wheels" は、pure Python (一切のコンパ
イル済み拡張を含まない)かつ Python 2 と 3 の片方しかネイティブにサポー
トしない whells だ。

この wheel をビルドするには:

::

 python setup.py bdist_wheel


`bdist_wheel` はコードが pure Python であることを検出し、ビルドに使っ
たのと同じメジャーバージョン (Python 2 または Python 3)の Python 環境
で使えるように名付けられた wheel を作る。Wheelファイルの命名の詳細は、
:pep:`425` を見よ。

コードが Python 2 と 3 の両方をサポートするが、それが異なったコードに
よる(例えば、 `"2to3" <https://docs.python.org/2/library/2to3.html>`_
を使っている)場合は、 ``setup.py bdist_wheel`` を 2 回(Python 2, 3 用
に 1 回ずつ)実行できる。これでそれぞれのバージョン用の wheels が生成さ
れる。


.. _`Platform Wheels`:

Platform Wheels
~~~~~~~~~~~~~~~

"Platform Wheels" は Linux, OSX, Windows といったプラットフォーム固有
の wheels だ。これは普通、コンパイル済み拡張を含むためにそうなってい
る。

この wheel をビルドするには:

::

 python setup.py bdist_wheel


`bdist_wheel` はコードが pure Python でないことを検出し、ビルドされた
プラットフォームでのみ使えるように名付けられた wheel を作る。Wheel
ファイルの命名の詳細は、:pep:`425` を見よ。

.. note::

  :term:`PyPI <Python Package Index (PyPI)>` は今のところ Windows と
  OS X 向けの platform wheels のみアップロードを許可しており、Linux は
  許可して「いない」。今のところ、wheel tag specification (:pep:`425`)
  は Linux ディストリビューション間の多様性を扱わない。


.. _`Uploading your Project to PyPI`:

PyPI へのプロジェクトのアップロード
===================================

.. note::

  メインの PyPI リポジトリへリリースする前に、 `PyPI テストサイト
  <https://testpypi.python.org/pypi>`_ で練習することを勧める。このテ
  ストサイトは半定期的にクリーンアップされる。テストサイトを使うための
  設定については、 `この説明 <https://wiki.python.org/moin/TestPyPI>`_
  を見よ。

Distribution を作るコマンドを実行すると、プロジェクトのルートディレク
トリ下に新規ディレクトリ dist/ が作られる。ここにアップロードすべき
distribution ファイルがある。

アカウント作成
--------------

まず、:term:`PyPI <Python Package Index (PyPI)>` のユーザアカウントが
必要だ。これには 2 つの方法がある:

1. `PyPI ウェブサイトのフォームを使って
   <https://pypi.python.org/pypi?%3Aaction=register_form>`_ 手動でアカ
   ウントを作る。

2. **(非推奨):** 最初のプロジェクトを登録するついでにアカウントを作る
   (セキュリティ上の理由で推奨されない。次のセクションの方法 #3 を見よ)。

方法 #1 (フォーム)でアカウントを作った場合、 ``~/.pypirc`` ファイルを
以下のように書く必要がある:

   ::

    [distutils]
    index-servers=pypi

    [pypi]
    repository = https://upload.pypi.org/legacy/
    username = <username>
    password = <password>

パスワード行は省略してもよい。twine に ``-p PASSWORD`` 引数を渡すか、
単に要求されたときにパスワードを入力すればよい。


プロジェクトの登録
------------------

次に、これが最初のリリースの場合、アップロードする前にプロジェクトを明
示的に登録する必要がある(今のところ)。

これには 3 つの方法がある:

1. `PyPI ウェブサイトのフォーム
   <https://pypi.python.org/pypi?%3Aaction=submit_form>`_ を使い、
   ローカルのプロジェクトツリーの ``myproject.egg-info/PKG-INFO`` にあ
   る ``PKG-INFO`` をアップロードする。このファイルまたはディレクトリ
   がない場合は、 ``python setup.py egg_info`` を実行すれば生成され
   る。
2. ``twine register dist/mypkg.whl`` を実行すると、:ref:`twine` が指定
   されたファイル内のパッケージメタデータに基づいてプロジェクトを登録
   する。twine が正しく動くために、予め ``~/.pypirc`` を適切に設定して
   おかなければならない。
3. **(非推奨):** ``python setup.py register`` を実行する。まだユーザア
   カウントがない場合、ウィザードが作成してくれる。ここでこのアプロー
   チを説明するのは他のガイドで言及されているからだが、推奨はしない。
   なぜなら、Python のバージョンによっては平文の HTTP, または検証され
   ていない HTTPS 接続を使う可能性があり、その場合ユーザ名とパスワード
   が傍受できてしまうからだ。


Distributions のアップロード
----------------------------

ついに、:term:`PyPI <Python Package Index (PyPI)>` へ distributions を
アップロードできるようになった。

これには 2 つの方法がある:

1. :ref:`twine` を使う:

   ::

     twine upload dist/*

   twine を使う最大の理由は、 ``python setup.py upload`` (以下の方法
   #2) はファイルを平文でアップロードすることだ。これだと MITM 攻撃で
   ユーザ名とパスワードが盗まれうる。twine は検証された TLS 接続のみを
   使って PyPI へのアップロードを行い、認証情報を盗難から守る。

   次に、twine を使うと distribution ファイルを事前に作っておくことが
   できる。 ``python setup.py upload`` では、同じコマンド呼び出しで
   作ったものしかアップロードできない。これだと、PyPI へのアップロード
   前にそのファイルをテストして正しく動くことを保証することができな
   い。

   最後に、twine を使うと、事前にファイルに署名し、その .asc ファイル
   をコマンドラインで渡せる (``twine upload twine-1.0.1.tar.gz
   twine-1.0.1.tar.gz.asc``)。これにより、パスフレーズを gpg 以外に対
   して入力していないことを保証できる(*あなた* が直接 ``gpg
   --detach-sign -a <filename>`` を実行するのだから)。


2. **(非推奨):** :ref:`setuptools` を使う:

   ::

    python setup.py sdist bdist_wheel upload

   ここでこのアプローチを説明するのは他のガイドで言及されているからだ
   が、推奨はしない。なぜなら、Python のバージョンによっては平文の
   HTTP, または検証されていない HTTPS 接続を使う可能性があり、その場合
   ユーザ名とパスワードが傍受できてしまうからだ。

----

.. [1] プラットフォームによっては、root または管理者権限が必要かもしれ
       ない。:ref:`pip` は現在、 `ユーザ単位のインストールをデフォルト
       とする <https://github.com/pypa/pip/issues/1668>`_ ことでこの状
       況を変えることを検討している。


.. [2] 具体的には、"console_script" アプローチを使うと Windows 上で
       ``.exe`` ファイルを生成できる。これが必要なのは Windows が
       ``.exe`` ファイルを特別扱いするためだ。 ``PATHEXT`` や
       :pep:`Python Launcher for Windows <397>` のようなスクリプト実行
       機能は多くのケースで利用できるが、全てではない。
