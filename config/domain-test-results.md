# ドメイン WebFetch テスト結果

テスト実施日: 2026-04-14

## テスト概要

5つの主要コンサルティング・ビジネス系ドメインに対して WebFetch テストを実施した。

---

## 詳細結果

### 1. mckinsey.com

| 項目 | 結果 |
|---|---|
| **URL** | https://www.mckinsey.com/featured-insights |
| **取得成功/失敗** | ❌ 失敗 |
| **エラー種別** | HTTP 403 Forbidden |
| **原因推測** | Bot/User-Agent フィルタリング、地域制限の可能性 |
| **有用性** | 取得不可 |
| **アクセスレベル推奨** | no_access |

---

### 2. bcg.com

| 項目 | 結果 |
|---|---|
| **URL** | https://www.bcg.com/publications |
| **取得成功/失敗** | ❌ 失敗 |
| **エラー種別** | HTTP 403 Forbidden |
| **原因推測** | Bot/User-Agent フィルタリング |
| **有用性** | 取得不可 |
| **アクセスレベル推奨** | no_access |

---

### 3. hbr.org

| 項目 | 結果 |
|---|---|
| **URL** | https://hbr.org/ |
| **取得成功/失敗** | ❌ 失敗 |
| **エラー種別** | HTTP 403 Forbidden |
| **原因推測** | ペイウォール保護 + Bot/User-Agent フィルタリング |
| **有用性** | 取得不可 |
| **アクセスレベル推奨** | no_access |

---

### 4. ft.com

| 項目 | 結果 |
|---|---|
| **URL** | https://www.ft.com/ |
| **取得成功/失敗** | ❌ 失敗 |
| **エラー種別** | WebFetch ツール側での拒否（Robot.txt 遵守 or Bot 検出） |
| **有用性** | 取得不可 |
| **アクセスレベル推奨** | no_access |

---

### 5. nikkei.com

| 項目 | 結果 |
|---|---|
| **URL** | https://www.nikkei.com/ |
| **取得成功/失敗** | ❌ 失敗 |
| **エラー種別** | HTTP 403 Forbidden |
| **原因推測** | ペイウォール保護 + 地域制限の可能性 |
| **有用性** | 取得不可 |
| **アクセスレベル推奨** | no_access |

---

## 総括

### 取得成功: 0 / 5 (0%)

すべてのテストドメインで WebFetch がブロックされた。

### 主な原因

1. **Bot/User-Agent フィルタリング** (4/5) — WebFetch ツールの User-Agent が自動化ツールとして識別・ブロック
2. **WebFetch ツール側での拒否** (1/5) — ft.com は Robot.txt 遵守により拒否
3. **ペイウォール保護** (2/5) — hbr.org, nikkei.com は有料会員限定コンテンツ

### 推奨アクション

- テスト対象の全5ドメインを `domain-access-levels.json` の `no_access` に移動
- メール本文内のリンク（ニュースレター配信用URL等）はペイウォール回避版の場合があるため、運用中に個別に再評価

---

## テスト環境情報

- テスト日時: 2026-04-14
- テストツール: WebFetch (Claude Code)
- テスト対象: 5ドメイン（config/test-domains.json に定義）
- 全成功率: 0%
