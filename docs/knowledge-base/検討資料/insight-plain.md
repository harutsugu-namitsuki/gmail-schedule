# ツール非依存 インサイトテンプレート（プレーン版）

> **設計思想**: 特定のツール（Notion / Obsidian）に依存しない、純粋な Markdown 形式。
> GitHub 上でそのまま閲覧・検索でき、将来どのツールにも移行可能な
> 「最大公約数」フォーマット。grep / GitHub Search で検索できることを重視。
> YAML Frontmatter は残すが、ツール固有の記法（`[[リンク]]` 等）は使わない。

---

## フォーマット仕様

```markdown
---
# ═══════════════════════════════════════════
# インサイト メタデータ（汎用）
# ═══════════════════════════════════════════

title: "[インサイトのタイトル（1行で端的に）]"
id: "[YYYY-MM-DD]-[連番3桁]"
date: "[YYYY-MM-DD]"
status: "未使用"                    # 未使用 / 検討中 / 提案済み / アーカイブ

category: "[Market | Competitor | Technology | Regulation | Client]"
priority: "[High | Medium | Low]"
confidence: "[High | Medium | Low]"

tags: "[タグ1, タグ2, タグ3]"
industry: "[業界1, 業界2]"
firms: "[企業名1, 企業名2]"

use_case: "[活用シーン]"
target_client: "[想定クライアント像]"

source_type: "[Newsletter | Press Release | Report | Article]"
source_title: "[元記事/メールの件名]"
source_url: "[URL]"
source_date: "[YYYY-MM-DD]"

created_at: "[YYYY-MM-DDTHH:MM:SS+09:00]"
updated_at: "[YYYY-MM-DDTHH:MM:SS+09:00]"
linked_report: "[reports/YYYY-MM-DD-consulting-digest.md]"
---

# [TITLE]

**カテゴリ**: `[CATEGORY]` | **重要度**: `[PRIORITY]` | **ステータス**: `[STATUS]`
**タグ**: `[TAG1]` `[TAG2]` `[TAG3]`

---

## 💡 インサイト（So What?）

[このファクトから導かれる「示唆」を2〜3文で記述。]

## 📋 ファクト（What happened?）

- [事実1]
- [事実2]
- [事実3]

## 🎯 提案への活用アイデア

- **提案仮説**: [具体的な提案の方向性]
- **差別化ポイント**: [競合ファームとの差別化要素]
- **想定インパクト**: [定量的な効果仮説]

## 🔗 ソース・参考資料

| # | タイトル | URL | 備考 |
|---|---------|-----|------|
| 1 | [TITLE] | [URL] | [メモ] |

## 📝 活用ログ

| 日付 | アクション | メモ |
|------|-----------|------|
| [YYYY-MM-DD] | 作成 | 自動生成 |
| [YYYY-MM-DD] | [検討開始/提案済み/アーカイブ] | [メモ] |
```

---

## GitHub 上での検索・フィルタリング方法

### GitHub Search（ブラウザ / CLI）

```bash
# リポジトリ内で「生成AI」関連のインサイトを検索
# GitHub Web UI の検索バー、または gh CLI で実行

# 特定タグのインサイトを検索
grep -rl "tags:.*生成AI" insights/

# 未使用の High Priority だけ抽出
grep -rl 'priority: "High"' insights/ | xargs grep -l 'status: "未使用"'

# 特定業界に関連するインサイトを抽出
grep -rl "industry:.*製造" insights/

# 特定ファームに関連するインサイトを抽出
grep -rl "firms:.*マッキンゼー" insights/
```

### インデックスファイルの自動生成（オプション）

`insights/` 配下の全ファイルのメタデータを集約した
`insights/INDEX.md` を定期的に自動生成すると、一覧性が向上する。

```markdown
# 📚 インサイト・インデックス

*最終更新: [YYYY-MM-DD HH:MM]*
*総件数: [N] 件 | 未使用: [N] 件 | High Priority: [N] 件*

## High Priority（未使用）

| ID | タイトル | カテゴリ | 業界 | 日付 |
|----|---------|---------|------|------|
| 2025-07-17-001 | [タイトル] | Technology | 製造 | 2025-07-17 |

## Medium Priority（未使用）

| ID | タイトル | カテゴリ | 業界 | 日付 |
|----|---------|---------|------|------|
| ... | ... | ... | ... | ... |

## 提案済み・アーカイブ

| ID | タイトル | 提案先 | 結果 | 日付 |
|----|---------|-------|------|------|
| ... | ... | ... | ... | ... |
```

---

## 他ツールへの移行方法

### → Notion へ移行する場合
1. YAML Frontmatter を CSV に変換（Python: `yaml` + `csv` モジュール）
2. Notion の「Import → CSV」でデータベースとして取り込み
3. tags フィールドはカンマ区切りなので、Notion の Multi-Select に分割して格納

### → Obsidian へ移行する場合
1. `insights/` フォルダを Obsidian Vault として開く
2. YAML Frontmatter はそのまま Dataview で読み取り可能
3. 必要に応じて `firms` / `industry` のテキスト値を `[[双方向リンク]]` 記法に置換
   （一括置換スクリプトで対応可能）

### → その他のツール（Airtable, Coda, Spreadsheet 等）
1. YAML → CSV 変換スクリプトで出力
2. 各ツールの CSV インポート機能で取り込み
