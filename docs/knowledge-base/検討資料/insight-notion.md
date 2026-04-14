# Notion DB 連携用インサイトテンプレート

> **設計思想**: Notion の「データベースインポート（CSV）」機能に直結する構造。
> YAML Frontmatter のキー名がそのまま Notion のプロパティ（カラム）名になる。
> GitHub Actions 等で YAML → CSV 変換 → Notion API 投入のパイプラインが組める。

---

## フォーマット仕様

```markdown
---
# ═══════════════════════════════════════════
# Notion DB プロパティ（カラム）に直接マッピング
# ═══════════════════════════════════════════

# --- 基本情報 ---
title: "[インサイトのタイトル（1行で端的に）]"
id: "[YYYY-MM-DD]-[連番3桁]"
date: "[YYYY-MM-DD]"
status: "未使用"                    # 未使用 / 検討中 / 提案済み / アーカイブ

# --- 分類・タグ（Notion の Multi-Select にマッピング） ---
category: "[Market | Competitor | Technology | Regulation | Client]"
tags:
  - "[タグ1: 例 生成AI]"
  - "[タグ2: 例 小売業界]"
  - "[タグ3: 例 コスト最適化]"
industry:
  - "[対象業界1: 例 製造]"
  - "[対象業界2: 例 小売]"
firms:
  - "[関連ファーム/企業名1]"
  - "[関連ファーム/企業名2]"

# --- 重要度（Notion の Select にマッピング） ---
priority: "[High | Medium | Low]"
confidence: "[High | Medium | Low]"  # 情報の確度

# --- 提案活用情報 ---
use_case: "[このインサイトをどの種類の提案に使えるか: 例 DX戦略提案 / コスト削減提案]"
target_client_profile: "[想定クライアント像: 例 製造業の経営企画部門]"

# --- ソース情報 ---
source_type: "[Newsletter | Press Release | Report | Article | Internal]"
source_title: "[元記事/メールの件名]"
source_url: "[URL]"
source_date: "[YYYY-MM-DD]"

# --- メタ情報 ---
created_at: "[YYYY-MM-DDTHH:MM:SS+09:00]"
updated_at: "[YYYY-MM-DDTHH:MM:SS+09:00]"
linked_report: "[reports/YYYY-MM-DD-consulting-digest.md]"
---

## 💡 インサイト（So What?）

[このファクトから導かれる「示唆」を2〜3文で記述。
「〇〇業界では△△の動きが加速しており、□□を持つ企業にとっては
◇◇という新たな課題／機会が生じている」のような形式。]

## 📋 ファクト（What happened?）

[元となった事実を箇条書きで3〜5点。]

- [事実1]
- [事実2]
- [事実3]

## 🎯 提案への活用アイデア（How to use?）

[このインサイトをコンサルティング提案にどう転用できるか。具体的な仮説を記述。]

- **提案仮説**: [例: 「〇〇業界のクライアントに対し、△△ソリューションの導入を提案できる」]
- **差別化ポイント**: [例: 「競合ファームはまだこの領域に手を出しておらず、先行者利益が取れる」]
- **想定インパクト**: [例: 「年間コスト XX% 削減 / 売上 XX% 向上の仮説」]

## 🔗 関連リンク・参考資料

| # | タイトル | URL | 備考 |
|---|---------|-----|------|
| 1 | [TITLE] | [URL] | [メモ] |
```

---

## Notion インポート手順（将来の移行時）

1. **方法A: CSV 変換 → 一括インポート**
   - `insights/` 配下の全 `.md` ファイルの YAML Frontmatter を抽出
   - CSV に変換（Python スクリプト等）
   - Notion の「Import → CSV」でデータベースとして取り込み
   - 本文（Markdown部分）は各レコードのページ内テキストとして格納

2. **方法B: Notion API による自動連携**
   - GitHub Actions で Push を検知
   - `notion-sdk-py` 等で Notion DB に自動登録
   - YAML のキー名 → Notion プロパティ名が1対1で対応する設計

### Notion DB カラム設計（推奨）

| プロパティ名 | Notion タイプ | YAML キー |
|---|---|---|
| タイトル | Title | `title` |
| 日付 | Date | `date` |
| ステータス | Select | `status` |
| カテゴリ | Select | `category` |
| タグ | Multi-Select | `tags` |
| 業界 | Multi-Select | `industry` |
| 関連企業 | Multi-Select | `firms` |
| 重要度 | Select | `priority` |
| 確度 | Select | `confidence` |
| 活用シーン | Rich Text | `use_case` |
| ソース種別 | Select | `source_type` |
| ソースURL | URL | `source_url` |
