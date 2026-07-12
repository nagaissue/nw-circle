---
title: "Cisco CLI設定コマンド一覧"
emoji: "🌐"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["nwcircle"]
published: true
---

## 基本設定

### ユーザEXECモード

| モード | 機能 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|---|
| `Router>` | 特権EXECモードへ移行 | `enable` | | |

### 特権EXECモード

| モード | 機能 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|---|
| `Router#` | 設定表示 | `show running-config` | `sho run` | |
| | 設定の保存 | `copy running-config startup-config` | `cop run sta` | |
| | 通信確認 | `ping [宛先IPアドレス]` | | 例：ping 192.168.0.1 |
| | IPv4インタフェース状態確認 | `show ip interface brief` | `sho ip int b` | |
| | インタフェース詳細確認 | `show interface [インタフェース名]` | `sho int [インタフェース名]` | 例：sho int gi0/0 |
| | IPv4ルーティングテーブル確認 | `show ip route` | `sho ip rou` | |
| | 隣接機器の情報を表示 | `show cdp neighbors` | `sho cdp nei` | |
| | グローバルコンフィグレーションモードへ移行 | `configure terminal` | `conf t` | |

### グローバルコンフィグレーションモード

| モード | 機能 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|---|
| `Router(config)#` | DNS名前解決の無効化 | `no ip domain-lookup` | | ※最初に設定することを推奨 |
| | ホスト名の設定 | `hostname [ホスト名]` | | 例：hostname R1 |
| | イネーブルパスワードの設定 | `enable password [パスワード]` | `ena pas [パスワード]` | 本階層の移行時に要求される |
| | IPv6ルーティング有効化 | `ipv6 unicast-routing` | | IPv6を使用する際は必須 |
| | ラインコンフィグレーションモードへ移行 | `line console 0` | `lin con 0` | |
| | インタフェースコンフィグレーションモードへ移行 | `interface [インタフェース名]` | `int [インタフェース名]` | 例：int gi0/0 |
| | ルーティングプロトコルコンフィグレーションモードへ移行 | `router [プロトコル名]` | | 例：router rip |
| | DHCPコンフィグレーションモードへ移行 | `ip dhcp pool [任意のプール名]` | `ip dh p [任意のプール名]` | 例：ip dhcp pool 1 |

### ラインコンフィグレーションモード

| モード | 機能 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|---|
| `Router(config-line)#` | コンソールパスワード設定 | `password [パスワード]` | `pass [パスワード]` | |
| | 自動ログアウト機能の無効化 | `exec-timeout 0 0` | | |
| | コマンド入力の割込みを有効化 | `logging synchronous` | `logg→Tabキーx2` | |
| | 特権EXECモードの常時アクセス許可 | `privilege level 15` | `priv→Tabキー→15` | ログイン直後から特権EXECモード |

## アドレッシング

### インタフェースコンフィグレーションモード

| モード | 機能 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|---|
| `Router(config-if)#` | インタフェース有効化 | `no shutdown` | `no sh` | |
| | IPv4アドレッシング | `ip address [IPv4アドレス] [サブネットマスク]` | | 例：ip add 192.168.0.1 255.255.255.0 |
| | 説明文の記述 | `description [コメント]` | `des [コメント]` | 地味に大事 |

## RIPルーティング

### ルーティングプロトコルコンフィグレーションモード

| モード | 機能 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|---|
| `Router(config-router)#` | ルーティングするネットワークを指定 | `network [ネットワークアドレス]` | | network 192.168.0.0 |
| | RIPv2有効化 | `version 2` | | |
| | デフォルトルートの設定 | `ip route 0.0.0.0 0.0.0.0 [隣接インタフェースのIPアドレスまたはインタフェース名]` | | |

## OSPFルーティング

| 現在のモード | コマンド | コマンド補完 | コマンド例 | 機能 | 備考 |
|---|---|---|---|---|---|
| `Router#` | `configure terminal` | `conf t` | | グローバル設定モードに昇格 | |
| `Router(config)#` | `router ospf [PROCCESS NUMBER]` | `rou o [PROCCESS NUMBER]` | `router ospf 1` | ルーティングプロセスを起動する | |
| `Router(config-router)#` | `network [NETWORK ADDRESS] [WILDCARD MASK] area [AREA NUMBER]` | | `network 192.168.0.0 0.0.0.0 area 0` | ルータプロセスを定義する | |

## DHCP

### DHCPコンフィグレーションモード

| モード | 機能 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|---|
| `Router(dhcp-config)#` | DHCPを有効化するネットワークの指定 | `network [ネットワークアドレス] [サブネットマスク]` | | 例：network 192.168.0.0 255.255.255.0 |
