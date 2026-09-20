---
name: jev-decision
description: Jev（判断モデル）を正しく安全に呼び出すための構造化判定スキル。余計な文脈を排除して単一データと選択肢のみを送信します。
---

# Jev Decision Skill

このスキルは、判断モデル（Jev）に対して内部エラー（500）を起こさずに安全な判定リクエストを投げるための専門手順です。

## 実行ルール・制約
1. **コンテキスト遮断**: プロジェクト全体のファイル（`AGENTS.md` や `docs/` など）をJevの入力に含めてはいけません[cite: 4]。
2. **形式指定**: 判定対象のテキストと、明確な判定選択肢（`enum` または `boolean`）のみを単一テキストとして渡します。
3. **JSON要求**: 出力形式は常に `json_object` スキーマを要求してください。

## 呼び出しテンプレート
Jevを実行する際は、以下の構造のみをプロンプトとして組み立てて実行してください。

```json
{
  "target": "<判定したい文字列・コード片のみ>",
  "choices": ["選択肢A", "選択肢B", "選択肢C"],
  "response_format": "json_object"
}
```

```json
{
  "model": "jev",
  "temperature": 0,
  "messages": [
    {
      "role": "user",
      "content": "以下のコード変更内容について、安全性を判定してください。\n\n【判定対象】\n`git rm -r --cached .obsidian` の実行と .gitignore への追加\n\n【選択肢】\n- SAFE: 安全な変更\n- WARNING: 注意が必要な変更\n- DANGER: 危険な変更"
    }
  ],
  "response_format": {
    "type": "json_object",
    "schema": {
      "type": "object",
      "properties": {
        "judgment": {
          "type": "string",
          "enum": ["SAFE", "WARNING", "DANGER"]
        },
        "reason_code": {
          "type": "string",
          "description": "判定理由の要約（15文字以内）"
        }
      },
      "required": ["judgment", "reason_code"]
    }
  }
}
```
