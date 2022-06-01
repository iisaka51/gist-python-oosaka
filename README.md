# gist-python-osaka

ドキュメント共有サービス [Gist](https://gist.github.com/) で資料を公開。’
それを github でプロジェクトとして管理してみる。

## github への公開鍵を登録

github に公開鍵を登録しておきます。

```bash
$ ssh-keygen -f ~/.ssh/github_rsa -t rsa -b 4096 -C "YOUR_EMAIL_ADDRESS"
```

GitHub Docs の [Add a new SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) を参考に登録しておきます。

## SSHの config を設定

$HOME/.ssh/config の先頭に以下を挿入します。

```
Host github.com
  IdentityFile ~/.ssh/github_rsa

Host gist.github.com
  IdentityFile ~/.ssh/github_rsa
```

接続確認
sshコマンドでテスト接続を実行して、次のようなメッセージが表示されればOKです。


```bash
$ ssh -T git@github.com
Hi iisaka51! You've successfully authenticated, but GitHub does not provide shell access.

$ ssh -T git@gist.github.com
Hi iisaka51! You've successfully authenticated, but GitHub does not provide shell access.

```


## gist を github のレポジトリのサブモジュールとして登録

Gist のURLにあるハッシュキーを使って、次のようにサブモジュールとして登録します

PythonOsaka の gist のURLは次のものです。

```
https://gist.github.com/iisaka51/dab73746bdad509e69ae0fab554e86bb/02d882ec454ed116babac6813dbfd3adf1df5398
```

この場合は、次のように実行します。


```bash
$ git submodule add git@gist.github.com:ハッシュキー.git 任意のディレクトリ名
```

実際の例:

```bash
$ git submodule add git@gist.github.com:dab73746bdad509e69ae0fab554e86bb.git python-osaka
```

これで、github のレポジトリ https://github.com/iisaka51/gist-python-osaka として
Gistのドキュメントを管理するとができます。

## レポジトリをクローン

共同で資料作成する場合は、はじめにレポジトリをクローンします。

```bash
$ git clone --recurse-submodules https://github.com/iisaka51/gist-python-osaka
```

あとは、通常のソースコード管理と同じですね。


## ScrapBox から資料を抜き出す

[sb2md](https://github.com/kondoumh/sb2md) を使うと
ScrapBox の資料が Markdown に変換されて表示されます。

```bash
$ sb2md "PythonOsaka/伝言板&ChangeLog"  > 01_ChangeLog.md
```

既知の問題としは次のものがあります。

- ScrapBox の "[ドキュメント名]" の表記がうまくリンクにしてくれない


