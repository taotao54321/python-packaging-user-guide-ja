
======
用語集
======

:Page Status: Complete
:Last Reviewed: 2015-09-08


.. glossary::


    Binary Distribution

        :term:`Built Distribution` のうち、コンパイル済み拡張を含むも
        の。


    Built Distribution

        :term:`Distribution <Distribution Package>` 形式のうち、中身の
        ファイルとメタデータをターゲットシステムの正しい場所へ移動する
        だけでインストールができるもの。:term:`Wheel` はそのような形式
        だが、distutils の :term:`Source Distribution <Source
        Distribution (or "sdist")>` はそうではない。後者はインストール
        前にビルドステップを要するからだ。この形式は Python ファイルが
        プリコンパイルを要するというわけではない(:term:`Wheel` は意図
        的にコンパイル済み Python ファイルを含めていない)。


    Distribution Package

        バージョン管理されたアーカイブファイルで、Python :term:`パッ
        ケージ <Import Package>` 、:term:`モジュール <module>` 、およ
        びその他のリソースファイルを含む。:term:`Release` の配布に使わ
        れる。エンドユーザがインターネットからダウンロードしてインス
        トールするのはこのアーカイブファイルだ。

        Distribution package は単に「パッケージ」とか "distribution"
        と呼ばれる方が一般的だが、このガイドでは明快さのためにこの長い
        用語を使うこともある。これは :term:`Import Package` (これもよ
        く「パッケージ」と呼ばれる)や、その他の類のディストリビュー
        ション(例えば、Linux ディストリビューションや Python 言語ディ
        ストリビューション。これらにしても単に「ディストリビューショ
        ン」と呼ばれがち)との混同を避けるためだ。

    Egg

        :ref:`setuptools` が導入した :term:`Built Distribution` 形式
        で、:term:`Wheel` に取って代わられた。詳しくは、
        `The Internal Structure of Python Eggs
        <https://setuptools.readthedocs.io/en/latest/formats.html>`_
        および `Python Eggs
        <http://peak.telecommunity.com/DevCenter/PythonEggs>`_ を見
        よ。

    Extension Module

        Python 実装における低レベル言語で書かれた :term:`モジュール
        <module>`: Python の場合 C/C++, Jython の場合 Java。通常、単一
        の動的ロード可能なコンパイル済みファイル内にある(例えば、Unix
        の Python拡張なら共有オブジェクト (.so) ファイル、Windows の
        Python 拡張なら DLL (拡張子 .pyd), Jython 拡張なら Java クラス
        ファイル)。


    Known Good Set (KGS)

        互換性を持つようにバージョン指定された distribution のセット。
        通常、テストスイートが全てのテストを通ってはじめて特定のパッ
        ケージセットが known good set と宣言される。この用語は、複数の
        独立した distribution からなるフレームワークやツールキットでよ
        く使われる。


    Import Package

        他のモジュール、または再帰的に他のパッケージを含む Python モ
        ジュール。

        Import package は単に「パッケージ」と呼ばれる方が一般的だが、
        このガイドでは明快さのためにこの長い用語を使うことがある。これ
        は :term:`Distribution Package` (これもよく「パッケージ」と呼
        ばれる)との混同を避けるためだ。

    Module

        Python におけるコード再利用の基本単位。:term:`Pure Module`,
        :term:`Extension Module` のいずれか。


    Package Index

        Distributions のリポジトリで、:term:`パッケージ <Distribution
        Package>` の発見と利用を自動化する Web インターフェースを備え
        ている。


    Project

        ライブラリ、フレームワーク、スクリプト、プラグイン、アプリケー
        ション、データやその他リソースのコレクション、またはそれらの組
        み合わせ。:term:`Distribution <Distribution Package>` へパッ
        ケージされる。

        ほとんどのプロジェクトは :ref:`distutils` または
        :ref:`setuptools` を使って :term:`Distributions <Distribution
        Package>` を作るので、現在におけるプロジェクトの実際的な定義
        は、そのルートディレクトリに :term:`setup.py` を含むものと言っ
        てもよい。ここで "setup.py" は :ref:`distutils`,
        :ref:`setuptools` が使うプロジェクト仕様のファイル名だ。

        Python プロジェクトの名前は一意でなければならず、この名前が
        :term:`PyPI <Python Package Index (PyPI)>` に登録される。各プ
        ロジェクトは一つ以上の :term:`リリース <Release>` を含み、各リ
        リースは一つ以上の :term:`distribution <Distribution Package>`
        を含む。

        プロジェクト名はそれを動かす際にインポートされるパッケージ名と
        同じにするという強い規約がある。しかしこれは必ずしも真ではな
        い。プロジェクト 'foo' から distribution をインストールしたと
        き、それがパッケージ 'bar' しか提供しない、ということも可能
        だ。


    Pure Module

        Python で書かれ、単一の .py ファイルに格納された
        :term:`モジュール <module>` (.pyc / .pyo ファイルに関連付けら
        れているかもしれない)。


    Python Packaging Authority (PyPA)

        PyPA は Python パッケージングにおける重要プロジェクトの多くを
        管理する作業グループだ。https://www.pypa.io サイトの管理、
        `github <https://github.com/pypa>`_, `bitbucket
        <https://bitbucket.org/pypa>`_ 上でのプロジェクトのホスト、
        `pypa-dev メーリングリスト
        <https://groups.google.com/forum/#!forum/pypa-dev>`_ における
        議論を行っている。

    Python Package Index (PyPI)

        `PyPI <https://pypi.python.org/pypi>`_ は Python コミュニティ
        のデフォルト :term:`Package Index` だ。全ての Python 開発者が
        distributions を利用、配布できる。

    Release

        特定の時点における :term:`プロジェクト <Project>` のスナップ
        ショット。バージョン識別子で示される。

        あるリリースで複数の :term:`Distributions <Distribution
        Package>` が公開されることもある。例えば、プロジェクトのバー
        ジョン 1.0 がリリースされたとき、source distribution 形式と
        Windows インストーラ distribution 形式が利用できるかもしれな
        い。


    Requirement

       インストールする :term:`パッケージ <Distribution Package>` の指
       定。:term:`PyPA <Python Packaging Authority (PyPA)>` 推奨インス
       トーラである :ref:`pip` は様々な形の指定ができるが、それらは全
       て "requirement" とみなせる。詳しくは、:ref:`pip:pip install`
       リファレンスを見よ。


    Requirement Specifier

       :term:`Package Index` からパッケージをインストールする際、
       :ref:`pip` に渡す指定の形式。EBNF 図は :ref:`setuptools` ドキュ
       メントの `pkg_resources.Requirement
       <https://setuptools.readthedocs.io/en/latest/pkg_resources.html#requirement-objects>`_
       エントリを見よ。例えば、"foo>=1.3" は requirement specifier で
       あり、ここで "foo" はプロジェクト名、">=1.3" は :term:`Version
       Specifier` である。

    Requirements File

       :ref:`pip` を使ってインストールできる :term:`Requirements
       <Requirement>` のリストを含むファイル。詳しくは、:ref:`pip` ド
       キュメントの :ref:`pip:Requirements Files` を見よ。


    setup.py

        :ref:`distutils` と :ref:`setuptools` のためのプロジェクト仕様
        ファイル。


    Source Archive

        :term:`リリース <Release>` の生のソースコードを含むアーカイ
        ブ。:term:`Source Distribution <Source Distribution (or
        "sdist")>` または :term:`Built Distribution` を作る前段階。


    Source Distribution (or "sdist")

        :term:`Distribution <Distribution Package>` 形式の一つで、通常
        ``python setup.py sdist`` で生成される。:ref:`pip` のような
        ツールでインストールを行ったり、:term:`Built Distribution` を
        生成するのに必要なメタデータとソースファイルを含む。


    System Package

        オペレーティングシステムのネイティブ形式で提供されるパッケー
        ジ(例: rpm, dpkg ファイル)。


    Version Specifier

       :term:`Requirement Specifier` のバージョン部分。例えば、
       "foo>=1.3" の ">=1.3" の部分。:pep:`440` には、Python パッケー
       ジングが現在サポートする specifiers の :pep:`完全な仕様
       <440#version-specifiers>` がある。PEP 440 のサポートは
       :ref:`setuptools` v8.0 および :ref:`pip` v6.0 で実装された。

    Virtual Environment

        隔離された Python 環境。この中ではパッケージを特定アプリケー
        ション専用にインストールでき、システムワイドにはインストールさ
        れない。詳しくは、:ref:`Creating and using Virtual
        Environments` セクションを見よ。

    Wheel

        :pep:`427` で導入された :term:`Built Distribution` 形式で、
        :term:`Egg` 形式の置き換えを意図している。:ref:`pip` は現在
        wheel をサポートしている。

    Working Set

        インポートできる :term:`distributions <Distribution Package>`
        の集合。これらは変数 `sys.path` 上にある distributions だ。あ
        る working set では、1 プロジェクトに対応する
        :term:`distribution <Distribution Package>` は高々 1 つだ。
