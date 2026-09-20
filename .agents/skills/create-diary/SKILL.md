---
name: create-diary
description: Generate a diary entry based on your input
disable-model-invocation: true
---

### 質問内容

> 日本語で質問してください

- What did you do today? | 今日は何をしましたか？
- What did you achieve today? | 今日はどんなことを成し遂げましたか？
- Is there anything you would reflect on? | 反省点はありますか？
- Did you do any strength training? | 筋トレはしましたか？
- How was your health? | 体調はどうでしたか？

> 回答内容は改変しないでください

### 日記の保存方法

- 日記はタイムスタンプを追記して`diaries/`に保存する
- ファイル名の体裁は`diary_YYYYMMDD.md`とする
- `YYYYMMDD`: タイムスタンプであり、YYYYは西暦、MMは月、DDは日を表す
