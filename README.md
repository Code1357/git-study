# Gitの勉強

- git add コマンドで、リポジトリに変更情報を追加する
  - このことをステージングと言う
- git commit コマンドで、リポジトリのインデックスに追加された変更情報にコメントを付けてコミットできる
- git push コマンドで、ローカルのコミットをリモートのリポジトリに反映させることができる


*git に自分の情報を登録しよう
まずは、自分の名前を git に登録しましょう。
この作業は初期設定ですので、最初に一度だけ行います。

git config --global user.name "あなたの名前"
git config --global user.email あなたのメールアドレス
git config --global core.editor "vim"
あなたの表示名 と あなたのメールアドレス はそれぞれ、あなたの名前とあなたのメールアドレスに変更して 実行してください。そして、自身が利用するエディタを vim に設定してください。

git config --global user.name "Soichiro Yoshimura"
git config --global user.email soichiro_yoshimura@dwango.co.jp
git config --global core.editor "vim"
例としては、このように入力します。

なお、この設定した自分自身の情報は、

git config -l
というコマンドで確認ができます。ここでは、以下のように表示されます。

user.name=Soichiro Yoshimura
user.email=soichiro_yoshimura@dwango.co.jp
core.editor=vim
自分の名前とメールアドレスが登録されたでしょうか。


*ローカルにリポジトリを作ろう
前回は GitHub リポジトリを clone することでローカルリポジトリを作成しました。
今回はまず、ローカルにリポジトリを作りましょう。

まず git-study というプロジェクトディレクトリを用意します。

cd ~/workspace
mkdir git-study
cd git-study
このようにプロジェクトのディレクトリを作成し、そこをカレントディレクトリにします。

git リポジトリを作るためのコマンドは、

git init
です。実行すると、

Initialized empty Git repository in /home/vagrant/workspace/git-study/.git/
と表示されます。これで git リポジトリが完成しました。
内部の処理としては何が起こったかというと、

/home/vagrant/workspace/git-study/.git/
というディレクトリが作成されました。
この .git ディレクトリを丸ごと削除すれば、ローカルリポジトリを消去できます。

*リポジトリに変更を加えてみよう

まだリポジトリは空っぽなので、ファイルを追加し、リポジトリに変更を加えます。

まずはコマンドで README.md というファイルを作成します。

cd ~/workspace/git-study
echo "# Gitの勉強" > README.md
cat README.md
以前に習ったリダイレクトを使って、 README.md ファイルを作っています。 cat README.md コマンドを実行した結果が、

# Git の勉強
と表示されることを確認しましょう。
なお、この README.md は、 GitHub において少し特別なファイルです。
この名前のファイルは、リポジトリのトップページに自動的に表示されるようになるのです。

さて、作成したファイルをリポジトリに追加するときには、 git add コマンドを使います。 add は「足す、追加する」という意味の英単語です。

git add README.md
ですが、ここで注意が必要です。
実はこのコマンド git add だけでは、「ファイルをリポジトリに追加」したことにはなりません。

git add は「ファイルをリポジトリに追加したい」という変更情報を登録するだけのコマンドなのです。
後ほど説明しますが、変更情報を「コミット」して初めて、リポジトリにデータが追加されます。

このように、いったん変更情報を登録することをステージングといいます。
そして変更情報を保持している領域を、インデックスといいます。コミットをする前の舞台というわけです。

なお、現在の変更情報の登録（ステージング）状況は次のコマンドで確認できます。

git status
実際に実行してみましょう。

On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   README.md
と表示されたでしょうか。
README.md ファイルが、コミット時に追加されるよう登録済み、という表示です。

では、この追加という変更情報をリポジトリにコミットしましょう。

git commit -m "はじめてのコミット"
git commit には必ずコミットコメント（メッセージ）を付ける必要があります。-m オプションに続けて、コメントを記載しましょう。

これでコミットが行われ、リポジトリにデータが登録されました。
このコミットログを確認するためには、

git log
というコマンドを利用します。 以下のようなコミットログが表示されます。

commit fa28e7c3f9a6f30e320275c48ff069a55e322fdf
Author: Soichiro Yoshimura <soichiro_yoshimura@dwango.co.jp>
Date:   Tue Nov 19 09:58:33 2020 +0000

