========================
パッケージのインストール
========================

:Page Status: Complete
:Last Reviewed: 2016-06-24

このセクションでは、Python :term:`パッケージ <Distribution Package>`
のインストール方法の基本を説明する。

重要な注意: この文脈で「パッケージ」とは、:term:`distribution
<Distribution Package>` (つまり、インストールされるひとかたまりのソフ
トウェア)の同義語であり、Python ソースコード内で import する
:term:`package <Import Package>` (モジュールコンテナ)を指すのではな
い。Python コミュニティでは、:term:`distribution <Distribution
Package>` を表すのに「パッケージ」の語を用いるのが普通だ。
"distribution" という用語はしばしば避けられる。というのは、Linux
distribution だとか、あるいは Python 自身のような他のより大きなソフト
ウェアの distribution と混同しやすいからだ。


.. contents:: Contents
   :local:


.. _installing_requirements:

パッケージインストールの要件
============================

このセクションでは、他の Python パッケージをインストールする前に行うべ
き手順を説明する。

pip, setuptools, wheel をインストールする
-----------------------------------------

* Python 2 の 2.7.9 以上、または Python 3 の 3.4 以上を `python.org
  <https://www.python.org>`_ からインストールした場合、:ref:`pip` と
  :ref:`setuptools` は既に存在する。ただし最新版へのアップグレードが必
  要だ:

  Linux または OS X では:

  ::

    pip install -U pip setuptools

  Windows では:

  ::

    python -m pip install -U pip setuptools

* Linux 上でシステムのパッケージマネージャ("yum", "apt-get" など…)管
  理下の Python 環境を使っており、システムのパッケージマネージャを使っ
  て pip のインストールとアップグレードを行いたいなら、
  :ref:`Installing pip/setuptools/wheel with Linux Package Managers`
  を見よ。

* それ以外の場合:

 * 安全な手段で `get-pip.py <https://bootstrap.pypa.io/get-pip.py>`_
   をダウンロードする。[1]_

 * ``python get-pip.py`` を実行する。[2]_ これは pip のインストールと
   アップグレードを行う。加えて、:ref:`setuptools` と :ref:`wheel` を
   (まだインストールされていなければ)インストールする。

   .. warning::

      オペレーティングシステムまたはその他のパッケージマネージャ管理下
      の Python 環境を使っている場合は注意が必要だ。get-pip.py はそれ
      らのツールとは協調しないので、システムが矛盾した状態になるかもし
      れない。


仮想環境を作る(必要なら)
------------------------

詳細は :ref:`以下のセクション <Creating and using Virtual
Environments>` で述べるが、基本的なコマンドはこうだ:

   :ref:`virtualenv` を使う場合:

   ::

    pip install virtualenv
    virtualenv <DIR>
    source <DIR>/bin/activate

   `venv`_ を使う場合: [3]_

   ::

    python3 -m venv <DIR>
    source <DIR>/bin/activate


.. _`Creating and using Virtual Environments`:

仮想環境の作成
==============

Python「仮想環境」は、Python :term:`パッケージ <Distribution Package>`
をグローバルにではなくアプリケーション固有の隔離された場所にインストー
ルできるようにする。

あるアプリケーションで LibFoo バージョン 1 が必要だが、別のアプリケー
ションではバージョン 2 が必要だとしよう。これらのアプリケーションを併
用するにはどうしたらよいか?もし何もかもを
/usr/lib/python2.7/site-packages (またはプラットフォーム標準の場所)に
インストールしていると、アップグレードすべきでないアプリケーションを意
図せずアップグレードしてしまう状況が容易に起こりうる。

より一般的な話をすると、インストールしたアプリケーションをそのままの状
態に保ちたい場合はどうか?現在あるアプリケーションがうまく動いていて
も、それが利用するライブラリが変わったり、ライブラリのバージョンが変
わったりすると、そのアプリケーションが壊れる可能性がある。

