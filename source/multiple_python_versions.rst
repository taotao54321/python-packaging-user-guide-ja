.. _`Supporting multiple Python versions`:

==================================
複数の Python バージョンのサポート
==================================

:Page Status: Incomplete
:Last Reviewed: 2014-12-24

.. contents:: Contents
   :local:


::

  FIXME

  Useful projects/resources to reference:

  - DONE six
  - DONE python-future (http://python-future.org)
  - tox
  - DONE Travis and Shining Panda CI (Shining Panda no longer available)
  - DONE Appveyor
  - DONE Ned Batchelder's "What's in Which Python"
    - http://nedbatchelder.com/blog/201310/whats_in_which_python_3.html
      - http://nedbatchelder.com/blog/201109/whats_in_which_python.html
  - Lennart Regebro's "Porting to Python 3"
  - Greg Hewgill's script to identify the minimum version of Python
    required to run a particular script:
    https://github.com/ghewgill/pyqver
  - the Python 3 porting how to in the main docs
  - cross reference to the stable ABI discussion
    in the binary extensions topic (once that exists)
  - mention version classifiers for distribution metadata

Python パッケージを作る際、異なるバージョンの Python で使えるようにす
る必要がしばしば生じる。異なる Python バージョンには異なる(または別名
の)標準ライブラリが含まれるかもしれず、また Python バージョン 2.x, 3.x
間では構文を含めた変更が行われている。

パッケージが全てのターゲット Python (および OS!) バージョンで正しく動
くことを保証するための全テストは、手動でやったのでは非常に時間がかかる
だろう。幸い、この問題に対処するツールがいくつかあるので、ここで簡単に
論ずる。

自動テストと継続的インテグレーション
------------------------------------

自動テスト用のホスト型サービスがいくつかある。これらは通常、ソースコー
ドリポジトリ(`Github <https://github.com>`_ や `Bitbucket
<https://bitbucket.org>`_) を監視し、新たなコミットのたびにプロジェク
トのテストスイートを実行する。

これらのサービスは、プロジェクトのテストスイートを *複数バージョンの
Python* で実行する機能も提供しており、コードが正しく動くかどうかの迅速
なフィードバックが得られる。開発者はそうしたテストを自分で実行する必要
がない。

Wikipedia に多くの継続的インテグレーションシステムの幅広い `比較
<http://en.wikipedia.org/wiki/Comparison_of_continuous_integration_software>`_
がある。2 つのホスト型サービスを組み合わせて使うことで、Linux, Mac,
Windows での自動テストができる:

  - `Travis CI <https://travis-ci.org>`_ は Linux と Mac OSX の両環境
    を提供する。執筆時点で、Linux 環境は Ubuntu 12.04 LTS Server
    Edition 64 bit, OSX は 10.9.2 だ。
  - `Appveyor <http://www.appveyor.com>`_ は Windows 環境 (Windows
    Server 2012) を提供する。

::

    TODO Either link to or provide example .yml files for these two
    services.

    TODO How do we keep the Travis Linux and OSX versions up-to-date in this
    document?

`Travis CI`_ と Appveyor_ はともに `YAML <http://www.yaml.org>`_ 形式
のファイルを必要とし、これがテスト指示書の仕様となる。失敗したテストが
あれば、指定した構成の出力ログを検査できる。

Python プロジェクトを単一ソースで Python 2, 3 両方へデプロイしたい場
合、方法はいくつかある。

単一ソース Python パッケージ用ツール
------------------------------------

`six <http://pythonhosted.org/six/>`_ は Benjamin Peterson が開発した
ツールで、Python 2 と Python 3 の間の違いを吸収するためのものだ。six_
パッケージは広く使われており、Python 2 と 3 の両方で使える単一ソース
Python モジュールを書くための信頼できる方法と考えられる。six_ モジュー
ルは Python 2.5 の時点から使われていた。Armin Ronacher が開発した
`modernize <https://pypi.python.org/pypi/modernize>`_ というツールを使
うと、six_ によるコード修正を自動で適用できる。

six_ と似たものとして `python-future
<http://python-future.org/overview.html>`_ パッケージがあり、これは
Python 2 と Python 3 の間の互換レイヤを提供する; ただしこのパッケージ
は six_ と異なり、2 つの Python バージョンの一方に合致する構文を使うこ
とで Python 2 と Python 3 の相互運用性を実現しようとする。つまり:

  - Python 3 プロジェクトで(構文上の) Python 2 モジュールが使える。
  - *Python 2* プロジェクトで(構文上の) Python 3 モジュールが使える。

この双方向性により、python-future_ は Python 2 パッケージを Python 3
構文へモジュールごとに変換する方法を提供する。しかし、six_ とは対照的
に、python-future_ は Python 2.6 以降でのみサポートされる。six_ に対す
る modernize_ と同様、python-future_ には ``futurize``, ``pasteurize``
という 2 つのスクリプトが付属しており、Python 2 モジュールと Python 3
モジュールそれぞれに適用できる。

six_ または python-future_ を使うと、パッケージに実行時の依存関係が追
加される: python-future_ を使う場合、 ``futurize`` スクリプトを
``--stage1`` オプション付きで呼び出すことができ、これは Python 2.6+ が
既に Python 3 への前方互換性を持つ変更のみを施す。残りの互換性問題は手
動で解決する必要がある。

どの Python で何が変わった?
---------------------------

Ned Batchelder が各 Python リリースでの変更点のリストを `Python 2
<http://nedbatchelder.com/blog/201109/whats_in_which_python.html>`__,
`Python 3
<http://nedbatchelder.com/blog/201310/whats_in_which_python_3.html>`__
について個別に提供している。これらのリストは Python バージョン間での変
更点がパッケージに影響するかどうかのチェックに使えるかもしれない。

::

    TODO These lists should be reproduced here (with permission).

    TODO The py3 list should be updated to include 3.4
