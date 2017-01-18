.. _`install_requires vs Requirements files`:

======================================
install_requires vs Requirements files
======================================

:Page Status: Complete
:Last Reviewed: 2015-09-08

.. contents:: Contents
   :local:


install_requires
----------------

``install_requires`` は :ref:`setuptools` ``setup.py`` のキーワード
で、プロジェクトが正しく動くのに **最低限** 必要なものを指定するのに使
う。:ref:`pip` がプロジェクトをインストールする際、これに従って依存関
係がインストールされる。

例えば、プロジェクトが A と B を必要とするなら、 ``install_requires``
はこのようになる:

::

 install_requires=[
    'A',
    'B'
 ]

加えて、バージョンの下限と上限があればそれを示すのがベストプラクティス
だ。

例えば、プロジェクトが最低でも 'A' の v1, および 'B' の v2 を必要とす
るとわかっているなら、このようにする:

::

 install_requires=[
    'A>=1',
    'B>=2'
 ]

A が semantic versioning を使っており、'A' の v2 が互換性を破っている
こともわかっているなら、v2 を許可しないのは理にかなっている:

::

 install_requires=[
    'A>=1,<2',
    'B>=2'
 ]

``install_requires`` を使って依存関係を特定バージョンに固定したり、サ
ブ依存関係(依存関係のさらに依存関係)を指定するのはベストプラクティスと
はいえない。これは制約が厳しすぎるし、ユーザが依存関係をアップグレード
するのを妨げる。

最後に、 ``install_requires`` は「抽象」requirements のリストであるこ
とを理解するのが重要だ。つまり、名前とバージョンに関する制約を記述する
だけで、その依存関係がどの場所(インデックスやソース)から満たされるかは
指定しないということだ。その場所(「具体化」)はインストール時に
:ref:`pip` オプションを使って決定される。


Requirements files
------------------

:ref:`Requirements Files <pip:Requirements Files>` は、最も簡単に説明
すると、単に :ref:`pip:pip install` への引数リストをファイルに格納した
ものだ。

``install_requires`` はプロジェクト単独の依存関係を定義するが、
:ref:`Requirements Files <pip:Requirements Files>` はしばしば完全な
Python 環境の要件を定義するのに使われる。

``install_requires`` の要件は最小限だが、requirements files は完全な環
境の :ref:`repeatable installations <pip:Repeatability>` を実現するた
めに固定されたバージョンの完全なリストを含むことがしばしばある。

``install_requires`` の要件は「抽象」(つまり、特定のインデックスに関連
付けられていない)だが、requirements files はしばしば ``--index-url``
や ``--find-links`` のような pip オプションを含んでおり、要件を「具体
化」(特定のインデックスやパッケージディレクトリに関連付け)している。
[1]_

``install_requires`` メタデータは pip がインストール中に自動解析する
が、requirements files はそうではない。requirements files が使われるの
は、ユーザが ``pip install -r`` でインストールするときだけだ。

----

.. [1] 「抽象」「具体」要件に関する詳細は、
       https://caremad.io/2013/07/setup-vs-requirement/ を見よ。
