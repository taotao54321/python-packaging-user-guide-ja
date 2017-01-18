
.. _projects:

================
プロジェクト概要
================

:Page Status: Complete
:Last Reviewed: 2016-06-24

Python インストールおよびパッケージングに関する最も重要なプロジェクト
群の概要とリンクを示す。

.. _pypa_projects:

PyPA 内のプロジェクト
#####################

.. _bandersnatch:

bandersnatch
============

`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bitbucket.org/pypa/bandersnatch/issues?status=new&status=open>`__ |
`Bitbucket <https://bitbucket.org/pypa/bandersnatch>`__ |
`PyPI <https://pypi.python.org/pypi/bandersnatch>`__

bandersnatch は PyPI ミラーリングクライアントだ。PyPI コンテンツを完全
かつ効率的にミラーリングするよう設計されている。


.. _distlib:

distlib
=======

`Docs <http://pythonhosted.org/distlib/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bitbucket.org/pypa/distlib/issues?status=new&status=open>`__ |
`Bitbucket <https://bitbucket.org/pypa/distlib>`__ |
`PyPI <https://pypi.python.org/pypi/distlib>`__

distlib は Python ソフトウェアのパッケージングと配布に関する低レベル機
能を実装するライブラリだ。これは `distutils2
<https://pypi.python.org/pypi/Distutils2>`_ プロジェクトの一部からな
る。distutils2 は Python 3.3 標準ライブラリで ``packaging`` としてリ
リースされる予定だったが、Python 3.3 がベータテストに入る直前に削除さ
れた。


.. _packaging:

packaging
=========

`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/packaging/issues>`__ |
`Github <https://github.com/pypa/packaging>`__ |
`PyPI <https://pypi.python.org/pypi/packaging>`__ |
User irc:#pypa |
Dev irc:#pypa-dev

:ref:`pip` と :ref:`setuptools` が利用する Python パッケージング用のコ
アユーティリティ。


.. _pip:

pip
===

`Docs <https://pip.pypa.io/en/stable/>`__ |
`User list <http://groups.google.com/group/python-virtualenv>`__ [1]_ |
`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/pip/issues>`__ |
`Github <https://github.com/pypa/pip>`__ |
`PyPI <https://pypi.python.org/pypi/pip/>`__ |
User irc:#pypa |
Dev irc:#pypa-dev

Python パッケージをインストールするツール。


Python Packaging User Guide
===========================

`Docs <https://packaging.python.org/en/latest/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ |
`Issues <https://github.com/pypa/python-packaging-user-guide/issues>`__ |
`Github <https://github.com/pypa/python-packaging-user-guide>`__ |
User irc:#pypa |
Dev irc:#pypa-dev

このガイド!


.. _setuptools:
.. _easy_install:

setuptools
==========

`Docs <https://setuptools.readthedocs.io/en/latest/>`__ |
`User list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/setuptools/issues>`__ |
`GitHub <https://github.com/pypa/setuptools>`__ |
`PyPI <https://pypi.python.org/pypi/setuptools>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev


setuptools (``easy_install`` を含む)は Python distutils の強化版で、
Python distributions, 特に他のパッケージに依存するものをより簡単にビル
ド/配布できるようにする。

`distribute`_ は setuptools の fork だったが、v0.7 で setuptools に再
度マージされた。これにより、setuptools が Python パッケージングの第一
の選択肢となった。


.. _twine:

twine
=====

`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://github.com/pypa/twine/issues>`__ |
`Github <https://github.com/pypa/twine>`__ |
`PyPI <https://pypi.python.org/pypi/twine>`__

Twine は PyPI とやりとりするユーティリティで、 ``setup.py upload`` の
安全な代替となる。



.. _virtualenv:

virtualenv
==========

