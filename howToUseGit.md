# gitのつかいかた

## 1. gitってなに
gitとは、
> 分散型バージョン管理システム (wikipe...)

である。

なんていうことをいっても意味がわからない。
簡単にいってしまえば、「ファイルの管理をしてくれる便利なツール」、で良いのだろうか。

まあ、文章で説明するのも難しいし、実際に例に触れてみるのが良いのかもしれない。

## 2. gitのすごさ

### 1. gitをつかわないとこうなる
ファイルの管理ってみんなはどのようにやっているのだろう。

自分ならこうしている。

```
 === Finder ===
 WFModel
 WFModel_v2
 WFModel_v3
 WFModel_test
```

実は、これ、非常によくないファイルの管理なんだ。これは一応、``WFMdel_v3``っていうのが一番新しいフォルダでわかりやすくなっている。
けど、``WFModel_test``なんていうフォルダなんかもあって、これでテストしながら、新しい機能を付けてしまっていたり、別の``v2``で機能追加していたり、
時間が経てば立つほど、中身がごちゃごちゃになっていくと思うんだ。

しかも、人とチーム開発をする状況を考えてみてほしい。Aさんは``v3``のほうで、色々なところを編集したり、新しいフォルダを追加したりしている。
さらに、Bさんは、``v4``なんていうフォルダを作ってそこで、開発していたとする。

このとき、AさんとBさんのフォルダをzipでまとめて渡して、どうやって管理するのだろうか。
これって、管理しやすい？　それともしにくい？

例えば、Aさんが編集したところを、Bさんのほうで動かすとエラーがおきて動かなくなってしまったりするかもしれない。
フォルダもぐちゃぐちゃになるし、そもそも、zipで渡しあったやつを統合するのってすごい難しいよね。
そこで、ちゃんとしたファイルの管理がしたくなっていくるわけなんです。

### 2. gitをつかうとこうなる

> じゃあ、神みたいな管理ができるような奴なんておるん？

はい。いますいます。それ、GIT君です。

Gitされあれば、こうなる。

```
 === Finder ===
 WFModel
```

もうフォルダの名前でファイルの管理なんてしない。時代はgitなんです(使ってない企業はないです多分)。
しかも、誰がどこを編集したとか、消したとか、追加したとかも分かる。さらには、いつでも前の状態に戻れる。
そんなすごいgitのフローを説明します。

## 2. gitのふろー
gitはこれみればわかります。[gitのつかいかた](https://tracpath.com/bootcamp/learning_git_firststep.html)

gitにはリポジトリという概念があります。上のリンク先ではリポジトリについては説明がないのに、リポジトリを連呼していますね。
リポジトリはファイルとフォルダとかの管理したい対象が入ったものです。

リポジトリにはリモートレポジトリとローカルリポジトリがあります。PCの中身にあるのがローカルで、皆と共有するのがリモートです。
チームメンバーはそれぞれ、リモートのほうから、ローカルへとリポジトリを持ってきて、PCで編集したりして、リモートのリポジトリを更新するという形になります。

とりあえず、上のリンク先をみたりgitについて色々と調べたりして理解してください。
理解できているという前提でフローを書きます（別に理解していなくてもできます）。

### 3. 管理者側
1. master から dev　ブランチを作成
2. プルリクエストが来たらコードレビューする
3. オッケーならプル
4. ある程度まで来たら devブランチからreleaseブランチを作成
5. releaseブランチで色々とリリース用に完成させられたら、masterとdevにプッシュ

### 2. 管理者側
1. dev　ブランチから自分用のブランチ(以下 dev/hoge)を作成
2. dev/hoge　ブランチをローカルにリモートレポジトリからクローン
3. PCのクローンしてきたところでプログラミングする
4. ある程度までプログラミングし終わったら、コミットしてプッシュ (適宜、プルする)
5. 管理者側へプルリクエスト

## 3. gitのこまんど
ブランチ、クローン、プルリク、プッシュ、コミットとか意味わからんとなっているかもしれないけど、
黄にせずに以下のコマンドをうっていけばオッケーです。

### 3. 開発者側
1. devからdev/yourName-hogeを作成
2. PCのどっかにフォルダを作成
3. そのフォルダの中に入る (Terminalで cdで)
4. $ git clone dev/yourName-hogeのブランチのURL
5. すると、作成したフォルダの中に色々なのが入ってる。
6. そこで色々と追加したり編集したりする。
7. Terminalでcdしてcloneして作られたフォルダに入る。
8. $ git branch でdev/yourName-hogeになっているか確認 -> なっていなかったら git checkout dev/yourName-hogeでブランチに接続
9. $ git status で編集、追加、削除されたファイルを確認 -> 差分の確認
10. $ git diff filePath で、そのファイルのどこが変わっているか確認
11. $ git add filePath　で、そのファイルをcommitできる状態にする
12. $ git commit -m "your comment" でcommitできる状態になっているファイルたちをリモートへ更新できる状態にする
13. $ git push origin dev/yourName-hoge　でcommitしたやつらをリモートのdev/yourNamge-hogeブランチの更新をする
14. ある程度できたら、dev/yourname-hogeをdevへプルリクエストする。
