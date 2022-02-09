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
- ファイルの中身を表示させる
- concatenateの略称
- `cat /bin/pwd`とか
