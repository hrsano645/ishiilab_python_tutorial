# 石井研究室 Pythonチュートリアル

この資料は、[東海大学石井研究室](http://ishiilab.net) へ新規参加された学生向けに作成したPythonチュートリアルの資料です。
Pythonの基礎的な扱い方と以下の課題を用意しています。

- csvモジュールを使いデータ収集: tutorial_exam_csv.ipynb
- BeautifulSoup4, Requestsを使ってWEBスクレイピング: tutorial_exam_webscraping.ipynb

# 必要環境

Python3.4が動作する環境に学習用の環境として利用しているipython notebookをインストールしています。  
また、WEBスクレイピングを行うためにBeautiflesoup4, requestsの２つの外部モジュール(Pythonに同梱されていないサードパーティパッケージ)をインストールする必要があります。

これら２つのパッケージは、pipという[PyPI](https://pypi.python.org/pypi)上で提供されているパッケージをインストール、管理するツールを利用してインストールします。

## Pyzoを利用する
WindowsでPythonをインストールしていない方は、予めipython notebook、科学技術系のモジュールライブラリなど開発でよく使われるモジュールが同梱されている「Pyzo」というポータブル環境を利用することを推奨しています。

[Python to the people — Pyzo - Python to the people](http://www.pyzo.org/)

マルチプラットフォームですが、特にWindowsユーザーにおすすめです。

このハンズオンでは、`2015a`というバージョンを利用しています。

- <http://bitbucket.org/pyzo/pyzo/downloads/pyzo_distro-2015a.win64.zip>
- <http://bitbucket.org/pyzo/pyzo/downloads/pyzo_distro-2015a.win32.zip>

### チュートリアル環境の準備
pyzoのフォルダ上にダウンロードしたzipファイルを解凍し適当なフォルダへ展開します。展開されたフォルダ内には、`pyzo2015a` というフォルダがあります。(このチュートリアルで指定されているpyzoのバージョンは2015aです)このフォルダをCドライブの配下に移動させて下さい。

以降、 `C:¥pyzo2015a`のフォルダがpyzoカレントディレクトリとなります。 

pyzoカレントディレクトリ内の`ipython_notebook.exe`を起動することで、自動的にブラウザが開いてipython notebookが利用できます。

また、このPyzoの環境に、課題で利用するBeautiflesoup4のインストールを行う必要があります。`ipython_notebook.exe` と同じフォルダに有る` IEP.exe`というIDE環境からインストール可能です。

- `IEP.exe`を起動する。
    - ウィザード画面が表示されますが、 `Show this wizard on startup` のチェックを外して `stopボタン` を押してウィザード画面を終了します。
- IPEのメイン画面の上部にあるipythonのコンソール上に、`pip install beautifulsoup4` と入力し `Enterキー` で実行します。
- インストールが終了したら、コンソール上で`import bs4`と入力し`Enterキー` で実行します。この時にimport Errorが表示されなければインストールは成功しています。

Pyzoに標準でインストールされているパッケージは以下のリンクを参照して下さい。

[Packages — Pyzo - Python to the people](http://www.pyzo.org/packages.html#packages)

## システムにPython3.4をインストールする

※このチュートリアルでは想定した環境ではありませんが、利用することは出来ます。（筆者はMac OS X 10.10 にて確認) 以下に参考情報を記載します。

インストール済みのシステム環境にipytho notebookをセットアップすると、システム側に不必要なパッケージが多くインストールされてしまうため、virtualenvというPythonの仮想環境作成ツールの利用を推奨します。

### 各種OSへのPythonのインストール

#### Windows
Windowsではインストーラーが用意されているので、利用すればすぐにPythonを始めることが出来ます。

[Python Release Python 3.4.3 | Python.org](https://www.python.org/downloads/release/python-343/)
(お持ちのPCで利用できるOSのメモリ空間、32/64bitを選んでインストーラーを利用して下さい。わからない場合は**32bit**のインストーラーを利用して下さい。)

Pythonのインストール先のパスを環境変数のPATHに登録するとスムーズに作業ができます。　インストール時に **Add python.exe to the Path** のオプションを有効にすると自動的にPATHをセットします。（以降はPATHを設定し、コマンドプロンプトでpythonを実行すると

Pythonの実行はコマンドプロンプト（またはPowershell）より行います。
最新の環境ではpipはインストール済みです。仮想環境を作成するためにvirtualenvをインストールします。

virtualenvを利用し仮想環境を作成し、仮想環境上でチュートリアル環境を用意します。

例では、`C:¥User¥ishiilab¥Documents` というユーザーディレクトリにあるDocumentsフォルダ内に `ishiilab_python_tutorial` フォルダを作成し、 `virtualenv` コマンドを利用して仮想環境を作成します。

作成出来ると、コンソール行の先頭にカッコで仮想環境名が表示されます。(この名前は仮想環境を作成した時のフォルダ名になります)

```
C:¥User¥ishiilab¥Documents> mkdir .¥ishiilab_python_tutorial
C:¥User¥ishiilab¥Documents> cd .¥ishiilab_python_tutorial
C:¥User¥ishiilab¥Documents¥ishiilab_python_tutorial> python -m virtualenv .¥
C:¥User¥ishiilab¥Documents¥ishiilab_python_tutorial> .¥Scripts¥activate # 仮想環境が利用できます。

(ishiilab_python_tutorial) C:¥User¥ishiilab¥Documents¥ishiilab_python_tutorial>
```

#### Mac OS, Linux

Mac OS Xではpython.orgからのインストーラーを利用する、もしくはhomebrew, macportsを使ってインストールする方法があります。
ここではhomebrewでのインストール方法を提示します。

```
$ brew install python3
$python3 --version
python 3.4.3
```

Linuxは各ディストリビューションのパッケージ管理システム(apt, yumなど)の利用やソースコードのビルドよりインストール下さい。

`Python --version` の結果が `python 3.4.3` と言った結果を取得できればインストールできています。

その後はWindowsと同じように、 `pip` を利用して `virtualenv` をインストール、 `virtualenv` コマンドを使い仮想環境を作成します。

```
~$ pip install virtualenv
```

```
~$ mkdir ishiilab_python_tutorial
~$ cd ishiilab_python_tutorial
~/ishiilab_python_tutorial$ python -m virtualenv ./
.~/ishiilab_python_tutorial$ ./bin/activate # 仮想環境が利用できます。
(ishiilab_python_tutorial) ~/ishiilab_python_tutorial$
```

### チュートリアル環境の準備

virtualenvという仮想環境を作成するツールを利用し、このチュートリアル用の仮想環境上に、ipython notebookや課題で利用するパッケージをインストールします。

以下のURLからファイル: `requirements.txt` をダウンロードして下さい。

<https://drive.google.com/a/ishiilab.net/file/d/0ByTX-9viSBPLU3JHOFFvc3ZMSVU/view?usp=sharing>

ダウンロードしたフォルダ内にある、すべてのファイルを用意した仮想環境のフォルダ（例では `ishiilab_python_tutorial` ）へコピーして下さい。

すべてのOSで、virtualenvの仮想環境が動作している状態で、`pip` コマンドを利用してパッケージをインストールします。

```
pip install -r requirements.txt #必要なパッケージをインストールします。
```

### virtualenvの終了方法

virtualenvは、仮想環境上にある `activate` を実行して利用しますが、終了する場合は、 `activate` が実行された状態で、`deactivate` を入力し実行します。Windowsの場合は補完されませんが、Mac OS, LinuxはTAB補完が可能です。

以下Windowsの例です。

```
(ishiilab_python_tutorial) C:¥User¥ishiilab¥Documents¥ishiilab_python_tutorial> deactivate
C:¥User¥ishiilab¥Documents¥ishiilab_python_tutorial> # 仮想環境から抜け出した
```

# 謝辞
このチュートリアルは、以下の資料を抜粋、改変、参考にしています。

1. [概要 — Python 3.4.3 ドキュメント](http://docs.python.jp/3/)
2. [Python Hack-a-thon 2010.11 ハンズオン 初級 — Python Hack-a-thon 2010.11 1.0 documentation](http://tokibito.bitbucket.org/python-hackathon201011/index.html)
3. [Python Developers Festa 2012.07 ハンズオン 初級 — Python Developers Festa 2012.07 documentation](http://pyfes-201207.readthedocs.org/en/latest/index.html)
    - [tokibito / pyfes-201207 — Bitbucket](https://bitbucket.org/tokibito/pyfes-201207/overview)

# ライセンス
謝辞にあります 2.の提供ライセンスにある [Creative Commons — 表示 2.1 日本 — CC BY 2.1 JP](http://creativecommons.org/licenses/by/2.1/jp/)として提供しています。
