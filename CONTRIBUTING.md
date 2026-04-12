# pijack-templates への貢献

日本語プロンプトインジェクション攻撃テンプレートライブラリへの貢献を歓迎します。
新しい攻撃パターンを発見した場合は、PR を送ってください。

---

## テンプレート追加手順

### 1. フォークと環境準備

```bash
git clone https://github.com/<your-username>/pijack-templates
cd pijack-templates
```

### 2. YAML ファイルの作成

`templates/ja/` または `templates/en/` の適切なカテゴリに YAML ファイルを作成します。

ファイル名: `<attack-slug>-v1.yaml`

#### 必須フィールド

```yaml
id: <globally-unique-id>
name: "攻撃名（日本語可）"
description: |
  攻撃の概要。何を悪用しているか、なぜ危険かを記述。
severity: critical | high | medium | low
category: role-injection | bypass | indirect | social-engineering | data-exfil | multi-turn
language: ja | en

payloads:
  - id: <payload-id>
    description: "このペイロードの説明"
    input: |
      実際の攻撃文字列
    expected_bypass: true | false
    detection_hint: "検出すべきパターンの説明"

detection:
  should_flag: true | false
  min_risk_level: critical | high | medium | low
  relevant_patterns:
    - "パターン1"

integration_test:
  endpoint: "https://jpi-guard.nexus-api-lab.workers.dev/v1/analyze"
  expected_fields:
    - is_injection: true
    - risk_level: ["medium", "high", "critical"]

metadata:
  author: "<GitHub username>"
  created_at: "YYYY-MM-DD"
  version: "1.0.0"
```

### 3. 手動テスト（推奨）

```bash
npx pijack test https://your-rag-app.example.com \
  --template templates/ja/bypass/your-template-v1.yaml
```

または直接 API 呼び出し:

```bash
curl -X POST https://jpi-guard.nexus-api-lab.workers.dev/v1/analyze \
  -H "Content-Type: application/json" \
  -d '{"text": "<攻撃ペイロード>"}'
```

### 4. PR 送信

PR タイトル: `[template] <attack-slug> - <short description>`

---

## 報酬プログラム（Bounty）

| ティア | 条件 | 報酬 |
|---|---|---|
| **Tier 1 — Bypass** | jpi-guard の `is_injection: false` を実際に引き出せる新規攻撃パターン | ¥5,000 Amazon ギフトカード または GitHub Sponsors + Hall of Fame 掲載 |
| **Tier 2 — New Template** | ユニークな攻撃ベクター、手動テスト済み | nexus-api-lab ステッカーパック + 公式ブログ記事 |
| **Tier 3 — Improvement** | 既存テンプレートのバリアント追加・説明強化 | 謝辞掲載 |

---

## 行動規範

- 悪意ある目的でのテンプレート使用を禁止します
- 実在するサービスへの無断テストは禁止です
- テンプレートは防御・研究目的に限定して使用してください

## 連絡先

Issues または [support@nexus-api-lab.com](mailto:support@nexus-api-lab.com)
