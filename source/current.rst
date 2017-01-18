.. _`推奨ツール`:

==========
推奨ツール
==========

:Page Status: Complete
:Last Reviewed: 2016-06-24

Python パッケージングとインストールについてはよく知っていて、単に現在
どのツールが推奨されているか知りたいだけなら、ここにその情報がある。


推奨インストールツール
======================

* :term:`PyPI <Python Package Index (PyPI)>` から Python
  :term:`パッケージ <Distribution Package>` をインストールするには、
  :ref:`pip` を使う。[1]_ [2]_ :ref:`pip` のインストール方法によって
  は、wheel キャッシュを利用するために :ref:`wheel` もインストールする
  必要があるかもしれない。[3]_

* 共用の Python 環境からアプリケーション固有の依存関係を隔離するには、
  :ref:`virtualenv` または `venv`_ を使う。[4]_

* 完全に統合されたクロスプラットフォームなソフトウェアスタック管理シス
  テムが欲しければ、以下を検討せよ:

  * :ref:`buildout`: 主に Web 開発コミュニティ向け。

  * :ref:`spack`, :ref:`hashdist`, または :ref:`conda`: 主に科学コミュ
    ニティ向け。


推奨パッケージングツール
========================

* プロジェクトを定義して :term:`Source Distributions <Source
  Distribution (or "sdist")>` を作るには、:ref:`setuptools` を使う。
  [5]_ [6]_

* :term:`Wheels <Wheel>` を作るには、:ref:`wheel project <wheel>` から
  利用できる :ref:`setuptools` 拡張 ``bdist_wheel`` を使う。プロジェク
  トがバイナリ拡張を含む場合、これは特に有用だ。[7]_

* :term:`PyPI <Python Package Index (PyPI)>` へ配布物をアップロードす
  るには、 `twine <https://pypi.python.org/pypi/twine>`_ を使う。


----

.. [1] 場合によっては、 ``easy_install`` (:ref:`setuptools` に含まれる)
       を選ぶことになるかもしれない。例えば、(pip がサポートしない)
       :term:`Eggs <Egg>` からインストールする必要がある場合だ。詳しい
       解説は :ref:`pip vs easy_install` を見よ。

.. [2] :pep:`453` が accept されたので、Python 3.4 以降のほとんどの環
       境で :ref:`pip` がデフォルトで利用できる。pip が選ばれた理由に
       ついては、:pep:`453` の :pep:`rationale セクション
       <453#rationale>` を見よ。

.. [3] :ref:`get-pip.py <pip:get-pip>` と :ref:`virtualenv` は
       :ref:`wheel` をインストールするが、:ref:`ensurepip` と
       :ref:`venv <venv>` は今のところそうではない。また、各種 Linux
       ディストリビューションでよく見られる "python-pip" パッケージは
       今のところ "python-wheel" に依存していない。

.. [4] Python 3.4 以降、 ``venv`` は ``pip`` がインストールされた仮想
       環境を作るので、:ref:`virtualenv` と同等になる。ただし、バー
       ジョン間の一貫性が必要なユーザには :ref:`virtualenv` の使用を勧
       める。

.. [5] ``distutils`` のみを使うことは多くのプロジェクトでは可能だが、
       これは他のプロジェクトへの依存関係の定義をサポートしておらず、
       また配布物のメタデータを自動で設定するために ``setuptools`` が
       提供するいくつかの便利なユーティリティを欠いている。
       ``setuptools`` は標準ライブラリの外部にあるので、Python の異な
       るバージョン間でより一貫した仕様を提供できる。また、
       (``distutils`` と異なり) ``setuptools`` はサポートする全ての
       バージョンで今後の "Metadata 2.0" 標準フォーマットを生成するよ
       うに更新される。

       ``distutils`` を選択したプロジェクトであっても、:ref:`pip` がそ
       のプロジェクトを(事前ビルドされた :term:`wheel <Wheel>` ファイ
       ルからではなく)ソースから直接インストールする場合、実際には
       :ref:`setuptools` を使ってビルドされる。

.. [6] `distribute`_ (setuptools のフォーク)は 2013 年 6 月に
       :ref:`setuptools` へマージされたので、setuptools がパッケージン
       グのデフォルトの選択肢となった。

.. [7] :term:`PyPI <Python Package Index (PyPI)>` は今のところ Windows
       および Mac OS X 用の wheels のみを受理しており、またそれらは
       python.org で提供されるバイナリインストーラと互換であるべきとさ
       れる。:pep:`wheel compatibility tagging scheme <425>` が改善さ
       れるまで、Linux 用 wheels は受理されない。

.. _distribute: https://pypi.python.org/pypi/distribute
.. _venv: https://docs.python.org/3/library/venv.html
