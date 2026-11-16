---
title: "Cisco Packet Tracer コマンドガイド"
emoji: "🔍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cisco", "cli", "network"]
published: true
---

# Cisco Packet Tracer コマンドガイド

この資料は、[Cisco PT設定コマンド一覧](./pt-commands-guide)をもとに、コマンドを入力するモードや設定の流れ、確認方法を補足した検証用の詳細版です。

> コマンドやインタフェース名は、Packet Tracerで使用する機器の機種・IOSの機能によって異なる場合があります。実機では、授業や管理者の指示に従ってください。

## 1. CLIの基本

### 1.1 コマンド入力画面を開く

Packet Tracerでルータまたはスイッチをクリックし、**CLI**タブを開きます。初回起動時に初期設定ダイアログが表示された場合は、学習で指示された方法を選択します。コマンド入力を始めるときは、プロンプト（入力行の先頭）を確認してください。

### 1.2 モードとプロンプト

Cisco IOSのコマンドは、現在のモードによって入力できるものが異なります。

| モード | プロンプト例 | 主な用途・移動方法 |
|---|---|---|
| ユーザEXEC | `Router>` | 基本的な確認。`enable`で特権EXECへ移動 |
| 特権EXEC | `Router#` | 詳細確認、保存、設定モードへの移動 |
| グローバル設定 | `Router(config)#` | ホスト名やルーティングなど、機器全体の設定 |
| インタフェース設定 | `Router(config-if)#` | IPアドレス、説明、インタフェース有効化 |
| ライン設定 | `Router(config-line)#` | コンソール接続などのログイン設定 |
| ルーティング設定 | `Router(config-router)#` | RIPやOSPFの設定 |
| DHCPプール設定 | `Router(dhcp-config)#` | DHCPで配布するネットワークなどの設定 |

`Router`の部分は、`hostname`で機器名を変更すると変わります。たとえばホスト名を`R1`にすると、グローバル設定モードのプロンプトは`R1(config)#`になります。

### 1.3 よく使うモード移動

```cisco
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# exit
Router(config)# end
Router#
```

- `enable`: ユーザEXECから特権EXECへ移動します。
- `configure terminal`: 特権EXECからグローバル設定モードへ移動します。
- `interface ...`: 指定したインタフェースの設定モードへ移動します。
- `exit`: ひとつ前の階層へ戻ります。
- `end`または`Ctrl+Z`: 設定モードから特権EXECへ戻ります。

`show`、`copy`、`ping`などは通常、特権EXECモードで実行します。設定モードから確認コマンドを使いたい場合は、先頭に`do`を付けられる機種があります（例：`do show ip interface brief`）。対応状況は機種によって異なります。

### 1.4 省略・補完・ヘルプ

コマンドは、ほかのコマンドと区別できる範囲で省略できます。たとえば`configure terminal`は`conf t`と入力できます。ただし、省略形は機種や入力候補によって変わるため、最初は正式なコマンドを使うのがおすすめです。

- `Tab`: 入力中のコマンドやキーワードを補完します。
- `?`: その位置で入力できるコマンド候補や引数を表示します。
- `Ctrl+A` / `Ctrl+E`: 行頭 / 行末へ移動します。
- `Ctrl+C`: 入力中のコマンドを中止します。
- `↑` / `↓`: コマンド履歴をたどります。

## 2. 基本設定

以下はルータの初期設定例です。`[ ]`で囲まれた部分は説明用の置き換え箇所で、角括弧自体は入力しません。

```cisco
enable
configure terminal
hostname R1
no ip domain-lookup
end
```

| コマンド | 入力モード | 説明 |
|---|---|---|
| `hostname [機器名]` | グローバル設定 | プロンプトに表示する機器名を設定 |
| `no ip domain-lookup` | グローバル設定 | 誤入力した文字列をホスト名として検索する動作を止める |
| `ipv6 unicast-routing` | グローバル設定 | ルータでIPv6パケットを転送する場合に有効化 |

### パスワードに関する注意

既存のコマンド一覧には`enable password [パスワード]`がありますが、このコマンドで設定したパスワードは安全に保護されません。学習用Packet Tracerで指示された場合に限って使用し、実環境では組織のセキュリティ方針に従ってください。設定例に実際のパスワードや個人情報を記載しないでください。

