# LinuxPractice

## cd

- change directory
- カレントディレクトリを移動する

## pwd

- print name of working directory
- カレントディレクトリを出力

## ls

- listの略称
- ディレクトリの中身をリスト表示する
- `ls /usr` : ディレクトリ指定可能
- `ls /usr -l` : -lオプションで詳細な情報を確認できる
- `ls -l -R ./Downloads` : -Rオプションで、配下の全ての情報を確認できる

```
# 例
19:04:40 :yutarom ~ $ ls -l
drwxr-xr-x+  5 yutarom  staff        160 10 12  2019 Public/
drwxr-xr-x   5 yutarom  staff        160  2 28  2020 app/
-rw-r--r--@  1 yutarom  staff  657457152 10  6  2019 archlinux-2019.10.01-x86_64.iso
drwxr-xr-x   3 yutarom  staff         96  7 26  2019 board_game/
drwxr-xr-x  11 yutarom  staff        352 12 16  2020 code/
drwxr-xr-x   2 yutarom  staff         64  4 11  2020 dotfiles/
-rw-r--r--   1 yutarom  staff         27 10 12  2019 package-lock.json
drwxr-xr-x   5 yutarom  staff        160 12 16  2020 vagrant/
```

- ディレクトリであるか
- 権限
- リンク数
- 所有者
- グループ
- サイズ
- 最終更新日
- ディレクトリ名

## man

- manualの略称
- `man ls` : lsコマンドの使い方が確認できる
- 終了時は`q`を押下
- 文書レベルで結構な量が詳しく表示される

## --helpオプション

- `ls --help` : lsコマンドのヘルプが出力される
- manに比べてシンプルな説明が出てくる
- `help ls` : こっちでも出るかも

## mkdir

- make directoryの略称
- ディレクトリを新規作成
- `mkdir test` : testという名称のディレクトリを作成する

## mv

- moveの略称
- ディレクトリやファイルの場所を移動する、名前の変更をする
- `mv test test2` : test→test2へ変更する

## rm

- removeの略称
- 指定したファイルを削除する
- `rm -f test.txt`
  - `-f`オプションは、有無を言わさず消させる。ファイル削除の前に確認されるのを省略する。

## rmdir

- remove directoryの略称
- 指定したディレクトリを削除する

## 絶対パス・相対パス

`/` はルートディレクトリを表す。

- 絶対パス
  - ルートディレクトリから辿ってパスを表現する方法
  - `/home/taro/test` `/` ルートディレクトリ
- 相対パス
  - カレントディレクトリを起点にしどのように辿っていけば特定のファイル・ディレクトリにたどり着くかを表現する方法
  - `./taro/test` `./` カレントディレクトリ
  - カレントディレクトリから近い

## cat

- concatenateの略称
- テキストファイルの中身を表示させる
- バイナリファイルの中身を見たいなら `od -t d1 /bin/pwd` とかで見れる

## cp

- copyの略称
- ファイルをコピーする
- `cp コピー元（ファイル名） コピー先（ファイル名）`

## echo

- echo（やまびこ）
- `echo Hello` 標準出力でHelloを表示するだけ。
- `echo Hello > output` outputというファイルを作成してその中にHelloを出力する意味。

## 出力リダイレクト

- ダイレクト（方向づけ）、リ（やり直す）　→ リダイレクト（方向づけし直す）
- 通常の出力はターミナルに表示するが、出力リダイレクトすると、ファイルに出力する
- `date > output`とかでもできる。「> ファイル名」とすると、結果をそのファイルに書き込むことができる

### 上書き

- `date >> output` 「>>」を使用する

## 入力リダイレクト

- キーボードから行うのではなく、ファイルから入力を行う
- お試し
  - bcコマンド（対話型の計算コマンド）の有無を確認
  - `echo 2+3 > input` 計算式の書かれたファイルを作成する
  - `bc < input` 計算式の書かれたファイルをbcコマンドへ渡す

## パイプ

- `|`記号のこと
- 標準出力された内容を次のコマンドへ橋渡しするために使われるテクニック
- `echo 2+3 | bc` 「2+3」という文字列をecho出力せず、bcコマンドに渡して、その計算結果をechoしている。
  - 計算式ぽくかくとこんな感じ？　`echo ((2+3) > bc)`
  - `ls -l /usr/bin` これだと最初の方が流れてしまって見にくい
  - `ls -l /usr/bin | less` 画面サイズに合わせて１ページごとに表示してくれる
    - lsの結果をlessへ渡しているイメージですわ。
- 利点
  - 正直なところ、出力リダイレクト（ファイルに出力）→入力リダイレクトでも可能。
  - 出力リダイレクトで出力したファイル（中間ファイルと呼ぶ）は、出力結果を確認できる側面もある一方で、HDDの容量を使用してしまう
  - 入力リダイレクトに渡すときも、中間ファイルを読み込むのでパイプに比べて時間がかかる短所がある。
  - なので、慣れた人は中間ファイルを使わずパイプを活用する

### | less

- 大量の出力結果などがある場合、`| less`を使ったテクニックが多用される。
- テキストデータが入力されると、画面の縦幅に応じて１ページずつ表示させる。
  - スペースキー：１ページ分進む
  - エンターキー：1行ずつ進む
  - ↑↓キーでも操作可能

### | wc

- word countの略称
- 数を見るときに使える。
- `ls -l /usr/bin | wc`
  - 「1035    9418   63021」　行数　語数　文字数
  - 行数を見ると、/usr/binのファイルの数がわかるね