`Docs <https://virtualenv.pypa.io/en/stable/>`__ |
`User list <http://groups.google.com/group/python-virtualenv>`__ |
`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/virtualenv/issues>`__ |
`Github <https://github.com/pypa/virtualenv>`__ |
`PyPI <https://pypi.python.org/pypi/virtualenv/>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev

隔離された Python 環境を作るツール。


.. _warehouse:

Warehouse
=========

`Docs <https://warehouse.pypa.io/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://github.com/pypa/warehouse/issues>`__ |
`Github <https://github.com/pypa/warehouse>`__ |
Dev irc:#pypa-dev


新しい未リリースの PyPI アプリケーション。
https://warehouse.python.org/ でプレビューできる。


.. _wheel:

wheel
=====

`Docs <http://wheel.readthedocs.io/en/latest/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bitbucket.org/pypa/wheel/issues?status=new&status=open>`__ |
`Bitbucket <https://bitbucket.org/pypa/wheel>`__ |
`PyPI <https://pypi.python.org/pypi/wheel>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev


主に、wheel プロジェクトは :term:`wheel distributions <Wheel>` を作る
ための :ref:`setuptools` ``bdist_wheel`` 拡張を提供する。加えて、wheel
の作成とインストールを行う独自のコマンドラインユーティリティも提供す
る。


PyPA 外のプロジェクト
#####################

.. _bento:

bento
=====

`Docs <http://cournape.github.io/Bento/>`__ |
`Mailing list <http://librelist.com/browser/bento>`__ |
`Issues <https://github.com/cournape/Bento/issues>`__ |
`Github <https://github.com/cournape/Bento>`__ |
`PyPI <https://pypi.python.org/pypi/bento>`__

Bento は Python ソフトウェアのためのパッケージングソリューションで、
distutils, setuptools, distribute などの代替を目指している。Bento の哲
学は再現性、拡張性、簡潔さだ(この順で)。

.. _buildout:

buildout
========

`Docs <http://www.buildout.org/en/latest/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bugs.launchpad.net/zc.buildout>`__ |
`PyPI <https://pypi.python.org/pypi/zc.buildout>`__ |
irc:#buildout

buildout は Python ベースのビルドシステムで、複数のパーツ(非 Python
ベースでもよい)からアプリケーションを作成、アセンブル、デプロイでき
る。buildout 構成を作り、後で同じソフトウェアを再現できるようにする。

.. _conda:

conda
=====

`Docs <http://conda.pydata.org/docs/>`__

Conda は `Anaconda <http://docs.continuum.io/anaconda/index.html>`__
Python 環境用のパッケージ管理ツールだ。Anaconda Python は `Continuum
Analytics <http://continuum.io/downloads>`__ によるディストリビュー
ションで、科学コミュニティ(特にバイナリ拡張のインストールが難しくなり
がちな Windows環境)向けに特化している。

Conda は pip, virtualenv, wheel とは完全に別のツールだが、これらを組み
合わせたような機能(パッケージ管理、仮想環境管理、バイナリ拡張のデプロ
イ)を提供する。

Conda はパッケージを PyPI からインストールせず、Continuum 公式リポジト
リ, anaconda.org (ユーザが作成した *conda* パッケージの置き場), または
ローカル(例:イントラネット)パッケージサーバからのみインストールを行
う。ただし、pip をインストールすることもでき、pip は conda とは独立し
て PyPI 由来の distributions を管理する。


devpi
=====

`Docs <http://doc.devpi.net/latest/>`__ |
`Mailing List <https://groups.google.com/forum/#!forum/devpi-dev>`__ |
`Issues <https://bitbucket.org/hpk42/devpi/issues>`__ |
`PyPI <https://pypi.python.org/pypi/devpi>`__

devpi には強力な PyPI 互換サーバと PyPI プロキシキャッシュがあり、
Python でパッケージング、テスト、リリース活動を行うためのコマンドライ
ンツールが付属する。


.. _hashdist:

Hashdist
========

`Docs <http://hashdist.readthedocs.org/en/latest/>`__ |
`Github <https://github.com/hashdist/hashdist/>`__

