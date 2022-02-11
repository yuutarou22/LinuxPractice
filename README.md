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

```sh
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

## ユーザ管理

### 基礎
- マルチユーザ（設計思想） : Unixでは、複数のユーザーが１台のコンピュータを同時に使うことができる
- アカウント（英語で口座の意味）
  - ユーザ名
  - パスワード
- 1人１つのアカウントがベター。１つのアカウントを複数人で使うのはタブー。
  - 例えば、ABC3人で共有のアカウントを使用していたとする。Aが大容量のファイルを置いたとき、HDDを圧迫して他のユーザにも影響が及ぶ。
  - 1人１つであれば、管理者はファイルの所有者を調べ、個人に警告を出すことができる
  - しかし共有アカウントだと誰がやったのか、話が複雑になる。そして個人の当事者意識も薄れ無責任な態度を取るかもしれない。
  - セキュリティの問題もあるので、1人１つが無難です。

### id

- 現在ログインしているアカウントの情報を確認できる
- `$ id`だけ。
- ユーザは、ユーザIDとユーザ名を紐付けて管理している
  - ユーザ名、ユーザIDは重複することを許容しない。一意である必要がある。
  - ユーザIDは数値（コンピュータがわかりやすい）、ユーザ名は文字列（人間がわかりやすい）関係性にある。ホストとIPアドレスみたいな感じ。

```
# このとき、ユーザIDは「1000」、ユーザ名は「yutarom」となる。
# 所属グループも見れるよ。
09:09:19 :yutarom ~ $ id
uid=1000(yutarom) gid=20(staff)
# 以下略
uid=1000(yutarom) gid=20(staff) 
```

## chmod

- change modeの略称
- ファイルやディレクトリに対する操作を可能・拒否（アクセス権限）を変更する
  - r : readable（読み取り）
  - w : writable（書き込み）
  - x : executable（実行可能）
- 権限の見方
  - １桁目　: ディレクトリかどうか
  - 2~４桁目 : 所有者（ユーザ）
  - 5~7桁目 : グループ
  - 8~10桁目 : その他のユーザ（Other）

```sh
# chmod -r output で、読み取り権限を剥奪できる
09:29:25 :yutarom LinuxPractice $ ls -l output
-rw-r--r--  1 yutarom  staff  7  2 11 09:29 output
09:29:30 :yutarom LinuxPractice $ chmod -r output
09:32:45 :yutarom LinuxPractice $ ls -l output
--w-------  1 yutarom  staff  7  2 11 09:29 output
cat: output: Permission denied

# chmod +r output で、読み取り権限を付与できる
09:34:26 :yutarom LinuxPractice $ chmod +r output
09:35:09 :yutarom LinuxPractice $ ls -l output
-rw-r--r--  1 yutarom  staff  7  2 11 09:29 output
09:35:13 :yutarom LinuxPractice $ cat output
Hello!

# 所有者以外の読み取り・書き込み権限を剥奪する方法
09:35:20 :yutarom LinuxPractice $ chmod u+rw output
09:42:25 :yutarom LinuxPractice $ ls -l output
-rw-r--r--  1 yutarom  staff  7  2 11 09:29 output
09:42:31 :yutarom LinuxPractice $ chmod g-rw output
09:42:46 :yutarom LinuxPractice $ ls -l output
-rw----r--  1 yutarom  staff  7  2 11 09:29 output
09:42:50 :yutarom LinuxPractice $ chmod o-rw output
09:43:01 :yutarom LinuxPractice $ ls -l output
-rw-------  1 yutarom  staff  7  2 11 09:29 output
```

### 権限に関する疑問

- 自分一人しか使わないコンピュータ、権限の管理なんて必要なの？
  - 変更してはならない重要なファイルがあった場合に、wの権限を
