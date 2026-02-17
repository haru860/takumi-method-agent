---
name: planning-all
description: 企画立案に関するすべての成果物（因果関係ループ図、MSP計画、ゴール記述、企画書）を一括作成する
---

# 企画立案全体フロー

因果関係ループ図、MSP計画、ゴール記述モデル、企画書を順番に作成します。

**前提条件**:
- Phase 4が完了している
- `/vm-all` が完了している（`output/vm-compare-score.md` が存在）
- 以下のファイルが存在する:
  - `output/requirement-tree-business.tsv`
  - `output/requirement-tree-it.tsv`
  - `output/requirement-tree-activity.tsv`
  - `output/requirement-tree.json`
  - `output/vm-compare-score.md`

**【重要】以下の手順に従い順番に実行してください。**

---

## Step1: 因果関係ループ図の作成

Skill toolを使用して `planning-causal-loop-diagram` を実行する。

**出力ファイル**: `output/causal-loop-diagram.md`

**目的**: 要求分析ツリーを元に、システム思考に基づいた因果関係ループ図を生成し、企画が最も効果的に進むための施策の優先順位を可視化する。

---

## Step2: MSP計画の作成

Skill toolを使用して `planning-msp-plan` を実行する。

**出力ファイル**: `output/msp-plan.md`

**目的**: 顧客に価値を提供し、販売を開始できる最小限の製品・サービス（MSP）の計画を立てる。

---

## Step3: ゴール記述モデルの作成

Skill toolを使用して `goal-description` を実行する。

**出力ファイル**: `output/goal-description-model.tsv`

**目的**: MSP計画の作業項目を、具体的なゴール記述として細分化し、誰が・何を・いつまでに・どのように達成するかを明確にする。

---

## Step4: 企画書の生成

Skill toolを使用して `planning-proposal-make` を実行する。

**出力ファイル**: `output/proposal-format1.md` または `output/proposal-format2.md`

**目的**: 匠Methodの成果物を基に、企画書を生成する。

---

## 全体完了時の動作

すべてのステップが完了したら、以下を報告：

1. 出力されたファイルの一覧
2. 因果関係ループ図のレバレッジポイントの要約
3. MSP計画の概要（フェーズ数、主要要件）
4. ゴール記述モデルの総数と期間
5. 企画書のフォーマットと構成
