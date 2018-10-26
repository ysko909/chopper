# ファイル中の文字列を正規表現で抜き出し整形する

## 概要

ある程度特定のフォーマットに則っているドキュメントを整形してCSV出力するスクリプト。

## 内容

ある程度特定のフォーマットに則っているドキュメントを、手を加えやすくするため正規表現で整形してCSV出力する。正規表現は、入力元の形式に則って記述する。

入力はテキストファイル。

出力は正規表現で処理された結果をカンマ区切りにしてCSV出力する。

なお、入力ファイルにおいて英数字や記号が含まれている場合は、全て半角に編集している（ソースを編集することで全角出力することも可能）。また、スペースは基本的に削除する。

現状は下記のようなドキュメントについて、「カッコで囲われ改行された単語、直後に説明の文章」というフォーマットに準拠した部分のみを抽出したい場合のソースとして実装している。

    出力対象じゃない文章1

    (関係ないテキスト)

    (カテゴリ名1)
    カテゴリ名の説明その1。
    カテゴリ名の説明その2。

    (カテゴリ名2)
    カテゴリ名の説明その1。
    カテゴリ名の説明その2。
    ...

    出力対象じゃない文章2

    (カテゴリ名3)
    カテゴリ名の説明その1。

    出力対象じゃない文章3
    ...

これを処理し出力すると下記のような内容になる。

    カテゴリ名1,カテゴリ名の説明その1。,カテゴリ名の説明その2。
    カテゴリ名2,カテゴリ名の説明その1。,カテゴリ名の説明その2。,...
    カテゴリ名3,カテゴリ名の説明その1。

入力がこの例とは異なる形式である場合は、ソースの正規表現（とそれに係る部分）を変更すればいい。

## 環境
* Python
* jaconv
  
  全角半角を交互に変換してくれるステキライブラリ。

    $ pip install jaconv

## 実行

    $ python chopper.py hoge.txt

結果は`output.csv`に出力される。
