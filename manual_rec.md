可読性の高いコーディングのための推奨事項
==================

- プログラミング規約がないとみんなが好き勝手に書いてしまうため共同開発者が困ってしまいます。
- ここの記載事項は一般的な推奨事項と渡部の個人的な推奨が混在しているので注意をしてください．


命名規則
==================
命名規則とは
------------------
- PEP8によって定められているPythonの関数名や変数名の命名するときの規則です。
- コードは書くことよりも読まれることの方が多いため、誰にでも読みやすいように規則はしっかりと守りましょう。
- なお、この規則はPythonのみに適応されるものであり、別の言語には別の規則があるので混同しないようにしましょう。

## Letter Case (大文字小文字)の規則の例

- クラス => ルール：最初大文字 + 大文字区切り (アッパーキャメルケース)
  ```python
  class ComnetsExampleClass():
      """これがクラスの書き方です"""
  ```

- 例外 => ルール：最初大文字 + 大文字区切り (アッパーキャメルケース)
  ```python
  class ComnetsExampleError(Exception):
      """これが例外処理の書き方です"""
  ```

- メソッド => ルール：全小文字 + アンダースコア区切り (スネークケース)
  ```python
  class ComnetsExampleClass():
      def _class_only_method(self):
          """自クラス内でのみ完結するメソッドは前にアンダースコアをつける"""
      
      def other_example_method(self):
          """自クラス内以外でも使うメソッドは前にアンダースコアはつけない"""
  ```

- 関数 => ルール：全小文字 + アンダースコア区切り (スネークケース)
  ```python
  def comnets_example_fuction():
      """これが関数の書き方です"""
  ```

- インスタンス変数 => ルール：全小文字 + アンダースコア区切り (スネークケース)
  ```python
  self._example_instance = "クラス内でしか使わないインスタンス変数は前にアンダースコアをつける"
  self.example_instance = "クラス外から参照されるインスタンス変数はアンダースコアをつけない"
  ```

- 変数 => ルール：全小文字 + アンダースコア区切り (スネークケース)
  ```python
  example_instance = "これが変数の書き方です"
  ```

- 定数 => ルール：全大文字 + アンダースコア区切り (コンスタントケース)
  ```python
  CONST_EXAMPLE = "これが定数の書き方です"
  ```


## その他の命名規則の例

