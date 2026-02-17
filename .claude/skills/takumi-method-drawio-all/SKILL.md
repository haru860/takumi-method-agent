---
name: takumi-method-drawio-all
description: 匠MethodのDrawIOモデル（コアモデル + ビジネスコンテキストフロー）を全て作成する。
---

# 実行手順

**前提条件**:
- `input/idea.md` が存在する
- `output/stakeholder.tsv` が存在する
- `output/value-design.tsv` が存在する
- `output/value-analysis-value-description.tsv` が存在する
- `output/value-analysis-objective.tsv` が存在する
- `output/requirement-tree.json` が存在する

**【重要】以下の手順に従い実行してください。他のコマンドを参照して手順、ToDoリストを作る必要はありません。**

# Step1 コアモデルのDrawIO作成

Skill toolを使用して `takumi-method-drawio-core-all` を実行する。


# Step2 ビジネスコンテキストフローの作成

Skill toolを使用して `business-context-flow-drawio-generator` を実行する。


## 全体完了時の動作

Skill toolを使用して `common-procedures` を実行し、「完了報告」を行う。

