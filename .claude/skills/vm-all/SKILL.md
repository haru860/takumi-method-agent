---
name: vm-all
description: 価値マネジメント（VM）の全評価を実行する
---

# 価値マネジメント全評価

価値概念の評価、IT要求・活動のインパクトスコア算出、価値概念との乖離検証を一括実行します。

**前提条件**:
- Phase 3-2が完了している
- `output/value-analysis-objective.tsv` が存在する
- `output/value-design.tsv` が存在する
- `output/requirement-tree-business.tsv` が存在する
- `output/requirement-tree-it.tsv` が存在する
- `output/requirement-tree-activity.tsv` が存在する

**【重要】以下の手順に従い順番に実行してください。**

---

## Step1: 価値概念のリストアップとインパクト評価

Skill toolを使用して `vm-value-concept-score` を実行する。

**出力ファイル**: `output/vm-value-concept.tsv`

---

## Step2: IT要求・活動インパクトスコア算出

Skill toolを使用して `vm-it-activity-impact-score` を実行する。

**出力ファイル**:
- `output/vm-it-requirement-impact-score.tsv`
- `output/vm-activity-impact-score.tsv`
- `output/vm-it-requirement-activity-impact-score.tsv`

---

## Step3: 価値概念乖離検証

Skill toolを使用して `vm-compare-score` を実行する。

**出力ファイル**: `output/vm-compare-score.md`

---

## 全体完了時の動作

すべてのステップが完了したら、以下を報告：

1. 出力されたファイルの一覧
2. 価値概念乖離検証の結果サマリー
