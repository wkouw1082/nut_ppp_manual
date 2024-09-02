# 問題解決型実践プログラミング 共同開発の進め方


## 基本の進め方
### プロジェクトを始めるとき
- GitHubリポジトリを作りローカルにcloneする(またはローカルからpushする)
```bash
cd <任意の場所>
git clone https://github.com/<GitHubユーザ名>/<プロジェクト名>.git
```
- pyenvでPythonのバージョンを選ぶ(xx.xxの部分は任意のバージョン)
```bash
pyenv versions
pyenv global 3.xx.xx
python -V
```
- venvで仮想環境構築
```bash
cd <プロジェクトディレクトリのパス>
python -m venv venv
```
- venvの仮想環境に入る
```bash
source venv/bin/activate
```
- `requirements.txt`でライブラリの指定があればインストール
```bash
pip install -r requirements.txt
```

### 作業を開始するたびにやること
- venvの仮想環境に入る
```bash
cd <プロジェクトディレクトリのパス>
source venv/bin/activate
```

### 機能実装毎にやること
- 他の人の更新を取り込む
```bash
git pull --no-edit origin main
```
- gitのブランチを作って移動
```bash
git branch <ブランチ名>
git checkout <ブランチ名>
```
- 機能実装に必要なタスクの分割を検討する
- タスク毎にローカルにコミット(繰り返し)
```bash
git status
git add <編集したファイル名>.py
git commit -m "<コミットメッセージ>"
```
- 他の人の更新を取り込む
```bash
git pull --no-edit origin main
```
- メインブランチにマージ
```bash
git checkout main
git merge <ブランチ名>
```
- 更新をリモートにプッシュ
```bash
git pull --no-edit origin main
```
- ブランチを削除
```bash
git checkout <ブランチ名>
```


### 新しいライブラリをインストールしたときにやること
- `requirements.txt`にライブラリを追加
```bash
pip freeze > requirements.txt
```




## 今回の演習の準備
- 2人ペアで作業するため，リーダー1人のGitHubのリポジトリにもう1人をコラボレータとして追加する
- コラボレータに追加された人は，リポジトリをcloneして作業を始める
```bash
git clone https://github.com/<リーダーGitHubユーザ名>/<プロジェクト名>.git
cd <プロジェクト名>
```
- コラボレータはvenvの仮想環境を構築
```bash
pyenv global 3.12.5
python -m venv venv
```
- リーダー，コラボレータともに，venvの仮想環境に入る
```bash
cd <プロジェクトディレクトリのパス>
source venv/bin/activate
```
- `requirements.txt`のライブラリをインストール
  - flake8などがインストールされる
```bash
pip install -r requirements.txt
```
- gitのブランチを作って移動
  - リーダーとコラボレータで別の名前にする．
```bash
git branch <適当な名前>
git checkout <適当な名前>
```
- リーダーは`field.py`を作成，コラボレータは`player.py`を作成
```bash
touch <field または player>.py
```
- gitでステータスを確認
```bash
git status
```
- 作成したファイルをステージング
```bash
git add <field または player>.py
```
- コミット
```bash
git commit -m "Add <field または player>.py"
```
- リーダーがmainブランチに自ブランチをマージ
```bash
git checkout main
git merge <ブランチ名>
```
- リーダーがリモートにプッシュ
```bash
git push origin main
```
- リーダーがブランチを削除
```bash
git branch -d <ブランチ名>
```
- コラボレータはmainブランチに移動
```bash
git checkout main
```
- コラボレータがmainブランチをリモートから取得
```bash
git pull --no-edit origin main
```
- コラボレータが自ブランチをマージ
```bash
git merge <ブランチ名>
```
- コラボレータがリモートにプッシュ
```bash
git push origin main
```
- コラボレータがブランチを削除
```bash
git branch -d <ブランチ名>
```
- リーダーがコラボレータ変更を取り込む
```bash
git pull --no-edit origin main
```





