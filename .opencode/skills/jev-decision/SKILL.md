---
name: jev-decision
description: Jev（判断モデル）を正しく安全に呼び出すための構造化判定スキル。余計な文脈を排除して単一データと選択肢のみを送信します。
---

# Jev Decision Skill

このスキルは、判断モデル（Jev）に対して内部エラー（500）を起こさずに安全な判定リクエストを投げるための専門手順です。

## 実行ルール・制約
1. **コンテキスト遮断**: プロジェクト全体のファイル（`AGENTS.md` や `docs/` など）をJevの入力に含めてはいけません。`state` には判定したい文字列・コード片のみを入れます。
2. **形式指定**: `state`（単一データ）+ `questions`（型付き質問）のみを送ります。安全性判定は `type: choice` を使い、`criteria` に選択肢と意味を明記します。`boolean` 判定は `type: noul` を使います。
3. **禁止フィールド**: `temperature`、`messages`、`max_tokens`、`stream`、`response_format` を送らないこと。これらがあると `400/422` の原因になります。出力はJev側の型付き `answers`（`choice` + `probabilities` + `confidence`）をそのまま使います。

## 呼び出しテンプレート
エンドポイントは1つのみです。OpenAI互換の `chat/completions` に投げないこと。

```http
POST https://api.typesafe.ai/v1/systemone
Authorization: Bearer $TYPESAFE_API_KEY
Content-Type: application/json
```

```json
{
  "model": "jev-latest",
  "state": "`git rm -r --cached .obsidian` の実行と .gitignore への追加",
  "questions": {
    "safety": {
      "type": "choice",
      "instructions": "このコード変更内容について、安全性を判定してください。",
      "criteria": {
        "SAFE": "安全な変更",
        "WARNING": "注意が必要な変更",
        "DANGER": "危険な変更"
      }
    }
  }
}
```

応答例（抜粋）:

```json
{
  "model": "jev-1.13.0",
  "answers": {
    "safety": {
      "type": "choice",
      "choice": "SAFE",
      "probabilities": { "SAFE": 0.9, "WARNING": 0.08, "DANGER": 0.02 },
      "confidence": 0.85
    }
  },
  "usage": { "input_tokens": 120, "output_tokens": 0 }
}
```

## アクセス
- Waitlistは2026-09-20/21に撤廃済み。`https://console.typesafe.ai/` から直接アカウント作成してAPIキーを発行します（$5無料クレジット付き）。
- モデル名は `jev-latest`（実体 `jev-1.13.0`）を指定。`jev` 単体や `temperature` 付きは使わないこと。
- 代替経路: Vercel AI Gateway `typesafe-ai/jev`、OpenRouter `typesafe/jev-1.13`（専用 `POST /api/alpha/decisions`）。

## エラー対応
- `400/422`: ボディ検証失敗（`state`・`questions`・未知フィールドを確認）
- `401`: APIキー不正
- `429/529`: レート制限・過負荷。`retry-after` に従い指数バックオフで再試行