- Letter Caseの規則に加えて，一般的に以下のようなガイドラインに従うと良いでしょう．
    - 頭文字による略語を使わない (良い例: InterPacketTime ，悪い例: IPTime)
    - クラス名は名詞にする (例: TrafficGenerator， GraphSet， StatisticsCalculator)
    - メソッド名は動詞から始める (例: get_parametors， is_active, update_status)
    - Testやtestで始まるクラス，メソッド，ファイルはUnit Test(後述)で使うので，使用しない．
    - 例外クラスは末尾にExceptionを付ける． (例: UnconnectedGraphException)
    - 意味のない文字列は使わない (悪い例: a， b)
        - listやdictのループのための`i`や`k`，`v`などは例外
        - ループの中だけで使うダミー変数など，スコープが非常に狭い変数も例外
    - 組み込み関数(list, dict, dir, maxなど)と同じ名前の変数を作らない．どうしても作りたい場合は`list_`のようにアンダースコアを付ける．
        - 予約語はエラーが出るが，組み込み関数は警告しか出ないので注意すること．
        - 組み込み関数の一覧は[こちら](https://docs.python.org/ja/3/library/functions.html)
    - 後で使わない変数には命名せず，以下の例のように`_`などを使う．
      ```python:
      for i, j, _ in [['a1', 'a2', 'a3'], ['b1', 'b2', 'b3']]
          print(f'{i}, {j}')  # 3つ目の要素は使わないので "_" で受け取る
      ```

Python doc stringの書き方
==================
Python doc stringとは
------------------
- Pythonにおけるクラスや、メソッド(関数)についての説明を記載したコメント文のことです
- 可読性が高まるため必ず書いてください．

Python doc stringスタイル
------------------
- doc stringのタイプは一種類ではなく、いくつかのタイプが存在します
  - Googleスタイル
  - Numpyスタイル
  - PyCharmスタイルなど
- 本演習ではGoogleスタイルで書くことにします．

GoogleスタイルのPython doc stringの例
```python
    """モジュールの説明タイトル
    
    モジュールの説明
    
    """
    
    class SampleClass() :
      """クラスの説明タイトル
  
      クラスについての説明文
  
      Attributes:
          属性の名前 (属性の型): 属性の説明
          属性の名前 (:obj:`属性の型`): 属性の説明.
  
      """
  
      def print_test(self, param1, param2=None) :
          """関数の説明タイトル
  
          関数についての説明文
  
          Args:
              引数の名前 (引数の型): 引数の説明
              引数の名前 (:obj:`引数の型`, optional): 引数の説明.
  
          Returns:
              戻り値の型: 戻り値の説明 (例 : True なら成功, False なら失敗.)
  
          Raises:
              例外の名前: 例外の説明 (例 : 引数が指定されていない場合に発生 )
  
          Yields:
              戻り値の型: 戻り値についての説明
  
          Examples:
  
              関数の使い方について記載
  
              >>> print_test ("test", "message")
              test message
  
          Note:
              注意事項などを記載
  
        """
```

- 最低限Attributes、Args、Returnsは必ず書くこと

Python doctestの書き方
==================
Python doctestとは
------------------
doctest モジュールは、対話的 Python セッションのように見えるテキストを探し出し、セッションの内容を実行して、そこに書かれている通りに振舞うかを調べます。

## doc testの例
- doctestの簡単な例として足し算のテストを示します
```python
def add(a, b):
    '''
    # 例えば足し算のテストコード
    >>> add(2, 3)
    5
    '''

    result = a + b
    return result

if __name__ == '__main__':
    import doctest
    doctest.testmod()
```
プログラムを実行します。
```
$ python hoge.py
```
実行が成功している場合、何も返してきません。
エラーが起きている場合、次のように返してくるので直しましょう。

```bash
**********************************************************************
File "Main.py", line 4, in __main__.add
Failed example:
    add(2, 3)
Expected:
    5
Got:
    -1
**********************************************************************
1 items had failures:
   1 of   1 in __main__.add
***Test Failed*** 1 failures.
```


# Unit Test (単体テスト)の書き方
## Unit Test とは
- ユニットテストとは，クラス単位，メソッド単位のテストのこと．
- プログラム全体で正常に動いているかをチェックする統合テストは実施が大変だし，バグを見つけるのも大変なので，ユニットに分けて個別にテストを先に行っておくのが一般的．
- Python の場合，標準モジュールに含まれるので，インストール不要．
- `Car`クラスのテストなら`TestCar`のように頭に`Test`をつけた名前にする．
- `test*.py` の形のファイル名は自動でテストを記述したファイルだと認識されるので，`car.py`のテストなら`test_car.py`のように名付ける．
    - 逆に，テストファイル以外に`test`から始まるファイルを作ってはいけない．

## サンプルコード
- 下記はpythonのunittestで，car.pyのテストtest_car.pyを書いた例．
- `car.py` には以下のようなクラスが定義されているとする．
```python
class Car():
    def __init__(self):
        self.light = False
        self.speed = 0

    def light_on(self):
        self.light = True

    def accelate(self):
        self.speed += 10

    def brake(self):
        self.speed = 0
```
- 例えば，`test_car.py` には以下のようなテストを書く．
```python
import unittest
import car

class TestCar(unittest.TestCase):
    def setUp(self):
        """前処理"""
        self.car = car.Car()

    def test_light(self):
        """ライトが点くかテスト"""
        self.car.light_on()
        self.assertTrue(self.car.light)

    def test_brake(self):
        """ブレーキで止まるかテスト"""
        self.car.accelate()
        self.car.brake()
        self.assertEqual(self.car.speed, 0)
```

- テストを実行するには，モジュールがおいてあるディレクトリ内で，以下のコマンドを叩く．
```
python3 -m unittest
```

- テスト用の関数は,assertTrueやassertEqualの他に，以下のようなものがある．
    - assertEqual(a, b)
    - assertNotEqual(a, b)
    - assertTrue(x)
    - assertFalse(x)
    - assertIs(a, b)
    - assertIsNot(a, b)
    - assertIsNone(x)
    - assertIsNotNone(x)
    - assertIn(a, b)
    - assertNotIn(a, b)
    - assertIsInstance(a, b)
    - isinstance(a, b)
    - assertNotIsInstance(a, b)
    - not isinstance(a, b)


# 型ヒントの書き方
## 型ヒントとは
- Pythonは動的型付け言語のため，変数型は適当に書いてしまうことができますが，可読性の観点からはこれはよくありません．
- 型ヒントとは，各変数の型を明示的に書くことで，可読性を上げたり，静的型チェックを実現する方法です．
- 少なくともメソッドに対しては必ず型ヒントを書くようにしましょう．

## 静的型チェック
- また，PyCharm や VScode などのIDEを使うと，型チェックを自動で行ってくれます．
    - PyCharmはデフォルトで警告(黄色いハイライト)が出ます．
    - VScodeユーザは，[ここ](https://future-architect.github.io/articles/20201223/)に書いてある設定をしてください．
- standard_projectにも含めてある`mypy`というモジュールを使って，以下のコマンドで型チェックを行うことができます．
```bash
mypy main.py
```


## メソッドの型付けの例
- 文字列と整数を引数，浮動小数点を返り値とする場合．
```python
def sample_method(var1: str, var2: int = 0) -> float:
```

- 返り値がない場合は必ずNoneを書いておく．
```python
def sample_method(var1: str, var2: int = 0) -> None:
```

- リストや辞書を引数や戻り値にする場合．
    - ただし，Python 3.6以前は別の書き方なので注意．
```python
def sample_method(var1: list[str], var2: dict[Any]) -> tuple[int]:
```

- タプルを引数や戻り値にする場合．
    - タプルは基本的に長さが固定のため，各要素毎に型を指定する必要があります．
```python
def sample_method(var1: tuple[str, str, str], var2: list[str]) -> tuple[int, str]:
```

- 任意長のタプルを引数や戻り値にする場合，ellipsis演算子`...`を使う．
```python
def sample_method(var1: tuple[str, ...], var2: list[str]) -> tuple[int, str]:
```

- どんな型でも許容する場合はAnyを使う．
    - ただし，安易に`Any`を使うと型指定が意味をなさないので，基本的には後述の`|`を使いましょう．
```python
from typing import Any
def sample_method(var1: Any, var2: Any) -> None:
```

- 文字または整数のように，複数の型を許容する場合．
    - ただし，Python 3.6以前は別の書き方なので注意．
```python
def sample_method(var1: str | int) -> None:
```

- 自作クラスなど`int`や`str`以外の一般的ではない型を使う場合は，クラス名そのものを与える．
```python
from sample_file import OriginalClass
def sample_method(var1: OriginalClass) -> None:
```

- 型指定について，より詳しくは，[ここ](https://future-architect.github.io/articles/20201223/)を参照．


## コーディング規約のチェック
- コーディング規約(PEP8)に準拠したコードを書いてください．
- PEP8に準拠しているかどうかは以下のコマンドで確認できます．
    - pipでflake8がインストールされている必要があります．
```shell
flake8
```
- また，VSCodeの拡張機能でflake8をインストールしていれば，エディタ上で警告が出ます．


# READ ME の書き方
## READ MEとは？

- READ MEとは、”このプロジェクトが何なのか”を**簡潔に**伝える説明書．
- ソースコードを見る前に、まず**最初に**READ MEを読んで概要を理解してもらう．
- README.mdというファイルでMarkdown形式で記述するのが一般的．
- 新しくプロジェクトに加わった人が，ReadMeを読むだけで理解できるよう必ず書きましょう．


## README.mdの構成
- プロジェクトには必ずREADMEをつけましょう．
- テンプレートに例があるので，参考にしてください．

```markdown
# プロジェクト名

プロジェクトの概要を**簡潔に**書く。

## Requirement
Pythonのバージョンや必要な外部ライブラリ，外部データセットなどについて記述します．


## Installation
- cloneしてから実行するまでに必要な手順やコマンドについて書く．
  - requirements.txtによる各種モジュールのインストール
  - 外部ライブラリのインストール
  - 外部データセットのダウンロード


## Usage
- プロジェクトの使い方を書く．
  - 典型的な実行の仕方．
  - オプションなどの説明．


## Parameter Settings
- プログラムで指定できるパラメータの説明を書きます．


## Directory Structure
- プロジェクト内のファイル構成と各ファイルの説明を書く．
- treeコマンドを使うと構成をかんたんに記述できる(Macにはtreeコマンドがデフォルトでないのでbrewでインストールする)．
```

# パラメータ管理
- 他の人に使わせることを前提としたプログラムでは，パラメータをわかりやすく管理することは非常に重要です．
- パラメータの管理方法について，一般的な方法はありませんので，以下は渡部研で推奨している管理方法です．
- 以下は簡単な概要の説明ですが，基本的にはテンプレートの`config.py`と`main.py`を参照してください．

- 基本的な内部パラメータは `config.py`内に定義されるdataclassデコレータを使ったParameterクラスで管理します．
    - frozenをTrueにしているため，実行中に値が書き換わることがありません．
    - argsにコマンドライン引数(後述)が格納されます．
    - 実行日時が `run_date` に記録されます．
    - 実行した時点のGitのリビジョンが `git_revision` に格納されます．
    - `param1` の例のようにパラメータの名前とデフォルトの値を定義します．
```python
@dataclass(frozen=True)
class Parameters:
    """
    プログラム全体を通して共通のパラメータを保持するクラス．
    ここにプロジェクト内で使うパラメータを一括管理する．
    """
    args: dict = field(default_factory=lambda: {})  # コマンドライン引数
    run_date: str = ''  # 実行時の時刻
    git_revision: str = ''  # 実行時のプログラムのGitのバージョ
    
    param1: int = 0  # パラメータを定義する例
    param2: dict = field(default_factory=lambda: {'k1': 'v1', 'k2': 'v2'})  # リストや辞書で与える例
```

- 実行するごとに切り替えられると便利なパラメータは，`config.py`内の`common_args`関数内で，コマンドライン引数として定義します．
    - ここで指定したコマンドライン引数は，実行時に `python main.py --arg2 2.0` のように指定できます．
    - オプション無しでも実行できるように，必ずデフォルトの値を定義しておきましょう．
    - `-p`/`--parameters` オプションでパラメータが記述されたjsonファイルを指定すると，Parameterクラスに定義されたデフォルトの値をjsonで上書き指定できます．
```python
def common_args(parser):
    """
    コマンドライン引数を定義する関数．
    """
    parser.add_argument("-p", "--parameters", help="パラメータ設定ファイルのパスを指定．デフォルトはNone", type=str, default=None)
    parser.add_argument("-a", "--arg1", type=int, help="arg1の説明", default=0)  # コマンドライン引数を指定
    parser.add_argument("--arg2", type=float, help="arg2の説明", default=1.0)  # コマンドライン引数を指定
    return parser
```

- `Parameter`クラスと`common_args`関数は以下のように`main.py`などの冒頭で使用する．
    - パラメータの値をプログラム内で使う場合は，下記の`params`変数を使用する． 
```python
    # コマンドライン引数の設定
    parser = argparse.ArgumentParser()
    parser = common_args(parser)  # コマンドライン引数引数を読み込み
    # parser.add_argument("--main")  # 実行スクリプト固有のコマンドライン引数があればここに記入する．
    args = parser.parse_args()
    params = Parameters(**setup_params(vars(args), args.parameters))  # args，run_date，git_revisionなどを追加した辞書を取得

    # 使用例
    logger.info(params.param1)  # params変数は各パラメータにドットアクセスが可能．
    logger.info(params.args['arg1'])  # コマンドライン引数はargs['']でアクセス．
```



# 結果の出力方法
- プログラムの実行結果の出力を綺麗にしておくと、以下の利点がある。
    - 後から結果を整理しやすい
    - 目当てのグラフを見つけやすい
    - モデルのロードが容易  etc…

## 出力日をディレクトリ名に
- datetimeで出力日のタイムスタンプを取得し、ファイル名にする。
```python
import os

result_dir = f'result/{params.run_date}'  # 結果出力ディレクトリ
os.mkdir(result_dir)  # 実行日時を名前とするディレクトリを作成
```

## パラメータをjson出力
- 実行時のパラメータをjsonファイルとして出力する。
```python
from utils import dump_params

dump_params(params, f'{result_dir}’)  # パラメータを出力
```

## グラフと同時にcsvを出す
- グラフを出力する際には、同時にcsvも出力しておく。
- 後でその結果を使いたい時に、csvを読み取ることができる。
```python
import matplotlib.pyplot as plt

…

# グラフを出力
file_name = ‘sample_test’
plt.figure()
os.makedirs(f’{result_dir}{file_name}, exist_ok=True)  # 結果を出力するディレクトリを作成
plt.plot(x, y, label="test")
np.savetxt(f’{result_dir}{file_name}/sample.csv’, y, delimiter=',')  # csvファイルを出力
plt.legend()
plt.close()
```

## logを吐く
- logを出力することをloggingという。
- print()でなく、loggingモジュールを使うメリットを以下に示す。
    - ログレベル(ログの種類: Error, Debug, etc…)を設定できる。
    - ログレベルに応じた出力結果(log)を得ることができる。
```python
from utils import set_logging

logger = logging.getLogger(__name__)
set_logging(result_dir)  # ログを標準出力とファイルに出力するよう設定
logger.info('log message...')
```


プログラム実行の仕方
==================
- pythonプログラムの実行の仕方を記述します。

基本の実行方法
------------------
    python 実行したいpythonファイル.py [--args]

バックグラウンドでの実行方法
------------------
- nohupをつけることでsshした先で実行した後にログアウトしてもプログラムを動かし続けることができます。
```shell
nohup python -u 実行したいpythonファイル.py [--args] > log.log &
```
- バックグラウンドで動かした場合，ログアウト後もずっとプロセスが残るので，常にpsコマンドなどで自分が実行中のプロセスを確認するようにしてください．
    - 不要なプロセスが動き続けると他のユーザに多大な迷惑をかけることになるので，適宜psコマンドで確認してkillするように．

シェルスクリプトでの実行方法
------------------
- pythonはシェルコマンドの一つであるため、シェルスクリプトを用いることで複数のpythonファイルを一度に実行できたりします。
- シェルスクリプトの中身の例 
```shell
#!/bin/bash

echo "これはシェルスクリプトの例です"
python test.py [--args]
```

- シェルスクリプトの実行例
```shell
./shellfile.sh
```
- 詳しい書き方は[こちら](https://qiita.com/zayarwinttun/items/0dae4cb66d8f4bd2a337)の記事を参照すること。