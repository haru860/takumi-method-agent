---
name: vm-value-concept-score
description: 価値概念のリストアップとインパクト評価を実行
---

# 価値概念のリストアップとインパクト評価

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 3-2が完了している
- `output/value-analysis-objective.tsv` が存在する
- `output/value-design.tsv` が存在する

---

## 実行手順

### 手順1: 入力ファイルの確認

`Glob` ツールで以下のファイルの存在を確認：
- `output/value-design.tsv`
- `output/value-analysis-objective.tsv`

ファイルが存在しない場合は、ユーザーに以下を案内：
- `value-design.tsv` がない場合 → `/value-design-all` を実行
- `value-analysis-objective.tsv` がない場合 → `/value-analysis-objective` を実行

### 手順2: 既存ファイルの削除

`output/vm-value-concept.tsv` が存在する場合は削除する。

### 手順3: 価値概念の作成とインパクト評価

`Task` ツールで `ValueConceptEvaluator` エージェントを起動する。

**エージェントへの追加指示**: 上記の「追加指示（引数）」が空でない場合、その内容をエージェント起動時のプロンプトに含めて渡すこと。

### 手順4: TSVファイルの出力

`Write` ツールで以下を作成：

- **パス**: `output/vm-value-concept.tsv`
- **形式**: TSV（タブ区切り）
- **ヘッダー**: `目的名	価値概念	インパクト	評価理由	関連コンセプト`
- **データ行**:
  - 目的名
  - 価値概念（『』で囲む）
  - インパクトスコア（1, 3, 8, 13, 21, 34, 89のいずれか）
  - 評価理由
  - 関連コンセプト
 **行の並び順**: インパクトスコアが大きい順

### 手順5: 出力確認

`Glob` ツールで `output/vm-value-concept.tsv` の存在を確認。
ファイルが存在しない場合は、手順4に戻りWriteツールでファイルを作成する。

### 手順6: サマリーの表示

インパクト評価のサマリーを表示：

- スコア別の件数
- 最高スコアの価値概念をハイライト
- 89点（ダントツ）がない場合は、34点の項目を89点に昇格させる施策案を提示

---

## 完了時の動作

- 出力したファイル名を報告
- インパクト評価サマリーを表示
- 89点昇格の施策案があれば提示