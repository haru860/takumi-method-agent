---
name: goal-description-model
description: 匠Methodのゴール記述モデルを作成
---

# ゴール記述モデルの作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/planning-msp-plan` が完了している（`output/msp-plan.md` が存在）

**出力ファイル**: `output/goal-description-model.tsv`

---

## 実行手順

### 手順1: ゴール記述モデルの作成

`Task` ツールで `GoalDescription` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/goal-description-model.tsv` が存在する場合は削除する。

### 手順3: TSVファイルの出力

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/goal-description-model.tsv`
- **ヘッダー**: `テーマ	役割名	何を	開始時期	終了時期	どうする	評価尺度	目標値`
- **データ行**:
  - テーマ: 上位目標・Phase名
  - 役割名: 担当者の役割
  - 何を: 対象となる成果物・機能
  - 開始時期: 具体的な日付・時期
  - 終了時期: 具体的な日付・時期
  - どうする: 具体的なアクション
  - 評価尺度: 測定可能な指標
  - 目標値: 達成すべきレベル
- ゴール記述1つにつき1行で出力
- 空白セルは空文字列（""）ではなく「-」を使用

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。

以下を報告に含める：
- 作成したゴール記述の総数
- Phase別のゴール数
- 期間の概要（最初の開始時期〜最後の終了時期）
