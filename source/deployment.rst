
==========================
アプリケーションのデプロイ
==========================

:Page Status: Incomplete
:Last Reviewed: 2014-11-11

.. contents:: Contents
   :local:


Overview
========


Supporting multiple hardware platforms
--------------------------------------

::

  FIXME

  Meaning: x86, x64, ARM, others?

  For Python-only distributions, it *should* be straightforward to deploy on all
  platforms where Python can run.

  For distributions with binary extensions, deployment is major headache.  Not only
  must the extensions be built on all the combinations of operating system and
  hardware platform, but they must also be tested, preferably on continuous
  integration platforms.  The issues are similar to the "multiple python
  versions" section above, not sure whether this should be a separate section.
  Even on Windows x64, both the 32 bit and 64 bit versions of Python enjoy
  significant usage.



OS Packaging & Installers
=========================

::

  FIXME

  - Building rpm/debs for projects
  - Building rpms/debs for whole virtualenvs
  - Building Mac OS X installers for Python projects
  - Building Android APKs with Kivy+P4A or P4A & Buildozer

Windows
-------

::

  FIXME

  - Building Windows installers for Python projects

Pynsist
^^^^^^^

`Pynsist <https://pypi.python.org/pypi/pynsist>`__ は、Python プログラ
ムに Python インタプリタをバンドルして NSIS ベースの単一インストーラを
作るツールだ。ほとんどの場合、ユーザは Python インタプリタのバージョン
選択とプログラムの依存関係の宣言を行うだけでパッケージングができる。こ
のツールは指定された Windows 用 Python インタプリタをダウンロードし、
全ての依存関係と一緒に単一の Windows-executable インストーラへパッケー
ジする。

できあがったインストーラはユーザのシステムに Python インタプリタをイン
ストールするか、または更新する。このインタプリタはパッケージされたプロ
グラムとは独立して使える。プログラム自体はインストーラがスタートメ
ニューに配置するショートカットから起動できる。プログラムをアンインス
トールしても、ユーザの Python 環境はそのまま残る。

Pynsist の大きな利点は、Linux 上で Windows パッケージが作れることだ。
`ドキュメント <http://pynsist.readthedocs.org>`__ に各種プログラム(コ
ンソール、GUI) の例がいくつかある。このツールは MIT ライセンスでリリー
スされている。

Application Bundles
===================

::

  FIXME

  - py2exe/py2app/PEX
  - wheels kinda/sorta


Configuration Management
========================

::

  FIXME

  puppet
  salt
  chef
  ansible
  fabric
