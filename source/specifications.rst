
.. _specifications:

=========
PyPA 仕様
=========

:Page Status: Complete
:Last Reviewed: 2016-01-22

Python Packaging Authority が管理している現在アクティブな相互運用性に
関する仕様のリストを示す。

Package distribution metadata
#############################

Core metadata
=============

現在の core metadata ファイルフォーマット バージョン 1.2 の仕様は
:pep:`345` にある。

しかし、当該 PEP の version specifiers および environment markers セク
ションについては他の PEP が優先される(後述)。さらに、メタデータファイ
ルは以下の追加フィールドを含んでもよい:

Provides-Extra (複数可)
~~~~~~~~~~~~~~~~~~~~~~~

オプション機能の名前を含む文字列。有効な Python 識別子でなければならな
い。オプション機能が要求されたかどうかによって条件付き依存関係を記述す
るのに使える。

例::

    Provides-Extra: pdf
    Requires-Dist: reportlab; extra == 'pdf'

角括弧で囲むことでオプションの依存関係を要求でき、カンマで区切ることで
複数指定することもできる。要求された各機能について要件が評価され、
distribution の要件セットに追加される。

Example::

    Requires-Dist: beaglevote[pdf]
    Requires-Dist: libexample[test, doc]

機能名 `test` と `doc` は予約されており、それぞれ自動テストとドキュメ
ント生成が必要であるとマークするのに使われる。

``Requires-Dist:`` で参照されない ``Provides-Extra:`` を指定するのは合
法だ。


Version Specifiers
==================

バージョン番号の要件、およびバージョン間の比較指定のセマンティクスは
:pep:`440` で定義されている。

この PEP の version specifiers セクションは :pep:`345` の version
specifiers セクションに優先する。

Dependency Specifiers
=====================

他のコンポーネントへの依存関係を宣言するための dependency specifier
フォーマットは :pep:`508` で定義されている。

この PEP の environment markers セクションは :pep:`345` の environment
markers セクションに優先する。

Source Distribution Format
==========================

Source distribution 形式 (``sdist``) には今のところ正式な定義がない。
代わりに、その形式は ``setup.py sdist`` コマンドを実行した際の標準ライ
ブラリの ``distutils`` モジュールの動作によって暗黙に定義される。

Binary Distribution Format
==========================

Binary distribution format (``wheel``) は :pep:`427` で定義されてい
る。

Platform Compatibility Tags
===========================

``Wheel`` distribution で使われる platform compatibility tagging model
は :pep:`425` で定義されている。

当該 PEP で定義されるスキームは Linux (一般には \*nix) 用 wheel のパブ
リックな配布のためには不十分なので、:pep:`513` が作られ、
``manylinux1`` タグが定義された。

インストール済み distribution の記録
====================================

インストール済みパッケージとその内容を記録するためのフォーマットは
:pep:`376` で定義されている。

デフォルトのパッケージングツールチェインは、今のところ当該 PEP のうち
``dist-info`` ディレクトリと ``RECORD`` ファイル形式のみを実装してい
る。


Package index interfaces
########################

Simple repository API
=====================

インデックスサーバにパッケージバージョンを問い合わせ、パッケージを取得
するためのインターフェースは :pep:`503` で定義されている。