Hashdist は non-root ソフトウェアディストリビューションを構築するライ
ブラリだ。Hashdist は「Debian の技術がうまくいかない場合に選ぶ
Debian」であろうとしている。Pythonista にとっての Hashdist のベストな
見方は、virtualenv と buildout のより強力なハイブリッドかもしれない。

.. _pex:

pex
===

`Docs <http://pex.readthedocs.org/en/latest/>`__ |
`Github <https://github.com/pantsbuild/pex/>`__ |
`PyPI <https://pypi.python.org/pypi/pex>`__

pex は ``.pex`` (Python EXecutable) を生成するライブラリおよびツールで
あり、同時に :ref:`virtualenv` の精神に基づくスタンドアロン Python 環
境でもある。 ``.pex`` ファイルは単なる zip ファイルで、
``#!/usr/bin/env python`` および特別な ``__main__.py`` を持ち、Python
アプリケーションのデプロイが ``cp`` と同じくらいシンプルにできるよう注
意深く構築されている。

.. _spack:

Spack
=====

`Docs <http://software.llnl.gov/spack/>`__ |
`Github <https://github.com/llnl/spack/>`__ |
`Paper <http://www.computer.org/csdl/proceedings/sc/2015/3723/00/2807623.pdf>`__ |
`Slides <https://tgamblin.github.io/files/Gamblin-Spack-SC15-Talk.pdf>`__

柔軟なパッケージマネージャで、複数のバージョン、構成、プラットフォー
ム、コンパイラをサポートするよう設計されている。Spack は homebrew に似
ているが、パッケージは Python で書かれており、またパラメータ化によって
コンパイラ、ライブラリのバージョン、ビルドオプションなどを容易に交換で
きるようになっている。パッケージのバージョンがどれだけ多くても、それら
全てが同じシステム上で共存できる。Spack はクラスタやスーパーコンピュー
タ上で高パフォーマンス科学アプリケーションを迅速に構築するために設計さ
れた。

Spack は PyPI には(まだ)入っていないが、インストールは不要で、github
からクローンしてすぐ使える。


標準ライブラリプロジェクト
##########################

.. _ensurepip:

ensurepip
=========

`Docs <https://docs.python.org/3/library/ensurepip.html>`__ |
`Issues <http://bugs.python.org>`__

既存の Python 環境または仮想環境で :ref:`pip` のブートストラッピングを
サポートする Python 標準ライブラリパッケージ。ほとんどの場合、エンド
ユーザがこのモジュールを使うことはなく、Python ディストリビューション
のビルド中に使われる。


.. _distutils:

distutils
=========

`Docs <https://docs.python.org/3/library/distutils.html>`__ |
`User list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <http://bugs.python.org>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev

:term:`distributions <Distribution Package>` の作成とインストールをサ
ポートする Python 標準ライブラリパッケージ。:ref:`setuptools` が
distutils より強力な機能を提供しているので、distutils を単独で使うより
はそちらを使う方がはるかに一般的だ。


.. _venv:

venv
====

`Docs <https://docs.python.org/3/library/venv.html>`__ |
`Issues <http://bugs.python.org>`__

A package in the Python Standard Library (starting with Python 3.3) for
creating :term:`Virtual Environments <Virtual Environment>`.  For more
information, see the section on :ref:`Creating and using Virtual Environments`.

:term:`仮想環境 <Virtual Environment>` を作るための Python 標準ライブ
ラリパッケージ (Python 3.3 以降)。詳しくは、:ref:`Creating and using
Virtual Environments` のセクションを見よ。

----

.. [1] pip を作ったのは virtualenv と同じ開発者で、早い段階で
       virtualenv メーリングリストを使うことにした。以来ずっとその状態
       が続いている。

.. [2] 複数のプロジェクトが distutils-sig メーリングリストをユーザ用と
       して再利用している。


.. _distribute: https://pypi.python.org/pypi/distribute