また、:term:`パッケージ <Distribution Package>` をグローバルな
site-package ディレクトリにインストールできない場合はどうか?共用ホスト
がその例だ。

仮想環境はこれら全てのケースで役立つ。仮想環境はそれ自身のインストール
ディレクトリを持ち、他の仮想環境とライブラリを共有しない。

現在、Python 仮想環境を作るために 2 つのツールが利用できる:

* `venv`_ は Python 3.3 以降でデフォルトで利用できる。Python 3.4 以降
  では、仮想環境作成時に :ref:`pip` と :ref:`setuptools` のインストー
  ルも行う。
* :ref:`virtualenv` は Python とは別にインストールする必要があるが、
  Python 2.6+ と Python 3.3+ の両方をサポートする。また、仮想環境作成
  時に :ref:`pip`, :ref:`setuptools`, :ref:`wheel` が常にインストール
  される(Python のバージョンによらず)。

基本的な使い方はこうだ:

:ref:`virtualenv` を使う場合:

::

 virtualenv <DIR>
 source <DIR>/bin/activate


`venv`_ を使う場合:

::

 python3 -m venv <DIR>
 source <DIR>/bin/activate


詳細は `virtualenv <http://virtualenv.pypa.io>`_, `venv`_ のドキュメン
トを見よ。


インストールには pip を使う
===========================

:ref:`pip` は推奨インストーラだ。以下では、最も一般的な使い方について
説明する。詳細については、完全な `リファレンスガイド
<https://pip.pypa.io/en/latest/reference/index.html>`_ を含む `pip ド
キュメント <https://pip.pypa.io>`_ を見よ。

まれなケースだが、pip の代わりに `easy_install
<https://pip.pypa.io/en/latest/reference/index.html>`_ を使いたくなる
ことがあるかもしれない。詳しくは、:doc:`追加トピック <additional>` の
:ref:`pip vs easy_install` の解説を見よ。


PyPI からのインストール
=======================

:ref:`pip` の最も一般的な用途は、:term:`requirement specifier
<Requirement Specifier>` を指定して :term:`Python Package Index
<Python Package Index (PyPI)>` からのインストールを行うことだ。大まか
に言うと、requirement specifier はプロジェクト名とそれに続くオプション
の :term:`version specifier <Version Specifier>` から成る。:pep:`440`
に現在サポートされる specifier の :pep:`完全な仕様
<440#version-specifiers>` がある。以下にいくつかの例を示す。

"SomeProject" の最新バージョンをインストール:

::

 pip install 'SomeProject'


特定のバージョンをインストール:

::

 pip install 'SomeProject==1.4'


あるバージョン以上、あるバージョン未満のものをインストール:

::

 pip install 'SomeProject>=1,<2'


特定のバージョンと :pep:`「互換」 <440#compatible-release>` なバージョ
ンをインストール: [4]_

::

 pip install 'SomeProject~=1.4.2'

この場合、"==1.4.*" かつ ">=1.4.2" である任意のバージョンがインストー
ルされる。


Source Distributions vs Wheels
==============================

:ref:`pip` は :term:`Source Distributions (sdist) <Source Distribution
(or "sdist")>`, :term:`Wheels <Wheel>` のいずれからのインストールも行
えるが、PyPI にその両方が存在する場合、pip は互換性のある :term:`wheel
<Wheel>` を優先する。

:term:`Wheels <Wheel>` は事前ビルドされた :term:`distribution
<Distribution Package>` フォーマットであり、:term:`Source
Distributions (sdist) <Source Distribution (or "sdist")>` より高速にイ
ンストールできる。プロジェクトがコンパイル済み拡張を含む場合は特に速
い。

インストール時に wheel が見つからない場合、:ref:`pip` はローカルに
wheel をビルドし、それを今後のインストール用にキャッシュする。これによ
り、今後 source distribution をリビルドする必要がなくなる。


パッケージのアップグレード
==========================

インストール済みの `SomeProject` を PyPI の最新版にアップグレード:

