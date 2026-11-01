---
title: "Cisco PT設定コマンド一覧"
emoji: "🔍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cisco", "cli", "network"]
published: true
---

Cisco Packet Tracerでよく使う設定・確認コマンドを、目的別にまとめています。
設定コマンドは、必要に応じて `configure terminal` で設定モードに移行してから実行してください。

## 基本設定

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| 特権EXECモードへ移行 | `enable` | `ena` | |
| 設定モードへ移行 | `configure terminal` | `conf t` | 特権EXECモードから実行 |
| DNS名前解決の無効化 | `no ip domain-lookup` | | コマンドの誤入力による名前解決待ちを防ぐ |
| ホスト名の設定 | `hostname [ホスト名]` | `hos [ホスト名]` | 例：`hostname R1` |
| イネーブルパスワードの設定 | `enable password [パスワード]` | `ena pas [パスワード]` | 特権EXECモードへの移行時に要求される |
| IPv6ルーティングの有効化 | `ipv6 unicast-routing` | `ipv u` | IPv6を使用する際に設定 |

## IPv4アドレッシング

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| インタフェースの選択 | `interface [インタフェース名]` | `int [インタフェース名]` | 例：`int gi0/0` |
| IPv4アドレスの設定 | `ip address [IPv4アドレス] [サブネットマスク]` | `ip add` | 例：`ip add 192.168.0.1 255.255.255.0` |
| インタフェースの有効化 | `no shutdown` | `no sh` | |
| インタフェースの説明設定 | `description [コメント]` | `des [コメント]` | 接続先などを記述 |
| IPv4インタフェース状態の確認 | `show ip interface brief` | `sho ip int b` | |

## RIPルーティング

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| RIPの起動 | `router rip` | `rou rip` | |
| RIPv2の有効化 | `version 2` | | |
| RIPで通知するネットワークの指定 | `network [ネットワークアドレス]` | | 例：`network 192.168.0.0` |

## OSPFルーティング

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| OSPFプロセスの起動 | `router ospf [プロセス番号]` | `rou o [プロセス番号]` | 例：`router ospf 1` |
| OSPFで通知するネットワークとエリアの指定 | `network [ネットワークアドレス] [ワイルドカードマスク] area [エリア番号]` | | 例：`network 192.168.0.0 0.0.0.0 area 0` |

## 静的ルート・デフォルトルート

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| デフォルトルートの設定 | `ip route 0.0.0.0 0.0.0.0 [隣接インタフェースのIPアドレスまたはインタフェース名]` | | |

## DHCP

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| DHCPプールの作成 | `ip dhcp pool [プール名]` | `ip dh p [プール名]` | 例：`ip dhcp pool LAN` |
| DHCPで割り当てるネットワークの指定 | `network [ネットワークアドレス] [サブネットマスク]` | | 例：`network 192.168.0.0 255.255.255.0` |

## コンソール設定

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| コンソール回線の選択 | `line console 0` | `lin con 0` | |
| コンソールパスワードの設定 | `password [パスワード]` | `pass [パスワード]` | |
| パスワード認証の有効化 | `login` | | 設定したパスワードで認証する |
| 自動ログアウトの無効化 | `exec-timeout 0 0` | | |
| コマンド入力の割込みを抑制 | `logging synchronous` | `logg` の後にTabキーを2回 | |
| ログイン直後から特権EXECモードにする | `privilege level 15` | `priv` の後にTabキー、続けて `15` | |

## 確認・保存・疎通確認

| 目的 | コマンド | 省略・補完 | 備考 |
|---|---|---|---|
| ルーティングテーブルの確認 | `show ip route` | `sho ip rou` | |
| 設定の表示 | `show running-config` | `sho run` | |
| インタフェース詳細の確認 | `show interface [インタフェース名]` | `sho int [インタフェース名]` | 例：`sho int gi0/0` |
| 隣接機器の確認 | `show cdp neighbors` | `sho cdp nei` | |
| 宛先への疎通確認 | `ping [宛先IPアドレス]` | | 例：`ping 192.168.0.1` |
| 設定の保存 | `copy running-config startup-config` | `cop run sta` | |

## 改訂履歴
| Ver. | 更新日 | 更新内容 |
| --- | --- | --- |
| 1.0 | 2026/10/03 | 初版作成 |
| 1.1 | 2026/11/02 | 目的別のコマンド集に内容を整理 |
