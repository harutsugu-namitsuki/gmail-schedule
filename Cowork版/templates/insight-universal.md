---
# ═══════════════════════════════════════════
# インサイト管理・ユニバーサルメタデータ
# ═══════════════════════════════════════════

title: "[インサイトのタイトル（1行で端的に）]"
date: "[YYYY-MM-DD]"
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
sources:
  - type: "email"
    title: "[元メール件名]"
    publisher: "[送信元の組織名のみ]"
  - type: "article"
    title: "[リンク先記事タイトル]"
    url: "[URL]"
    publisher: "[発行元]"

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