::

 pip install --upgrade SomeProject



ユーザディレクトリへのインストール
==================================

:term:`パッケージ <Distribution Package>` を現在のユーザ専用にインス
トールするには、 ``--user`` フラグを使う:

::

  pip install --user SomeProject


詳しくは、pip ドキュメントの `User Installs
<https://pip.readthedocs.org/en/latest/user_guide.html#user-installs>`_
セクションを見よ。


Requirements files
==================

:ref:`Requirements File <pip:Requirements Files>` で指定された必要な
パッケージをまとめてインストール:

::

 pip install -r requirements.txt


VCS からのインストール
======================

VCS から "editable" モードでプロジェクトをインストールできる。構文の完
全な解説は、pip の :ref:`VCS Support <pip:VCS Support>` セクションを見
よ。

::

 pip install -e git+https://git.repo/some_pkg.git#egg=SomeProject          # from git
 pip install -e hg+https://hg.repo/some_pkg.git#egg=SomeProject            # from mercurial
 pip install -e svn+svn://svn.repo/some_pkg/trunk/#egg=SomeProject         # from svn
 pip install -e git+https://git.repo/some_pkg.git@feature#egg=SomeProject  # from a branch


PyPI 以外のインデックスからのインストール
=========================================

代替インデックスからインストール:

::

 pip install --index-url http://my.package.repo/simple/ SomeProject


インストール中に :term:`PyPI <Python Package Index (PyPI)>` の他に追加
のインデックスも検索:

::

 pip install --extra-index-url http://my.package.repo/simple SomeProject



ローカルソースツリーからのインストール
======================================


ローカルのソースから `開発モード
<https://setuptools.readthedocs.io/en/latest/setuptools.html#development-mode>`_
でインストール(プロジェクトはインストールされたように見えるが、ソース
ツリーから編集可能なままになる):

::

 pip install -e <path>


ソースから通常のインストールも可能:

::

 pip install <path>


ローカルアーカイブからのインストール
====================================

特定のローカルアーカイブファイルからインストール:

::

 pip install ./downloads/SomeProject-1.0.4.tar.gz


アーカイブ群を含むローカルディレクトリからインストール(:term:`PyPI
<Python Package Index (PyPI)>` は無視):

::

 pip install --no-index --find-links=file:///local/dir/ SomeProject
 pip install --no-index --find-links=/local/dir/ SomeProject
 pip install --no-index --find-links=relative/dir/ SomeProject



プレリリースのインストール
==========================

安定版に加え、プレリリースおよび開発版も探す(デフォルトでは、pip は安
定版のみを探す):

::

 pip install --pre SomeProject


Setuptools "Extras" のインストール
==================================

`setuptools extras`_ をインストール:

::

  $ pip install SomePackage[PDF]
  $ pip install SomePackage[PDF]==3.0
  $ pip install -e .[PDF]==3.0  # editable project in current directory



----

.. [1] この文脈で「安全」とは、モダンブラウザや `curl` のようなツール
       を使い、https URL からのダウンロード時に SSL 証明書を検証するこ
       とを指す。

.. [2] プラットフォームによっては、root または管理者権限が必要かもしれ
       ない。:ref:`pip` は現在、 `ユーザ単位のインストールをデフォルト
       とする <https://github.com/pypa/pip/issues/1668>`_ ことでこの状
       況を変えることを検討している。

.. [3] Python 3.4 から、 ``venv`` (:ref:`virtualenv` の標準ライブラリ
       版)は ``pip`` がインストールされた仮想環境を作るので、
       :ref:`virtualenv` と同等になる。

.. [4] この compatible release specifier は :pep:`440` で accept さ
       れ、:ref:`setuptools` v8.0, :ref:`pip` v6.0 でサポートされた。

.. _venv: https://docs.python.org/3/library/venv.html
.. _setuptools extras: http://setuptools.readthedocs.io/en/latest/setuptools.html#declaring-extras-optional-features-with-their-own-dependencies
