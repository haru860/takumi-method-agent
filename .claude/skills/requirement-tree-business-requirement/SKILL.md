---
name: requirement-tree-business-requirement
description: 要求分析ツリーの業務要求を作成（Phase 4-1）
---

# Phase 4-1: 業務要求の作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 1, Phase 2, Phase 3が完了している
- `output/value-analysis-value-description.tsv` が存在する
- `output/value-analysis-objective.tsv` が存在する

**出力ファイル**: `output/requirement-tree-business.tsv`

---

## 実行手順

### 手順1: 業務要求の作成

`Task` ツールで `RequirementTreeBusiness` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/requirement-tree-business.tsv` が存在する場合は削除する。

### 手順3: TSVファイルの出力

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/requirement-tree-business.tsv`
- **ヘッダー**: `業務要求	説明	目的	関連する価値記述名	関連する価値記述`
- **データ行**:
  - 業務要求: 業務要求の名前
  - 説明: 業務要求の内容を説明する文章
  - 目的: 関連する目的の名前（1つのみ出力する。複数ある場合は関連が強い目的のみを出力する）
  - 関連する価値記述名: 業務要求の元となった価値記述名
  - 関連する価値記述: 業務要求の元となった価値記述
- 業務要求1つにつき1行で出力

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 出力件数確認

【重要】「`output/value-analysis-value-description.tsv`の価値記述の全件数」と、`output/requirement-tree-business.tsv`の出力件数が一致していることを確認する。一致していなければ、手順3に戻る。

### 手順6: 完了報告

@common-procedures の「完了報告」に従う。
