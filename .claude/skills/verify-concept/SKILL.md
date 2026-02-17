---
name: verify-concept
description: コンセプトの良い点・悪い点を分析し、改善点と改善のための問いを生成
---

# コンセプトの検証

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 2-2が完了している
- `output/value-design.tsv` が存在し、ビジョンとコンセプトが記載されている

**出力ファイル**: `output/verify-concept-result.md`

---

## 実行手順

### 手順1: コンセプトの検証

`Task` ツールで `VerifyConcept` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 検証結果のファイル出力

**【重要】エージェント完了後、検証結果を必ず以下のファイルに出力する**:

`Write` ツールで以下を作成（@common-procedures の「検証結果出力の共通ルール」に従う）：

- **ファイルパス**: `output/verify-concept-result.md`
- **内容**: エージェントが出力した検証結果（良い点・悪い点・改善点・改善のための問い）

### 手順3: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。