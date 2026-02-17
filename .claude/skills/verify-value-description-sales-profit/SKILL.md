---
name: verify-value-description-sales-profit
description: 自社の価値記述が十分な売上・利益を上げられるか検証
---

# 価値記述の売上・利益観点での検証

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 3-1が完了している
- `output/value-analysis-value-description.tsv` が存在し、価値記述が記載されている

**出力ファイル**: `output/verify-value-description-sales-profit-result.md`

---

## 実行手順

### 手順1: 既存ファイルのバックアップ

@common-procedures の「バックアップ手順」に従い、`output/verify-value-description-sales-profit-result.md` をバックアップする。

### 手順2: 売上・利益観点での価値記述検証

`Task` ツールで `VerifyValueDescriptionSalesProfit` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順3: 検証結果のファイル出力

**【重要】エージェント完了後、検証結果を必ず以下のファイルに出力する**:

`Write` ツールで以下を作成（@common-procedures の「検証結果出力の共通ルール」に従う）：

- **ファイルパス**: `output/verify-value-description-sales-profit-result.md`
- **内容**: エージェントが出力した検証結果

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。