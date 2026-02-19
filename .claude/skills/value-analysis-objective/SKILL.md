---
name: value-analysis-objective
description: Phase 3-2（目的の作成とTSV生成）を実行
---

# Phase 3-2: 目的の作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 3-1が完了している
- `output/value-analysis-value-description.tsv` が存在する
- `output/value-design.tsv` が存在する

**出力ファイル**: `output/value-analysis-objective.tsv`

---

## 実行手順

### 手順1: 目的の作成

`Task` ツールで `ValueAnalysisObjective` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/value-analysis-objective.tsv` が存在する場合は削除する。

### 手順3: TSVファイルの出力

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/value-analysis-objective.tsv`
- **ヘッダー**: `目的名	目的の説明	関連するコンセプト`
- **データ行**:
  - 目的名
  - 目的の説明
  - 関連するコンセプト

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。