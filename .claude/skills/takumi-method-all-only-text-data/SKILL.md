---
name: takumi-method-all-only-text-data
description: 匠Methodの全成果物（コアモデル、価値マネジメント評価、企画立案）を一括作成する
---

# 匠Method全成果物一括作成

匠Methodのコアモデル（Phase 1〜4）、価値マネジメント評価、企画立案に関するすべての成果物を順番に作成します。

**前提条件**:
- `input/idea.md` が存在する

**【重要】以下の手順に従い順番に実行してください。他のコマンドを参照して手順、ToDoリストを作る必要はありません。**

---

## Step1: コアモデルのテキストデータ作成

Skill toolを使用して `takumi-method-core-all-only-text-data` を実行する。

**目的**: Phase 1〜4（ステークホルダーモデル、価値デザインモデル、価値分析モデル、要求分析ツリー）のTSVファイルを作成する。

**出力ファイル**:
- `output/stakeholder.tsv`
- `output/value-design.tsv`
- `output/value-analysis-value-description.tsv`
- `output/value-analysis-objective.tsv`
- `output/requirement-tree-business.tsv`
- `output/requirement-tree-it.tsv`
- `output/requirement-tree-activity.tsv`

---

## Step2: 価値マネジメント評価の実行

Skill toolを使用して `vm-all` を実行する。

**目的**: 価値概念の評価、IT要求・活動のインパクトスコア算出、価値概念との乖離検証を実行する。

**出力ファイル**:
- `output/vm-value-concept.tsv`
- `output/vm-it-requirement-impact-score.tsv`
- `output/vm-activity-impact-score.tsv`
- `output/vm-it-requirement-activity-impact-score.tsv`
- `output/vm-compare-score.md`

---

## Step3: 企画立案の実行

Skill toolを使用して `planning-all` を実行する。

**目的**: 因果関係ループ図、MSP計画、ゴール記述モデル、企画書を作成する。

**出力ファイル**:
- `output/causal-loop-diagram.md`
- `output/msp-plan.md`
- `output/goal-description-model.tsv`
- `output/proposal-format1.md` または `output/proposal-format2.md`

---

## 全体完了時の動作

Skill toolを使用して `common-procedures` を実行し、「完了報告」を行う。

/clear