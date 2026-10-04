---
title: "Git/GitHubデビュー"
emoji: "🐱"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [CLI, Git, GitHub, VSCode]
published: false
---

> まともな記事を執筆することは今回が初です。Zennブロガーとして精進します。

:::message
**注意**
内容の一部はサークルメンバーのみ参考になることがあります。
:::

# Git/GitHubってなんぞ
## GitHubとは
GitHubはクラウド上でプログラムコードなどのファイルデータを一元管理できるプラットフォーム（PaaS）です。  
GitHubでは、データを管理するために“リポジトリ（Repository）”という箱を作成します。  

- GitHubのイメージ図
```mermaid
flowchart TB
  subgraph Repo["Repository"]
    readme["📝 README"]
  end
  user["👤 user"] --> readme
  index["📄 index.html"] --> Repo
  ignore["📄 .gitignore"] --> Repo
  file["📄 file A,B,C,...etc."] --> Repo
```
> 上図はmermaidという記法で描いた図です。

- GitHubのホームページはコチラ

https://github.co.jp/

## Gitとは
GitはGitHubリポジトリを操作するためのツールです。基本的にコマンド操作（CLI）となります。

- GitHubのホームページはコチラ

https://git-scm.com/

# GIT(Get It Tried)
Git/GitHubを簡単に説明したところで、早速Git/GitHubに挑戦してみましょう。

## GitHubの導入
まずはGitHubアカウントを作成しましょう。GitHubのホームページにアクセスします。  
[GitHubホームページ](https://github.co.jp/)

画面右上の“Sign up”をクリックします。
![GitHubホームページ.png](/images/GitHubホームページ.png)

特段こだわらないのであればGoogleアカウント連携に進みます。
![GitHub_Googleログイン.png](/images/GitHub_Googleログイン.png)

Gmailアドレスを入力します。
![GitHub_Googleログイン_メアド入力.png](/images/GitHub_Googleログイン_メアド入力.png)

Botチェックがあればチェックボックスをクリックします。
![GitHub_Googleログイン_Botチェック.png](/images/GitHub_Googleログイン_Botチェック.png)

パスワードを入力します。
![GitHub_GoogleLogin_input_password.png](/images/GitHub_GoogleLogin_input_password.png)

Gmailに届いた認証コードを入力します。
![GitHub_GoogleLogin_input_authcode.png](/images/GitHub_GoogleLogin_input_authcode.png)

:::message
この後のサインアップ手順は割愛します。
:::

GitHubアカウントのサインアップが完了したら、今度はサインインします。
![GitHub_SignUp.png](/images/GitHub_SignUp.png)

Googleアカウントを選択します。
![GitHub_SignIn.png](/images/GitHub_SignIn.png)

その後はGmailアドレスやパスワード入力を進めていきます。サインインが完了するとGitHubのダッシュボードに遷移します。
![GitHub_Dashboard.png](/images/GitHub_Dashboard.png)
これでGitHubを使用できるようになります。

## Gitのインストール
:::message
今回インストールするGitのバージョンは2.55.0.5です。
:::

GitHubアカウントの作成後はGitをインストールしていきます。[Gitのインストールページ](https://git-scm.com/install/windows)にアクセスします。

“Git for Windows/x64 Setup”をクリックしてexeファイルをダウンロードします。
![Git_Install.png](/images/Git_Install.png)
ダウンロードする場所は任意のフォルダ（基本的にはダウンロードフォルダですが、今回はDドライブ直下）にします。

ダウンロードが完了したら、ブラウザからexeファイルを実行します。
![Git_Exec.png](/images/Git_Exec.png)

実行するとウィザードが表示されます。ライセンス情報が表示されたらNextをクリックします。
![Git_Wizard01.png](/images/Git_Wizard01.png)

コンポーネントの選択画面では、赤枠のチェックを外してください（今回は不要な機能です）。  
その後Nextをクリックします。
![Git_Wizard02.png](/images/Git_Wizard02.png)

次の画面ではNextをクリックします（GitのデフォルトエディタはVimにします）。  
その次の画面では下のラジオボタンをチェックし、テキストボックスが“main”であることを確認します。  
その後Nextをクリックします。
![Git_Wizard03.png](/images/Git_Wizard03.png)

:::message
ここから画面を8つ分全てNextをクリックしてください。
:::



# 参考文献

# 改訂履歴
| Ver. | 更新日 |
| --- | --- |
| 1.0 | 2026/10/05 |

以上