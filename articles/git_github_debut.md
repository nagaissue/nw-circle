---
title: "Git/GitHubデビュー"
emoji: "🐱"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Git, GitHub]
published: true
---

# はじめに
本記事ではGit/GitHubをとりあえず使用できるようにすることを目標に公開します。  
Git/GitHubの概念や使用方法の具体的な説明は割愛します。今後それらも執筆していく所存です。

:::message
**注意**
内容の一部はサークルメンバーのみ参考になることがあります。
:::

# Git/GitHubってなんぞ

## GitHubとは
GitHubはクラウド上でプログラムコードなどのファイルデータを一元管理できるプラットフォーム（PaaS）です。  
このロゴが目印です。
[![GitHub_Logo](https://skillicons.dev/icons?i=github)](https://skillicons.dev)

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

# Git/GitHubのセットアップ
Git/GitHubを簡単に説明したところで、早速Git/GitHubに挑戦してみましょう。  
Git/GitHubが使用できる段階までハンズオン形式で説明します。

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
今回インストールするGitのバージョンは2.56.0です。
:::

GitHubアカウントの作成後はGitをインストールしていきます。[Gitのインストールページ](https://git-scm.com/install/windows)にアクセスします。

“Git for Windows/x64 Setup”をクリックしてexeファイルをダウンロードします。
![Git_Install.png](/images/Git_Install.png)
ダウンロードする場所は任意のフォルダ（基本的にはダウンロードフォルダですが、今回はDドライブ直下）にします。

ダウンロードが完了したら、ブラウザからexeファイルを実行します。
![Git_Exec.png](/images/Git_Exec.png)

実行するとウィザードが表示されます。ライセンス情報が表示されたらNextをクリックします。
![Git_Wizard01.png](/images/Git_Wizard01.png)

インストール先はDドライブ直下を指定します。
その後Nextをクリックします。
![Git_Wizard02.png](/images/Git_Wizard02.png)

コンポーネントの選択画面では、チェックを全て外してください。  
その後Nextをクリックします。
![Git_Wizard03.png](/images/Git_Wizard03.png)

:::message
2つほど画面をスキップします（Nextをクリックしてください）。
:::

デフォルトのブランチ名はmainに指定します。その後Nextをクリックします。
![Git_Wizard04.png](/images/Git_Wizard04.png)

:::message
ここから画面を8つほどスキップします（Nextをクリックしてください）。
:::

InstallをクリックしてGitのインストールを開始します。
![Git_Wizard05.png](/images/Git_Wizard05.png)

インストールが開始されます。
![Git_Wizard06.png](/images/Git_Wizard06.png)

インストールが完了したらFinishをクリックしてインストールを終了します（View Release Notesはチェックを外して構いません）。
![Git_Wizard07.png](/images/Git_Wizard07.png)
これでGitを使用できるようになります。

:::message
サークルでGitを使用する場合は、PCの再起動ごとにGitを再インストールする必要があります。  
（ポータブル版Gitならその必要ないのでは？と思われるかもしれませんが、今はご容赦願います。）
:::

## 補足
上記手順をクリアしたメンバーはGitHubアカウントの初期ユーザ名を教えてください。  
私がフォローします。

# 改訂履歴
| Ver. | 更新日 |
| --- | --- |
| 1.0 | 2026/10/05 |

以上