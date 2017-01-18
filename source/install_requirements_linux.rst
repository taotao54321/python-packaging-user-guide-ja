
.. _`Installing pip/setuptools/wheel with Linux Package Managers`:

====================================================================
Linux パッケージマネージャによる pip/setuptools/whell のインストール
====================================================================

:Page Status: Incomplete
:Last Reviewed: 2015-09-17


このセクションでは、Linux パッケージマネージャを使って :ref:`pip`,
:ref:`setuptools`, :ref:`wheel` をインストールする方法を説明する。

`python.org <https://www.python.org>`_ からダウンロードした Python を
使っているなら、このセクションの内容は当てはまらない。代わりに、
:ref:`installing_requirements` セクションを見よ。

特定の Linux ディストリビューションでサポートされる :ref:`pip`,
:ref:`setuptools`, :ref:`wheel` は、それが公開された時点で既に古いバー
ジョンであることがよくある。そして、更新は普通セキュリティ上の理由での
み行われ、機能更新は行われない。ディストリビューションによっては、より
新しいバージョンを提供する追加リポジトリがある。我々が知っているリポジ
トリについては以下で説明する。

また、Linux ディストリビューションがセキュリティ上の理由だったり固有の
標準に合わせるためにパッチを当てていることもしばしばある。場合によって
は、これがオリジナルのパッチなしバージョンとは異なるバグや予期せぬ動作
につながる可能性がある。わかっている範囲については以下で注意する。


Fedora
~~~~~~

* Fedora 21:

  * Python 2::

      sudo yum upgrade python-setuptools
      sudo yum install python-pip python-wheel

  * Python 3: ``sudo yum install python3 python3-wheel``

* Fedora 22:

  * Python 2::

      sudo dnf upgrade python-setuptools
      sudo dnf install python-pip python-wheel

  * Python 3: ``sudo dnf install python3 python3-wheel``


Python 2 の pip, setuptools, wheel のより新しいバージョンを得るには、
`Copr Repo instructions
<https://fedorahosted.org/copr/wiki/HowToEnableRepo>`__ に従って `PyPA
Copr Repo <https://copr.fedoraproject.org/coprs/pypa/pypa/>`_ を有効に
し、以下を実行する::

  sudo yum|dnf upgrade python-setuptools
  sudo yum|dnf install python-pip python-wheel


CentOS/RHEL
~~~~~~~~~~~

CentOS と RHEL はデフォルトで :ref:`setuptools` がインストールされてい
るが、:ref:`pip`, :ref:`wheel` はコアリポジトリでは提供されない。

システムの Python 用に pip, wheel をインストールするには、2 つの方法が
ある:

1. `この説明
   <https://fedoraproject.org/wiki/EPEL#How_can_I_use_these_extra_packages.3F>`__
   に従って `EPEL repository <https://fedoraproject.org/wiki/EPEL>`_
   を有効にする。EPEL 6, EPEL 7 では、以下のようにして pip をインス
   トールできる:

     sudo yum install python-pip

   EPEL 7 (EPEL 6 は不可)では、以下のようにして wheel をインストールで
   きる::

     sudo yum install python-wheel

   EPEL が提供するのは競合を起こさない追加パッケージのみなので、
   setuptools は提供されない。それはコアリポジトリに存在するからだ。


2. `この説明
   <https://fedorahosted.org/copr/wiki/HowToEnableRepo>`__ [1]_ に従っ
   て `PyPA Copr Repo
   <https://copr.fedoraproject.org/coprs/pypa/pypa/>`_ を有効にする。
   以下のようにして pip, wheel をインストールできる::

     sudo yum install python-pip python-wheel

   setuptools のアップグレードも行うには、以下を実行する::

     sudo yum upgrade python-setuptools


並行して非システム環境に pip, wheel, setuptools を (yum を使って)イン
ストールするには、2 つの方法がある:


1. "Software Collections" 機能を使い、pip, setuptools, wheel を含む共
   存可能なソフトウェアコレクションを有効にする。

   * RedHat の場合、以下を参照:
     http://developers.redhat.com/products/softwarecollections/overview/
   * CentOS の場合、以下を参照:
     https://www.softwarecollections.org/en/

   このコレクションは最新バージョンを含むとは限らない。

2. `IUS repository <https://ius.io/GettingStarted/>`_ を有効にし、
   `parallel-installable
   <https://ius.io/SafeRepo/#parallel-installable-package>`_ な Python
   を pip, setuptools, wheel と一緒にインストールする。これはほぼ最新
   に保たれている。

   例えば、CentOS7/RHEL7 で Python 3.4 を選ぶ場合::

     sudo yum install python34u python34u-wheel


openSUSE
~~~~~~~~

* Python 2::

    sudo zypper install python-pip python-setuptools python-wheel


* Python 3::

    sudo zypper install python3-pip python3-setuptools python3-wheel


Debian/Ubuntu
~~~~~~~~~~~~~

::

  sudo apt-get install python-pip

Python 3 の場合、"python" を "python3" に置き換える。


.. warning::

   Debian/Ubuntu の最近のバージョンは pip がデフォルトで `"User
   Scheme" <https://pip.pypa.io/en/stable/user_guide/#user-installs>`_
   を使うように修正を加えている。これは大きな仕様変更であり、ユーザに
   よっては驚くべき動作になりうる。


Arch Linux
~~~~~~~~~~

* Python 2::

    sudo pacman -S python2-pip

* Python 3::

    sudo pacman -S python-pip

----

.. [1] 今のところ、CentOS/RHEL では "copr" yum プラグインは利用できな
       い。よって、説明にあるように唯一の選択肢はリポジトリファイルを
       手動で配置することだ。
