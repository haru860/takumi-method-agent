---
name: verify-activity
description: 活動の良い点・悪い点を分析し、改善点と改善のための問いを生成
---

# 活動の検証

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 4-3が完了している
- `output/requirement-tree-activity.tsv` が存在し、活動が記載されている

**出力ファイル**: `output/verify-activity-result.md`

---

## 実行手順

### 手順1: 活動の検証

`Task` ツールで `VerifyActivity` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 検証結果のファイル出力

**【重要】エージェント完了後、検証結果を必ず以下のファイルに出力する**:

`Write` ツールで以下を作成（@common-procedures の「検証結果出力の共通ルール」に従う）：

- **ファイルパス**: `output/verify-activity-result.md`
- **内容**: エージェントが出力した検証結果（良い点・悪い点・改善点・改善のための問い）

### 手順3: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。
