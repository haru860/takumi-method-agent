---
name: requirement-tree-it-requirement
description: 要求分析ツリーのIT要求を作成（Phase 4-2）
---

# Phase 4-2: IT要求の作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 4-1が完了している
- `output/requirement-tree-business.tsv` が存在する

**出力ファイル**: `output/requirement-tree-it.tsv`

---

## 実行手順

### 手順1: IT要求の作成

`Task` ツールで `RequirementTreeIt` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/requirement-tree-it.tsv` が存在する場合は削除する。

### 手順3: TSVファイルの出力

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/requirement-tree-it.tsv`
- **ヘッダー**: `IT要求	説明	業務要求`
- **データ行**:
  - IT要求: IT要求の名前
  - 説明: IT要求の内容を説明する文章
  - 業務要求: 関連する業務要求の名前（**1つのみ**。最も関連度が高いものを選択）
- **重要**: IT要求1つにつき必ず1行で出力すること（同じIT要求名で複数行を作成しない）

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。