## 3. インタフェースとIPアドレス

### 3.1 インタフェース名を確認する

機種によってインタフェース名は異なります。たとえば`GigabitEthernet0/0`、`GigabitEthernet0/0/0`、`FastEthernet0/0`などがあります。次のコマンドで実際の名前と状態を確認します。

```cisco
show ip interface brief
```

`administratively down`は、設定でインタフェースが無効になっている状態です。`down`の場合は、物理リンクや接続先などに問題がある可能性があります。原因を詳しく調べるには、`show interface [インタフェース名]`も確認します。

### 3.2 IPv4アドレスを設定する

例として、`GigabitEthernet0/0`に`192.168.10.1/24`を設定します。

```cisco
enable
configure terminal
interface gigabitEthernet 0/0
description LAN
ip address 192.168.10.1 255.255.255.0
no shutdown
end
show ip interface brief
```

| コマンド | 入力モード | 説明 |
|---|---|---|
| `interface [インタフェース名]` | グローバル設定 | 設定するポートを選択 |
| `description [説明]` | インタフェース設定 | 接続先や用途を記録 |
| `ip address [IPv4アドレス] [サブネットマスク]` | インタフェース設定 | IPv4アドレスとサブネットマスクを設定 |
| `no shutdown` | インタフェース設定 | インタフェースを有効化 |
| `shutdown` | インタフェース設定 | インタフェースを無効化 |

`no shutdown`を入力してもリンクが上がらないときは、ケーブルの種類・接続先ポート・接続先機器の電源やポート状態を確認します。

### 3.3 IPv6アドレスを設定する

IPv6を使う場合は、インタフェースへのアドレス設定に加え、ルータでIPv6転送を有効にします。

```cisco
configure terminal
ipv6 unicast-routing
interface gigabitEthernet 0/0
ipv6 address 2001:db8:10::1/64
no shutdown
end
show ipv6 interface brief
```

`2001:db8::/32`は説明や例示に使うIPv6プレフィックスです。実ネットワークでは割り当てられたアドレスを使用してください。リンクローカルアドレスを明示する場合は、インタフェース設定モードで`ipv6 address [リンクローカルアドレス] link-local`を使います。

## 4. ルーティング

ルータが宛先ネットワークへパケットを転送するには、そのネットワークへの経路が必要です。接続済みのネットワークはインタフェースにIPアドレスを設定すると学習されます。それ以外の経路は、静的ルートまたはルーティングプロトコルで設定します。

### 4.1 静的ルート・デフォルトルート

```cisco
configure terminal
ip route [宛先ネットワーク] [サブネットマスク] [次ホップIPアドレス]
end
show ip route
```

たとえば、`192.168.20.0/24`へ向かう次のルータが`192.168.10.2`の場合：

```cisco
ip route 192.168.20.0 255.255.255.0 192.168.10.2
```

デフォルトルートは、より具体的な経路が見つからない宛先への転送先です。

```cisco
ip route 0.0.0.0 0.0.0.0 [次ホップIPアドレス]
```

次ホップIPには、隣接するルータの到達可能なアドレスを指定します。出力インタフェースだけを指定する書式もありますが、Ethernetのようなマルチアクセスネットワークでは、意図しないARP動作を避けるため、学習時は次ホップIPを指定する方法が分かりやすいです。設定後は`show ip route`で`S`（静的）や`S*`（候補デフォルトルート）の表示を確認します。

### 4.2 RIP version 2

RIPは隣接ルータと経路情報を交換する動的ルーティングプロトコルです。各ルータで、RIPに参加させるネットワークを設定します。

```cisco
configure terminal
router rip
version 2
no auto-summary
network 192.168.10.0
network 192.168.20.0
end
show ip protocols
show ip route
```

| コマンド | 説明 |
|---|---|
| `router rip` | RIPの設定モードへ移動 |
| `version 2` | RIPv2を使用 |
| `no auto-summary` | クラスフルな境界での自動集約を無効化 |
| `network [ネットワークアドレス]` | RIPを有効にするインタフェースが属するネットワークを指定 |
| `show ip protocols` | 動作中のルーティングプロトコルと設定を確認 |

