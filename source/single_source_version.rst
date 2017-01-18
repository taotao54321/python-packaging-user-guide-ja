.. _`Single sourcing the version`:

====================================
プロジェクトバージョンの単一ソース化
====================================

:Page Status: Complete
:Last Reviewed: 2015-12-03


プロジェクトのバージョン番号について、単一ソースの原則を維持する多くの
手法がある:

#.  ``setup.py`` を正規表現でパースしてバージョンを得る。例えば(`pip
    の setup.py
    <https://github.com/pypa/pip/blob/1.5.6/setup.py#L33>`_ より)::

        def read(*names, **kwargs):
            with io.open(
                os.path.join(os.path.dirname(__file__), *names),
                encoding=kwargs.get("encoding", "utf8")
            ) as fp:
                return fp.read()

        def find_version(*file_paths):
            version_file = read(*file_paths)
            version_match = re.search(r"^__version__ = ['\"]([^'\"]*)['\"]",
                                      version_file, re.M)
            if version_match:
                return version_match.group(1)
            raise RuntimeError("Unable to find version string.")

        setup(
           ...
           version=find_version("package", "__init__.py")
           ...
        )

    .. note::

        この手法は複雑な正規表現を扱わなければならない欠点がある。

#.  両方の場所で更新管理ができるか、もしくは両方の場所で使える API を
    持つ外部ビルドツールを使う。

    そんなツールはほとんどないが、挙げるとすれば `bumpversion
    <https://pypi.python.org/pypi/bumpversion>`_, `changes
    <https://pypi.python.org/pypi/changes>`_, `zest.releaser
    <https://pypi.python.org/pypi/zest.releaser>`_ だ。この順序に特定
    の意図はないし、これで全てだとも限らない。


#.  プロジェクト内の専用モジュール(例えば ``version.py``) でグローバル
    変数 ``__version__`` の値を設定し、 ``setup.py`` がそれを読んで
    ``exec`` した値を変数に格納する。

    ``execfile`` を使う例:

    ::

        execfile('...sample/version.py')
        # now we have a `__version__` variable
        # later on we use: __version__

    ``exec`` を使う例:

    ::

        version = {}
        with open("...sample/version.py") as fp:
            exec(fp.read(), version)
        # later on we use: version['__version__']

    この手法を使っている例: `warehouse
    <https://github.com/pypa/warehouse/blob/master/warehouse/__about__.py>`_

#.  単純な ``VERSION`` というテキストファイルに値を格納し、
    ``setup.py`` とプロジェクトコードの両方でそれを読む。

    ::

        with open(os.path.join(mypackage_root_dir, 'VERSION')) as version_file:
            version = version_file.read().strip()

    この手法の利点は Python に特化していないことだ。どのツールでもバー
    ジョンを読み取れる。

    .. warning::

        この手法をとる場合、 ``VERSION`` ファイルが全ての source /
        binary distributions に含まれていることを確認しなければならな
        い(例えば、 ``MANIFEST.in`` に ``include VERSION`` を追加する
        など)。

#.  ``setup.py`` で値を設定し、プロジェクトコードでは
    ``pkg_resources`` API を使う。

    ::

        import pkg_resources
        assert pkg_resources.get_distribution('pip').version == '1.2.0'

    注意: ``pkg_resources`` API が認識するのはインストール環境のメタ
    データだけであり、これは必ずしも現在インポートされているコードとは
    限らない。


#.  ``sample/__init__.py`` で ``__version__`` の値を設定し、
    ``setup.py`` で ``sample`` をインポートする。

    ::

        import sample
        setup(
            ...
            version=sample.__version__
            ...
        )

    この手法はよく使われているが、 ``sample/__init__.py`` が
    ``install_requires`` 依存関係からパッケージをインポートしていると
    失敗しうる。 ``setup.py`` の実行時点では、その依存関係はまだインス
    トールされていない可能性が高いからだ。


#.  コードではなくバージョン管理システム (Git, Mercurial など)のタグに
    バージョン番号を保管し、 `setuptools_scm
    <https://pypi.python.org/pypi/setuptools_scm>`_ を使って自動抽出す
    る。
