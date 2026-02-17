---
name: requirement-tree-it-activity-add
description: 下位要素が存在しない業務要求に対してIT要求または活動を追加作成
---

# Phase 4-4: 下位要素が不足している業務要求への補完

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 4-1, 4-2, 4-3が完了している
- `output/requirement-tree-business.tsv` が存在する
- `output/requirement-tree-it.tsv` が存在する
- `output/requirement-tree-activity.tsv` が存在する

---

## 実行手順

### 手順1: 知識とデータの読み込み

以下のファイルを読み込む：

1. `Read` で `.claude/skills/takumi-method/requirement-tree.md` を読み込む
2. `Read` で `output/requirement-tree-business.tsv` を読み込む
3. `Read` で `output/requirement-tree-it.tsv` を読み込む
4. `Read` で `output/requirement-tree-activity.tsv` を読み込む

### 手順2: 下位要素が不足している業務要求の特定

読み込んだデータを分析し、以下の条件に該当する業務要求を特定する：

- IT要求にも活動にも紐づいていない業務要求（下位要素が0件）

### 手順3: 不足している下位要素の作成

特定した業務要求に対して、以下の観点でIT要求または活動を作成する：

**IT要求を作成する場合**:
- システムやツールで実現すべき機能
- データ管理、自動化、効率化に関する要件

**活動を作成する場合**:
- 人が実施すべき作業やタスク
- コミュニケーション、教育、運用に関する活動

**判断基準**:
- 業務要求の性質に応じて、IT要求か活動のどちらが適切かを判断
- 必要に応じて両方を作成することも可能

### 手順4: TSVファイルへの追記

追加作成した要素を既存のTSVファイルに追記する：

**IT要求の追記** (`output/requirement-tree-it.tsv`)（@common-procedures の「TSV出力形式の共通ルール」に従う）:
- 既存のファイル内容を読み込み、追加分を末尾に追記
- **ヘッダー**: `IT要求	説明	業務要求`（既存のまま維持）

**活動の追記** (`output/requirement-tree-activity.tsv`)（@common-procedures の「TSV出力形式の共通ルール」に従う）:
- 既存のファイル内容を読み込み、追加分を末尾に追記
- **ヘッダー**: `活動	説明	業務要求`（既存のまま維持）

### 手順5: 出力確認

`Read` ツールで以下のファイルを読み込み、行数と内容を確認する：
- `output/requirement-tree-it.tsv`
- `output/requirement-tree-activity.tsv`

---

## 完了時の動作

以下の情報を報告：

1. 下位要素が不足していた業務要求の一覧
2. 追加作成したIT要求の一覧（業務要求との紐づけを含む）
3. 追加作成した活動の一覧（業務要求との紐づけを含む）
4. 更新後のファイル名