`network`には、ルータに直接接続されているネットワークのアドレスを指定します。このコマンドにより、そのネットワークに属するインタフェースでRIPが有効になります。指定が誤っていると、必要なインタフェースでRIPが動作しません。ルータ間の接続状態と経路を確認し、`show ip route`に`R`で始まる経路が現れるかを見ます。

### 4.3 OSPF

OSPFでは、ルータごとにローカルなプロセス番号を選び、広告するネットワークとエリアを指定します。以下はプロセス番号`1`、エリア`0`の設定例です。

```cisco
configure terminal
router ospf 1
network 192.168.10.0 0.0.0.255 area 0
network 192.168.20.0 0.0.0.255 area 0
end
show ip protocols
show ip ospf neighbor
show ip route
```

`network`コマンドの第2引数はサブネットマスクではなく、ワイルドカードマスクです。サブネットマスクのビットを反転して求めます。たとえば`255.255.255.0`の反転は`0.0.0.255`です。特定インタフェースのアドレスだけを対象にする場合は、`0.0.0.0`を指定できます。

```cisco
network 192.168.10.1 0.0.0.0 area 0
```

OSPFのプロセス番号は、通常、隣接ルータ間で同一である必要はありません。一方、エリアやネットワーク設定などが一致しないと隣接関係が確立しないことがあります。`show ip ospf neighbor`で隣接状態を確認します。

## 5. DHCPサーバー

ルータをDHCPサーバーとして使い、`192.168.10.0/24`の端末へアドレスを配布する例です。ルータ自身など固定で使用するアドレスは、配布対象から除外します。

```cisco
configure terminal
ip dhcp excluded-address 192.168.10.1 192.168.10.20
ip dhcp pool LAN
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.10.53
end
show ip dhcp pool
show ip dhcp binding
```

| コマンド | 入力モード | 説明 |
|---|---|---|
| `ip dhcp excluded-address [開始IP] [終了IP]` | グローバル設定 | DHCPで配布しないアドレス範囲を指定 |
| `ip dhcp pool [プール名]` | グローバル設定 | DHCPプールを作成し、プール設定モードへ移動 |
| `network [ネットワーク] [サブネットマスク]` | DHCPプール設定 | 配布対象ネットワークを指定 |
| `default-router [ルータのIP]` | DHCPプール設定 | クライアントへ通知するデフォルトゲートウェイ |
| `dns-server [DNSのIP]` | DHCPプール設定 | クライアントへ通知するDNSサーバー |
| `show ip dhcp binding` | 特権EXEC | クライアントへの割り当て状況を確認 |

`192.168.10.53`は例示用のDNSアドレスです。Packet Tracer上でDNSサーバーを用意していない場合は、環境に合わせたアドレスに置き換えてください。クライアント側は、IP設定を**DHCP**にしてリースを取得できるか確認します。

## 6. コンソール接続設定

コンソールパスワードを設定する例です。パスワードを要求させるには`login`も必要です。

```cisco
configure terminal
line console 0
password [学習用パスワード]
login
logging synchronous
end
```

| コマンド | 説明 |
|---|---|
| `line console 0` | コンソール回線の設定モードへ移動 |
| `password [パスワード]` | コンソール回線のパスワードを設定 |
| `login` | 接続時に設定済みのパスワードを要求 |
| `logging synchronous` | ログメッセージの表示時に、入力中のコマンドを再表示する |
| `exec-timeout [分] [秒]` | 無操作時にセッションを終了する時間を設定 |

元の一覧にある`exec-timeout 0 0`は自動ログアウトを無効化します。学習環境では便利なことがありますが、実環境では不正利用や離席時の操作を防ぐため、安易に無効化しないでください。

同じく、`privilege level 15`をコンソール回線に設定すると、接続直後から特権レベルの操作が可能になります。権限を制限したい環境には適しません。必要性を理解し、指示がある場合にのみ使用してください。

## 7. 確認・疎通・保存

