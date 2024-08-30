# 問題解決型実践プログラミング 環境構築の手引書

## 環境構築
- 本演習では，各々のPCを使用してプログラムを作成します．
- そのため，事前に下記の手順に従って各種ツールが使えるよう環境構築を行ってください．
    - Unix系OS環境 (Mac，Linux，WSL2)
    - Git
    - GitHub
    - Python
    - pyenv
    - venv
    - IDE (VSCode 他)

### OSの準備
- 本演習では，Unix系OS (Mac，Linux，WSL2) を前提とします．Windowsしか持っていない場合は，WSL2をインストールしてください．
    - WSL2のインストール方法は[こちら](https://docs.microsoft.com/ja-jp/windows/wsl/install)を参照してください．
        - 「WSL1 から WSL2 へのバージョンのアップグレード」までを実施してください．
    - LinuxはUbuntuを推奨しますが，自分で問題解決可能なら他のディストリビューションでも問題ありません．
- いずれのOSの場合も，ターミナルを使ってコマンドで操作ができることが前提です．
    - 基本的なコマンド操作ができない場合は，2回目の演習までに習得してください．
    - もしCUI操作が不慣れな場合は，[こちら](https://qiita.com/Umeda-East45/items/6beaf53bdc24d0736ec7)を参考にしてください．



### Gitの準備
- 本演習では，Gitを使用してプログラムのバージョン管理を行います．
- 複数人での開発や，プログラムの変更履歴を残すためにもGitは非常に重要です．
    - Gitは誰が，いつ，何を，どのように変更したかを記録することができます．
    - 複数人で異なる機能を並行して開発する場合，Gitを使うことで，それぞれの機能を独立して開発することができます．
    - 独立して開発した後に，それぞれのコードを統合する機能もあります．
    - バグが発生した場合に，コードを以前のバージョンに戻せば，どの変更が原因でバグが発生したかを特定することができます．
- Gitのインストールは，MacやUbuntu，WSL2など，大抵の環境ではデフォルトでインストールされています．
    - 念の為，ターミナルで以下のコマンドを実行してGitのバージョンを確認できるか確認してください．
        - Windowsの場合は，当然WSL環境に入ってから下記コマンドを実行してください．
    ```bash
    git --version
    ```
    - また，以下のコマンドでGitのユーザ名とメールアドレスを設定されているか確認してください．
    ```bash
    git config user.name
    git config user.email
    ```
    - 何も表示されない場合は，以下のコマンドで設定してください．
    ```bash
    git config --global user.name "<あなたのユーザ名>"
    git config --global user.email "<あなたのメールアドレス>"
    ```
- 上記のコマンドでバージョンが表示されない場合は，以下の手順でインストールしてください．
    <details><summary>Macの場合</summary>

    - Homebrewをインストールしていない場合は，[ここ](https://brew.sh/ja/)の手順に従ってインストールしてください．
    - Homebrewをインストールしたら，以下のコマンドを実行してgitをインストールします．
    ```bash
    brew update
    brew install git
    ```
    </details>
    <details>
    <summary>WSL または Linux (Ubuntu)の場合</summary>
    
    - 以下の手順に従ってGitをインストールしてください．
        - Windowsの場合は，WSL2環境にGitをインストールするため，「Windowsにインストール」ではなく「Linuxにインストール」の手順に従ってください．
    ```bash
    sudo apt update
    sudo apt install git
    ```
    </details>

### GitHubの準備
- 本演習では，GitHubを使用してプログラムの共有を行います．
- GitHubは，Gitを使ってバージョン管理を行う際に，リモートリポジトリを保存するためのサービスです．
    - GitHubのリポジトリを公開設定にした場合，他の人があなたのユーザ名やメールアドレスが公開されますので注意してください．
- GitHubのアカウントを持っていない場合は，[ここ](https://github.co.jp/)からアカウントを作成してください．
- アカウントを作成したら，以下の手順でアクセストークンを取得します．
    - すでにGitHubにpushなどができている人はこの作業は不要です．
    - [ここ](https://qiita.com/shiro01/items/e886aa1e4beb404f9038)の「個人アクセストークン」の取得方法を実施して，アクセストークンを取得してください．
    - アクセストークンは，GitHubにログインする際のパスワードの代わりに使用するので，記録しておきます．
- GitHubのウェブサイトにログインして，以下の手順で新しいリポジトリを作成してください．
    - `New`をクリック
    - `pacman`など，適当なプロジェクト名をつける．
    - `Public`または`Private`を選択
        - 就活などで活用する場合は`Public`を選択するとよいでしょう．
    - それ以外の項目はデフォルトのまま，`Create repository`をクリック．
    - `Private`を選択した場合は，作成後に`Settings` > `Collaborators` > `Add people`から渡部のアカウント`wkouw1082`を追加してください．
- 以下のコマンドで，作成したリポジトリをローカルにクローンしてください．
```bash
cd <任意の場所>
git clone https://github.com/<GitHubユーザ名>/<プロジェクト名>.git
```
- `<任意の場所>`に`<プロジェクト名>`のディレクトリができていることを確認してください．
    - 中身は空で問題ありません．


### 必要ファイルのダウンロード
- [ここ](https://suitc-my.sharepoint.com/:f:/g/personal/kwatabe_mail_saitama-u_ac_jp/EvJkjZXiYs9Arh0yXf7RH1ABNLqa_nhQ7RqRY31Oa1md4w?e=aGa5Gh)に今回の演習で作成するプログラムの雛形があります．
- すべてのファイルをダウンロードして，以下のコマンドでGitHubからcloneしてできたディレクトリにコピーしてください．
  - GUIでコピーすると不可視ファイル`.gitignore`などがコピーされない可能性があることに注意してください．
```shell
cp -r <ダウンロードしたディレクトリのパス>/* <GitHubからcleneしたディレクトリのパス>/
cp -r <ダウンロードしたディレクトリのパス>/.* <GitHubからcleneしたディレクトリのパス>/
```
- 必要なファイルがコピーされていることを確認してください．
  - コピー先のディレクトリで`ls -a`を実行すると以下のような出力が得られるはずです．
  - `.git`や`.gitignore`，`result`があることを確認してください．
  ```shell
  .
  ..
  .git
  .gitignore
  README.md
  config.py
  main.py
  requirements.txt
  result
  utils.py
  ```
- 以下，特に指定がない限り，コマンドはこのコピー先のディレクトリ内で実行するものと思ってください．


### Python環境の準備
- 本演習では，Pythonを使用します．
- MacやUbuntu，WSL2など，大抵の環境ではデフォルトでPython3が使用可能ですので，インストールは不要です．
    - 念の為，ターミナルで以下のコマンドを実行してPythonのバージョンを確認できるか確認してください．
        - Windowsの場合は，当然WSL環境に入ってから下記コマンドを実行してください．
    ```bash
    python3 -V
    ```
- 各自のPCにPythonがインストールされていない場合は，[ここ](https://www.python.jp/install/install.html)の「Pythonのインストール」にある手順に従ってPythonをインストールしてください．
    - ただし，Windowsの場合はWSL2環境にPythonをインストールするため，「Windowsのインストール」ではなく「Ubuntuのインストール」の手順に従ってください．
- Google Colabなどのクラウド上でPythonを実行するツールの使用は不可です．
- Anacondaはサポート対象外ですが，問題解決を自力で行える方は使用しても構いません．
    - 本演習程度の課題なら，大きな問題は起きないと思いますので，すでにPythonに習熟していてAnacondaを使っている方はそのままで構いません．

### pyenvの準備
- pyenvはPythonのバージョン管理ツールです．
- 複数のバージョンのPythonをインストールして切り替えることができます．
- プロジェクト毎にバージョンを切り替えることで、バージョンによる互換性の問題を回避することができます．
- 以下の手順に従い，pyenvをインストールしてください．
    <details>
    <summary>Macの場合</summary>
    
    - Homebrewをインストールしていない場合は，[ここ](https://brew.sh/ja/)の手順に従ってインストールしてください．
    - Homebrewをインストールしたら，以下のコマンドを実行してpyenvをインストールします．
    ```bash
    brew update
    brew install pyenv
    ```
    - さらに以下のコマンドでpyenvの環境変数と初期化を`.zshrc`に書き込みましょう．
    ```
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
    echo 'eval "$(pyenv init -)"' >> ~/.zshrc
    source ~/.zshrc
    ```
    </details>

    <details>
    <summary>WSL または Linux (Ubuntu)の場合</summary>
    
    - [ここ](https://zenn.dev/hr0t15/articles/8ae3564bde2cce)を参考にpyenvをインストールします．
    </details>

- インストールが完了したら，pyenvを使って特定バージョンのPythonをインストールします．
    - ここでは，以下のコマンドで`3.12.5`をインストールしましょう．
    ```bash
    pyenv install 3.12.5
    ```
    - 開発を始める段階で，どのバージョンを使うかを開発者全員で合意しておくことが重要です．
    - なお，インストール可能なバージョンは以下のコマンドで確認できます．
    ```bash
    pyenv install --list
    ```
- 続いて，以下のコマンドを実行して，pyenvでインストールしたPython 3.12.5 に切り替えられることを確認してください．
```bash
pyenv global 3.12.5
python -V
```
- 以下のように`3.12.5`のバージョンが表示されればOKです．
```bash
Python 3.12.5
```


### venvの準備
- venvはPythonの仮想環境を作成するためのツールです．
- Pythonではpipというパッケージ管理ツールを使ってライブラリをインストールしますが，venvを使うことで，プロジェクト毎に異なるpipの環境を作成することができます．
- venvはPython3.3以降に標準で付属しているのでるので，インストール作業は不要です．
- 今回はPythonで完結するアプリケーションなのでvenvで十分ですが，Dockerなどのコンテナ技術を使ってプロジェクト毎の個別環境を用意することも可能ですので勉強してみると良いでしょう．
- 以下のコマンドで，プロジェクトディレクトリ内に仮想環境を作成してください．
    - コマンドの最後の`venv`は任意の名前でOKですが，`venv`または`.venv`が一般的です．
```bash
cd <プロジェクトディレクトリのパス>
python -m venv venv
```
- `ls`コマンドでディレクトリ内のファイルを確認して，`venv`ディレクトリが作成されていることを確認してください．
- 続いて，以下のコマンドを実行してvenvを有効化してください．
```bash
source venv/bin/activate
```
- 有効化されると，以下のようにターミナルのプロンプトの先頭に`(venv)`と表示されます．
```bash
(venv) username@machinename project %
```
- このプロジェクトでPythonを実行する際は，常にvenvを有効化した状態で作業してください．
    - なお，作業が終わったら，以下のコマンドでvenvを無効化できます．
    ```bash
    deactivate
    ```


### IDEの準備
- 開発環境は任意ですが，テキストエディタだけでは型のチェックなどに限界があるため，本演習では，ある程度リッチな機能を持つIDEを使用する方が良いでしょう．
- 特にこだわりがない場合はVSCodeを推奨します．
    - VSCodeを使う場合は，[ここ](https://code.visualstudio.com/)からダウンロードしてください．
    - インストール後，VSCodeを起動して，左側の拡張機能アイコンをクリックして，以下の拡張機能をインストールしてください．
        - 必須
            - Python
            - Python Debugger
            - Flake8
            - Mypy Type Checker
            - Git Graph
            - Live Share
        - 推奨
            - Japanese Language Pack for Visual Studio Code
    - AI生成機能ややフォーマットを自動で修正してくれる拡張機能は敢えて外してあります．
        - AI生成機能やオートフォーマッターは便利ですが，どこがどう間違いなのか，なぜそれが正解なのかを理解することが難しくなり，本演習の趣旨に合わないためです．
        - ある程度プログラミングの構造や文法，ルールを理解してからならば，以下の拡張機能が非常に強力なツールになるでしょう．
            - Copilot
            - autoDocstring
            - Black Formatter
            - isort
            - gitignore
- WSLの場合，WSL上のコードをVSCodeで編集するために以下の作業を行ってください．
    - [ここ](https://learn.microsoft.com/ja-jp/windows/wsl/tutorials/wsl-vscode)にある手順に従って，WSL上のプロジェクトのファイルが開けること確認してください．


#### GitとGitHubのプロジェクト初期設定
- Gitの使い方は後ほど詳しく説明しますが，ここでは，GitとGitHubのプロジェクト初期設定を行います．
- ローカルとGitHubのリポジトリを紐づけるために，以下のコマンドを実行してください．
```bash
cd <プロジェクトディレクトリのパス>
git add README.md
git add config.py
git add main.py
git add utils.py
git add requirements.txt
git add .gitignore
git status
```
- Gitのバージョンにより多少異なるかもしれませんが，以下のような出力が表示されればOKです．
```bash
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   README.md
	new file:   config.py
	new file:   main.py
	new file:   utils.py
	new file:   requirements.txt
	new file:   .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)
  ．．．
```
- 続いて，以下のコマンドを実行して，gitのコミットができることを確認してください．
```bash
git commit -m "Initial commit"
```
- 概ね以下のような出力が表示されればOKです．
```bash
[main (root-commit) 9c6d271] Initial commit
4 files changed, 159 insertions(+)
create mode 100755 README.md
create mode 100755 config.py
create mode 100755 main.py
create mode 100755 requirements.txt
```
- 最後に，以下のコマンドを実行して，GitHubにpush(アップロード)できることを確認してください．うまくいかない場合は`main`の部分を`master`に変更してみてください．
    - アカウント名とパスワードを聞かれるので，GitHubのユーザ名と記録したアクセストークンを入力してください．
```bash
git push origin main
```
- 以下のような出力が表示されればOKです．
```bash
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 2.79 KiB | 2.79 MiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/wkouw1082/PPP.git
 * [new branch]      main -> main
```
- GitHubのウェブサイトにアクセスして，リポジトリにファイルがアップロードされていることを確認してください．



### 環境構築の確認
- 2回目の演習に臨む前に，ここまでの手順が正しく行われてるか確認するために，以下の手順を必ず実行してください．

#### VSCodeの確認
- 以下のコマンドを実行して，VSCodeが起動して，ダウンロードしたファイル群が表示できればOKです．
    - VSCode以外のIDEを使う場合は，そのIDEを起動して，ダウンロードしたファイル群が表示できる状態にしてください．
```bash
code .
```

#### Gitの確認
- GitHubのウェブサイトにアクセスして，ダウンロードしたファイル群がvenvを除きすべてアップロードされていることを確認してください．
- GitHubのウェブサイトにアクセスして，`.gitignore`ファイルがアップロードされていることを確認して，中身が記述されていることを確認してください．


#### Python環境の確認
- 以下のコマンドを実行して，venv環境に入れることを確認してください．
```bash
cd <プロジェクトディレクトリのパス>
source venv/bin/activate
```
- 以下のようにターミナルのプロンプトの先頭に`(venv)`と表示されればOKです．
```bash
(venv) username@machinename project %
```
- venv環境に入ったあとに，以下のコマンドを実行して，`Python 3.12.5`と表示されることを確認してください．
```bash
python -V
```
- venv環境に入ったあとに，以下のコマンドを実行してPythonが実行できることを確認してください．`Process terminated successfully. `と表示されればOKです． 
```bash
python main.py
```


### トラブルが発生した場合
- まずはコマンドの英語のエラーメッセージをきちんと読みましょう．
- エラーメッセージをGoogleで検索してみましょう．
- 英語のサイトも諦めずに参照しましょう．
