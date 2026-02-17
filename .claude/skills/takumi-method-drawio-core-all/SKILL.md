---
name: takumi-method-drawio-core-all
description: 匠MethodのコアモデルのDrawIOモデルを作成する。
---

## 概要

匠Methodの4つのモデル（ステークホルダーモデル、価値デザインモデル、価値分析モデル、要求分析ツリー）のDrawIOファイルを作成する。

## 前提条件

以下のファイルが存在すること：
- `input/idea.md`
- `output/stakeholder.tsv`
- `output/value-design.tsv`
- `output/value-analysis-value-description.tsv`
- `output/value-analysis-objective.tsv`
- `output/requirement-tree.json`
---

## 実行手順
THINK HARD

以下を順に実行してください。(並行で実行しないこと)

### 手順1: 企画の把握

- `Read` ツールで `input/idea.md` を読み込み、企画内容を把握し、コンソールに出力する。

### 手順2: ステークホルダーモデル
@stakeholder-drawio-generator.md の **「実行手順」** に従い、処理を実行する。


### 手順3: 価値デザインモデル
@value-design-drawio-generator.md の **「実行手順」** に従い、処理を実行する。


### 手順4: 価値分析モデル
@value-analysis-drawio-generator.md の **「実行手順」** に従い、処理を実行する。


### 手順5: 要求分析ツリー
@requirement-tree-drawio-generator.md の **「実行手順」** に従い、処理を実行する。

