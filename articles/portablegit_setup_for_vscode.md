---
title: "Portable GitをVS Codeにセットアップしてみる"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Git, vscode]
published: true
---

# 1. はじめに

## 執筆目的
最近サークルでGit/GitHubを学習し始めましたが、本校ではPC再起動の度にGitを再インストールする必要があります  
ですので、その手間を省くためにPortable Gitを導入しようということで、VS Codeの設定と共に学習しようと考えました

## 対象読者
ネットワークサークルメンバー  
VS CodeでGitを使用しているが、Portable版Gitに乗り換えたい方

# 2.Portable Gitのインストール

このURLにアクセスします↓
https://git-scm.com/install/windows

`Git for Windows/x64 Portable.`をクリックして、任意のフォルダにexeファイルをダウンロードします  
（今回はDドライブを指定します）
![setup01.png](/images/portablegit_setup_for_vscode/setup01.png)

ダウンロードが完了したら、exeファイルをクリックして実行します
![setup02.png](/images/portablegit_setup_for_vscode/setup02.png)

実行するとこのような画面（ウィザード）が表示されます
![setup03.png](/images/portablegit_setup_for_vscode/setup03.png)

インストールパス（場所）は今回Dドライブ直下に指定します、PortableGitフォルダは新規作成されます  
入力後に`OK`をクリックします
:::message
画面右の3点マーカは動作しない恐れがあります、その場合はパスを直接指定します
:::
![setup04.png](/images/portablegit_setup_for_vscode/setup04.png)

インストールが開始されます
![setup05.png](/images/portablegit_setup_for_vscode/setup05.png)
完了すると画面が閉じます

Dドライブ直下にこのフォルダが作成されます
![setup06.png](/images/portablegit_setup_for_vscode/setup06.png)
フォルダ内はこんな感じです
![setup07.png](/images/portablegit_setup_for_vscode/setup07.png)

:::message
これでPortable Gitのインストールは完了です
:::

# 3. VS CodeへのPortable Gitセットアップ

既にVS Codeがインストールされていますので、Windowsキーをクリックして`VS Code`と入力してください
![setup08.png](/images/portablegit_setup_for_vscode/setup08.png)

VS Codeが起動しましたら、画面左下の歯車アイコンをクリックします
![setup09.png](/images/portablegit_setup_for_vscode/setup09.png)
`設定`をクリックします
![setup10.png](/images/portablegit_setup_for_vscode/setup10.png)

上の検索欄に`git: path`と入力し、`settings.jsonで編集`をクリックします
![setup11.png](/images/portablegit_setup_for_vscode/setup11.png)

JSON形式の設定ファイルが編集モードで表示されます（既存の設定が数行あります）
![setup12.png](/images/portablegit_setup_for_vscode/setup12.png)

既存の設定に次のコードを追記してください
```json
{
    "terminal.integrated.profiles.windows": { // Windows環境での統合ターミナルのプロファイル設定
        "Portable Git Bash": { // プロファイル名を「Portable Git Bash」に設定
            "path": [
                "D:\\PortableGit\\bin\\bash.exe"
            ],
            "args":["--login", "-l"],
            "icon": "terminal-bash",
            "env": { // 環境変数の設定
                "GIT_CONFIG_GLOBAL": "Z:\\PortableGit\\.gitconfig",
            }
        }
    },
    "git.path": "D:\\PortableGit\\cmd\\git.exe",
    "git.configLocation":  "Z:\\PortableGit\\.gitconfig",
}
```

:::message
既に`git.path`等のコードがあれば削除してください
:::
:::message
設定内のファイルパスが`D:\\`と`Z:\\`で異なる箇所があるので注意してください
:::

次に`Z:\\PortableGit`フォルダを新規作成し、`.gitconfig`ファイルを作成します  
エクスプローラを起動し、`Z:\\PortableGit`フォルダに移動して右クリック→`新規作成`→`テキスト ドキュメント`をクリックします
![setup14.png](/images/portablegit_setup_for_vscode/setup14.png)
ファイル名を全選択し、`.gitconfig`と入力してEnterキーをクリックします
![setup15.png](/images/portablegit_setup_for_vscode/setup15.png)
警告が表示されますが、`はい`をクリックします
![setup16.png](/images/portablegit_setup_for_vscode/setup16.png)

ここからはVS Codeを使用していきます  
VS Codeの起動画面を操作している（アクティブにしている）状態で`Ctrl`キーを押しながら`K`→`O`と順に押します  
するとフォルダの選択画面が表示されます  
そこでZドライブに移動して`PortableGit`をクリックし、`フォルダーの選択`をクリックしてください
![setup17.png](/images/portablegit_setup_for_vscode/setup17.png)

`Z:\\PortableGit\\`に移動することができます
![setup18.png](/images/portablegit_setup_for_vscode/setup18.png)

:::message
フォルダを閉じるときは`Ctrl`キーを押しながら`K`、その後`F`を押します
:::

フォルダ内にある`.gitconfig`をクリックしてファイルを展開します
![setup19.png](/images/portablegit_setup_for_vscode/setup19.png)
ファイルに次のサンプルコードをコピー&ペーストしてください
```json
[user]
    name = taro
    email = hogehoge@example.com
```
:::message
`name`はGitHubのユーザ名、`email`は([このURL](https://github.com/settings/emails))にアクセスし、プライベートに用意されたemailアドレスを入力してください
![setup20.png](/images/portablegit_setup_for_vscode/setup20.png)
:::
:::message
`.gitconfig`をDドライブに作成すると、使用PCを変更するときに自分以外の設定が適用されてしまうためZドライブに作成します
:::

入力後は`Ctrl`キー + `S`で保存してください  
設定後のサンプルがこちらです
![setup21.png](/images/portablegit_setup_for_vscode/setup21.png)

これで設定は完了です、最後に設定が反映されたか確認します

VS Codeのスタート画面で`Ctrl`キー + `@`を押します  
すると画面下部にターミナル画面が表示されます
![setup22.png](/images/portablegit_setup_for_vscode/setup22.png)
右上のトグルリストをクリックし、`Portable Git Bash`をクリックします
![setup23.png](/images/portablegit_setup_for_vscode/setup23.png)
プロンプトに`git config --global user.name`を実行、次に`git config --global user.email`を実行し、先ほど設定した`user`と`email`が出力されれば設定成功です




# 改訂履歴
| Ver. | 更新日 | 更新内容 |
| --- | --- | --- |
| 1.0 | 2026/10/19 | 本記事を初公開 |
| 1.1 | 2026/10/21 | トピックスをPortableGitからGitに変更 |
| 1.2 | 2026/10/26 | 前回の改訂履歴の追記、Portable Gitのダウンロードパス明記、不要なメッセージブロックの削除、`settings.json`手順の全コピー化およびペースト後表示の削除 |
| 1.3 | 2026/10/27 | 対象読者の追記、設定手順の見直し、`.gitconfig`の保存先をZドライブに変更 |
| 1.4 | 2026/10/27 | ターミナルのプロファイル名を「Portable Git Bash」に修正 |

以上