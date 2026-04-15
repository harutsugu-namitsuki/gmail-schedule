# Obsidian ナレッジグラフ用インサイトテンプレート

> **設計思想**: Obsidian の Dataview プラグインでクエリ可能な YAML Frontmatter +
> `[[双方向リンク]]` によるナレッジグラフ構築を前提とした構造。
> GitHub 上では通常の Markdown として可読、Obsidian で開くと
> グラフビュー・Dataview テーブル・タグ検索がすべて機能する。

---

## フォーマット仕様

```markdown
---
# ═══════════════════════════════════════════
# Obsidian Dataview クエリ対応メタデータ
# ═══════════════════════════════════════════

aliases:
  - "[検索用の別名1]"
  - "[検索用の別名2]"

# --- 基本情報 ---
title: "[インサイトのタイトル]"
id: "[YYYY-MM-DD]-[連番3桁]"
date: [YYYY-MM-DD]
status: "🟢未使用"                # 🟢未使用 / 🟡検討中 / 🔵提案済み / ⚪アーカイブ

# --- 分類（Dataview の WHERE/GROUP BY で使用） ---
category: "[Market | Competitor | Technology | Regulation | Client]"
priority: "[High | Medium | Low]"
confidence: "[High | Medium | Low]"

# --- タグ（Obsidian のタグ検索 + Dataview 対応） ---
tags:
  - "insight"
  - "[カテゴリタグ: 例 AI]"
  - "[業界タグ: 例 製造業]"
  - "[テーマタグ: 例 コスト最適化]"

# --- リンク情報（Obsidian グラフビュー用） ---
related_firms:
  - "[[マッキンゼー]]"
  - "[[BCG]]"
related_industries:
  - "[[製造業]]"
  - "[[小売業]]"
related_insights:
  - "[[YYYY-MM-DD-別のインサイトファイル名]]"

# --- ソース ---
source_type: "[Newsletter | Press Release | Report | Article]"
source_title: "[元記事/メールの件名]"
source_url: "[URL]"
source_date: [YYYY-MM-DD]

# --- 提案活用 ---
use_case: "[活用シーン]"
target_client: "[想定クライアント像]"

# --- メタ ---
created: [YYYY-MM-DDTHH:MM:SS+09:00]
updated: [YYYY-MM-DDTHH:MM:SS+09:00]
linked_report: "[[reports/YYYY-MM-DD-consulting-digest]]"
---

# [TITLE]

## 💡 インサイト（So What?）

[このファクトから導かれる「示唆」を2〜3文で記述。]

> [!tip] 提案への転用ポイント
> [1行で、どのような提案シーンで使えるかを端的に記述]

## 📋 ファクト（What happened?）

- [事実1]
- [事実2]
- [事実3]

## 🎯 提案への活用アイデア

- **提案仮説**: [具体的な提案の方向性]
- **差別化ポイント**: [競合ファームとの差別化要素]
- **想定インパクト**: [定量的な効果仮説]

### 関連するインサイト
- [[YYYY-MM-DD-関連インサイト1]]
- [[YYYY-MM-DD-関連インサイト2]]

## 🔗 ソース・参考資料

| # | タイトル | URL | 備考 |
|---|---------|-----|------|
| 1 | [TITLE] | [URL] | [メモ] |

---

> [!note] ステータス更新ログ
> - [YYYY-MM-DD] 🟢 作成
> - [YYYY-MM-DD] 🟡 〇〇案件で検討開始
> - [YYYY-MM-DD] 🔵 △△クライアントへ提案済み
```

---

## Obsidian での活用方法（将来の移行時）

### セットアップ
1. GitHub リポジトリをローカルに Clone
2. Obsidian で `insights/` フォルダを Vault として開く
3. **Dataview プラグイン**をインストール（Community Plugins）

### Dataview クエリ例

#### 全インサイト一覧（テーブル表示）
````
```dataview
TABLE
  priority AS "重要度",
  category AS "カテゴリ",
  status AS "ステータス",
  use_case AS "活用シーン",
  date AS "日付"
FROM "insights"
WHERE contains(tags, "insight")
SORT priority ASC, date DESC
```
````

#### 特定業界のインサイトだけ抽出
````
```dataview
TABLE title, priority, use_case
FROM "insights"
WHERE contains(related_industries, "[[製造業]]")
AND status = "🟢未使用"
SORT date DESC
```
````

#### 未使用の High Priority インサイト（提案ネタ探し用）
````
```dataview
LIST
FROM "insights"
WHERE priority = "High" AND status = "🟢未使用"
SORT date DESC
LIMIT 10
```
````

### ナレッジグラフの構築
- `related_firms` / `related_industries` / `related_insights` に `[[リンク]]` を使用
- Obsidian のグラフビューで「どのファームの動向が、どの業界と関連しているか」を視覚的に把握
- 例: `[[マッキンゼー]]` → `[[生成AI]]` → `[[製造業]]` のような関連ネットワークが自然に形成される
