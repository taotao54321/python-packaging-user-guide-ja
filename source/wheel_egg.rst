.. _`Wheel vs Egg`:

============
Wheel vs Egg
============

:Page Status: Complete
:Last Reviewed: 2015-09-10

:term:`Wheel` と :term:`Egg` はともに、ビルドやコンパイルなしでインス
トールを行うユースケースをサポートするパッケージ形式だ。これらによって
ビルドやコンパイルに伴うテストや開発ワークフローのコストが削減される。

:term:`Egg` 形式は :ref:`setuptools` が 2004 年に導入した。一方
:term:`Wheel` 形式は :pep:`427` が 2012 年に導入した。

現在は :term:`Wheel` が Python 用の :term:`ビルド済み <Built
Distribution>` または :term:`バイナリ <Binary Distribution>` パッケー
ジ方式の標準と考えられている。

:term:`Wheel` と :term:`Egg` の重要な違いを示す:


* :term:`Wheel` には :pep:`公式 PEP <427>` があるが、:term:`Egg` には
  ない。

* :term:`Wheel` は :term:`distribution <Distribution Package>` 形式、
  つまりパッケージング形式だ。[1]_ :term:`Egg` は distribution 形式で
  ある一方ランタイムインストール形式でもあり (zip 形式のままの場合)、
  インポートができるように設計されている。

* :term:`Wheel` アーカイブは .pyc ファイルを含まない。よって、
  distribution が Python ファイルのみを含み(一切のコンパイル済み拡張を
  含まず)、Python 2 および 3 と互換性があるなら、wheel を "universal"
  にできる(:term:`sdist <Source Distribution (or "sdist")>` のように)。

* :term:`Wheel` は :pep:`PEP 376 準拠 <376>` の ``.dist-info`` ディレ
  クトリを使う。Egg は ``.egg-info`` を使う。

* :term:`Wheel` には :pep:`情報量の多いファイル名規約 <425>` がある。
  Wheel アーカイブ名を見るだけで、互換性のある Python バージョンおよび
  実装、ABI, システムアーキテクチャがわかる。

* :term:`Wheel` はバージョン管理されている。全ての wheel ファイルは、
  wheel 仕様およびパッケージングを行った実装のバージョンを含む。

* :term:`Wheel` は内部的に `sysconfig path type
  <http://docs.python.org/2/library/sysconfig.html#installation-paths>`_
  を使って構成されているため、他の形式に変換するのが容易だ。

----

.. [1] ときどき wheel がインポート可能なランタイム形式として使われるこ
       とがあるが、:pep:`現在これは公式にはサポートされない
       <427#is-it-possible-to-import-python-code-directly-from-a-wheel-file>` 。
