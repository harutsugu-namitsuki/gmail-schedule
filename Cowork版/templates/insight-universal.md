---
# ═══════════════════════════════════════════
# インサイト管理・ユニバーサルメタデータ
# ═══════════════════════════════════════════

title: "[インサイトのタイトル（1行で端的に）]"

# ───── 追跡用タイムスタンプ（必須） ─────
# いつ取り込んだインサイトかを後から追えるようにするため、
# date（論理日付）とは別に captured_at（取込時刻）を明示する。
date: "[YYYY-MM-DD]"                    # インサイトの論理日付（通常は元メールの受信日）
captured_at: "[YYYY-MM-DDTHH:MM:SS+09:00]"  # タスクが本インサイトを生成した実時刻（JST, ISO8601）
source_run_id: "[YYYY-MM-DD-consulting-digest]"  # 同日の日次レポートへの逆引きキー
# ─────────────────────────────────────

status: "未使用"            # NotionのSelect用 / Obsidian検索用

# プラクティス軸カテゴリ（日次レポート セクション3と同じ8分類）
# A_Strategy_CorpFinance | B_Operations_SupplyChain | C_Growth_MarketingSales
# D_People_Organization | E_Technology_Digital_AI | F_Risk_Resilience_Regulation
# G_Sustainability_EnergyTransition | H_Industry_Spotlight
practice: "[A_Strategy_CorpFinance 等の1つ]"

priority: "[High | Medium | Low]"

# C-suiteアジェンダタグ（どの役員の関心事か）
c_suite:
  - "[CEO | CFO | COO | CIO | CTO | CMO | CHRO | CRO | CLO | CSO]"

# 以下の配列は、NotionではMulti-selectに変換しやすく、
# ObsidianではDataview検索でクエリしやすい標準フォーマット
tags:
  - "[タグ1]"
  - "[タグ2]"
industry:
  - "[業界1]"
  - "[業界2]"
firms:
  - "[ファーム1]"
  - "[ファーム2]"

use_case: "[コンサル提案の想定シーン]"

# 情報源（複数可）— メール本体と、その中で参照した記事URLを並列に記載
# 追跡用のタイムスタンプも必ず記録する
sources:
  - type: "email"
    title: "[元メール件名]"
    publisher: "[送信元の組織名のみ]"
    sender_domain: "[bcg.com / email.mckinsey.com など]"  # 特定アドレスは匿名化
    received_at: "[YYYY-MM-DDTHH:MM:SS+09:00]"  # Gmail の受信タイムスタンプ（JST, ISO8601）
    gmail_message_id: "[Gmail 内部ID（あれば。匿名化対象外）]"
  - type: "article"
    title: "[リンク先記事タイトル]"
    url: "[URL]"
    publisher: "[発行元]"
    fetched_at: "[YYYY-MM-DDTHH:MM:SS+09:00]"  # Chrome/Computer Use で取得した実時刻
    access_method: "[chrome_browser | computer_use | manual | failed]"
    extraction_method: "[html_part | gmail_dom | plain_text_regex]"  # タスク定義 手順4-1 の分岐
    access_level: "[full_access | partial_access | no_access]"      # domain-access-levels.json 基準

# 本インサイトで押さえるべき英単語（日次レポート セクション5から引き継ぐ）
key_english_terms:
  - "[word/phrase 1]"
  - "[word/phrase 2]"
---

# [TITLE]

## 💡 インサイト（So What?）

[このファクトから導かれる「示唆」を記述。本文中で`key_english_terms`に含まれる単語が初出する日本語の直後には `（English）` を併記する。例: 資本配分（capital allocation）の規律]

## 📋 ファクト（What happened?）

- [事実1]
- [事実2]

## 📝 原文引用と和訳（Evidence in Original Language）

*※日次レポート セクション4の原文引用を、インサイトDBにも永続化する。将来Notion/Obsidianのどちらに移しても、英語原文が一次エビデンスとして残るようにする。*

> **原文 (EN)**: "[メールまたは記事本文からの重要段落をそのまま引用]"
>
> **和訳 (JA)**: 「[上記段落の日本語訳]」

（引用は記事の骨子理解に必要な範囲に限定。1段落あたり3〜8文程度）

## 🎯 提案活用仮説

- **仮説**: [提案の方向性]
- **想定クライアント/シーン**: [どの業界・どの役員アジェンダに刺さるか]
- **インパクト**: [想定される効果]

---
## 🔗 ナレッジリンク（Obsidian用）
<!--
※ Notion連携時には単なるテキストとして無視されますが、
   Obsidian等のツールで開いた際はこれが「グラフビュー」の結節点（ノード）になります。
-->
関連キーワード: [[プラクティス軸]] / [[C-suiteアジェンダ]] / [[タグ1]] / [[ファーム1]] / [[業界1]]