| コマンド | モード | 確認内容 |
|---|---|---|
| `show running-config` | 特権EXEC | 現在動作中の設定 |
| `show startup-config` | 特権EXEC | 起動時に読み込む保存済み設定 |
| `show ip interface brief` | 特権EXEC | IPv4アドレスとインタフェース状態 |
| `show interface [インタフェース名]` | 特権EXEC | インタフェースの詳細やエラー |
| `show ip route` | 特権EXEC | IPv4ルーティングテーブル |
| `show ip protocols` | 特権EXEC | RIPやOSPFなどの設定・状態 |
| `show cdp neighbors` | 特権EXEC | CDPを利用した隣接Cisco機器情報 |
| `ping [宛先IPアドレス]` | 特権EXEC | 宛先までの基本的な到達性 |

設定を保存するには、特権EXECモードで次を実行します。

```cisco
copy running-config startup-config
```

保存先ファイル名の確認が表示されたら、通常は何も入力せず`Enter`を押します。保存しないままPacket Tracerを閉じたり機器を再起動したりすると、起動時設定に反映されない場合があります。

疎通確認は近い範囲から段階的に行います。

1. `show ip interface brief`で自分のインタフェースが有効か確認する。
2. 直結している相手のIPアドレスへ`ping`する。
3. `show ip route`で宛先ネットワークへの経路を確認する。
4. 目的の端末やサーバーへ`ping`する。
5. 必要に応じて端末のIPアドレス、サブネットマスク、デフォルトゲートウェイ、DNS設定を確認する。

最初の`ping`が失敗しても、ARP解決などのため再試行で成功する場合があります。複数回試し、経路とインタフェースの状態も合わせて判断してください。

## 8. よくある確認ポイント

| 症状 | 確認すること |
|---|---|
| コマンドが拒否される | プロンプトが必要なモードか、コマンドの綴りや引数が正しいか |
| `show`コマンドが使えない | 特権EXECモード（`Router#`）か。設定モードなら`end`で戻る |
| インタフェースが`administratively down` | インタフェース設定モードで`no shutdown`を実行したか |
| インタフェースが`down` | ケーブル、接続ポート、相手側インタフェースの状態 |
| 端末同士で通信できない | IPアドレスとマスク、同一セグメントか、端末の接続先 |
| 別ネットワークへ通信できない | 送信元・宛先双方の経路、デフォルトゲートウェイ、戻り経路 |
| RIPの経路が表示されない | RIPの`network`、`version 2`、`no auto-summary`、接続状態 |
| OSPFの隣接関係ができない | IP到達性、ワイルドカードマスク、エリア、インタフェース状態 |
| DHCPアドレスを取得できない | DHCPプールのネットワーク、除外範囲、ゲートウェイ、クライアント設定 |
| 入力を誤り名前解決が始まった | `Ctrl+Shift+6`で中断できる場合がある。再発防止には`no ip domain-lookup` |

## 9. コマンド早見表

| 目的 | コマンド |
|---|---|
| 特権EXECへ移動 | `enable` |
| グローバル設定モードへ移動 | `configure terminal` |
| 設定を終了して特権EXECへ戻る | `end` |
| 機器名を設定 | `hostname [機器名]` |
| インタフェースを選択 | `interface [インタフェース名]` |
| IPv4アドレスを設定 | `ip address [IPv4アドレス] [サブネットマスク]` |
| IPv6転送を有効化 | `ipv6 unicast-routing` |
| IPv6アドレスを設定 | `ipv6 address [IPv6アドレス/プレフィックス長]` |
| インタフェースを有効化 | `no shutdown` |
| ルートを設定 | `ip route [宛先ネットワーク] [サブネットマスク] [次ホップ]` |
| RIPv2を設定 | `router rip`、`version 2`、`network ...` |
| OSPFを設定 | `router ospf [プロセス番号]`、`network ... [ワイルドカード] area [エリア]` |
| DHCPプールを作成 | `ip dhcp pool [プール名]` |
| 設定を表示 | `show running-config` |
| IPv4インタフェースを確認 | `show ip interface brief` |
| ルーティングテーブルを確認 | `show ip route` |
| 疎通を確認 | `ping [宛先IPアドレス]` |
| 設定を保存 | `copy running-config startup-config` |

## 改訂履歴

| Ver. | 更新日 | 更新内容 |
|---|---|---|
| 1.0 | 2026/11/16 | 初版を作成 |