はじめてのコミット
このように先ほど入力したコメントが表示されたら、コミットに成功しています。



*変更を GitHub に置こう

ここまでは、ローカルリポジトリで作業していました。 これを GitHub に置くためには、 GitHub にも新たにリポジトリを作る必要があります。

GitHub のトップページにアクセスして、「 New 」ボタンをクリックします。



*これでリポジトリが完成しました。

https://github.com/あなたのusername/git-study
以上の URL にアクセスします。

まず、「 Quick setup 」の欄の中にある「 HTTPS 」と「 SSH 」のいずれかを選択する箇所で、「 SSH 」をクリックします。


そして

…or push an existing repository from the command line
と書いてある項目があるので、それをそのままコピーして実行します。



ここでの例は、

git remote add origin git@github.com:自分のGitHubアカウント名/git-study.git
git push -u origin master
こうなっています。あなたのusername の部分は、あなたの GitHub アカウント名になっているはずです。

git remote add origin git@github.com:自分のGitHubアカウント名/git-study.git
1 行目のこのコマンドは「リモートリポジトリの origin は、この GitHub のアドレスのリポジトリを指すことにするよ」という設定です。

git push -u origin master
2 行目のこちらは push コマンドです。前回、リモートのリポジトリから変更を取得することを pull と習いましたが、 ローカルの変更をリモートに適用することを push といいます。英語で「押す」という意味ですね。
-u というオプションは、次回以降 origin と master を省略した時に、自動でこの値とするためのものです。

実行できたでしょうか。

Counting objects: 3, done.
Writing objects: 100% (3/3), 264 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:Soichiro-Yoshimura/git-study.git
* [new branch]      master -> master
Branch master set up to track remote branch master from origin.
このように表示されれば成功です。

https://github.com/あなたのusername/git-study
以上の URL にアクセスしてみましょう。
開いたページに「Git の勉強」と書かれた見出しが表示されていれば成功です。

ここまでのイメージを図にまとめると次のようになります。

ここでは、まだインデックスにステージングされていないファイル変更のことをワークツリーと呼んでいます。
インデックスは、英語では index 。 ワークツリーは、英語では working tree と呼びます。
これが Git における変更のやり取りの全体像です。


*タグを使ってみよう

タグとは、荷物などにつけるタグと同じで、特定のコミットの状態に別の名前をつけることをいいます。
git tag タグ名 という形式でコマンドを実行することで、タグが作成されます。

タグは、 GitHub において特定のバージョンのソフトウェアをリリースするために使われます。

ここでは、

git tag 1.0
として、 1.0 という数字のバージョンをタグとしてつけてみましょう。

さらに、タグを GitHub のリポジトリにも反映させるためには、

git push --tags origin master
と入力します。 --tags というオプションが、タグを push する際のオプションとなります。

git tag 1.0
git push --tags origin master
と入力して

Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:Soichiro-Yoshimura/git-study.git
* [new tag]         1.0 -> 1.0
と表示されれば成功です。

https://github.com/あなたのusername/git-study
を再度表示して、 release タブを選択してみましょう。

すると、先ほどタグをつけたバージョンが、 zip などでダウンロードできるページが自動的に作られます。

以上で、ローカルのリポジトリで編集を行い、GitHub のリモートリポジトリへ反映させることができました。


*まとめ

git add コマンドで、リポジトリに変更情報を追加する
このことをステージングと言う
git commit コマンドで、ステージングされた情報にコメントを付けてコミットできる
git push コマンドで、ローカルのコミットをリモートのリポジトリに反映できる
練習

README.md の内容を、

# Git の勉強

- git add コマンドで、リポジトリに変更情報を追加する
  - このことをステージングと言う
- git commit コマンドで、リポジトリのインデックスに追加された変更情報にコメントを付けてコミットできる
- git push コマンドで、ローカルのコミットをリモートのリポジトリに反映させることができる
と変更し、コミットメッセージを「内容を追加」にしてコミットしましょう。
そして、GitHub にも push してみましょう。


*vim README.md
以上のように Vim を使うか、あるいは VS Code を用いてファイルを編集します。その後、

git status
git add README.md
git commit -m "内容を追加"
git push origin master
以上のコマンドで、GitHub に変更が適用されます。

