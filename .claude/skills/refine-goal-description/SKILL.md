---
name: refine-goal-description
description: 検証結果に基づいてゴール記述モデルを洗練・修正する
---

# ゴール記述モデルの洗練

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-goal-description` が完了している
- `output/verify-goal-description-result.md` が存在する

**出力ファイル**: `output/goal-description-model.tsv`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-goal-description-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-goal-description-result.md

先に `/verify-goal-description` を実行して、ゴール記述モデルの検証を行ってください。
```

### 手順2: 検証結果の読み込み

`Read` ツールで `output/verify-goal-description-result.md` を読み込み、以下の情報を抽出する：

- **悪い点・改善点**: 現在のゴール記述モデルの問題点
- **改善のための問い**: ゴール記述モデルを改善するためのヒント

### 手順3: ゴール記述モデルの再作成

`Skill` ツールで `goal-description` スキルを呼び出す。

**引数として以下を渡す**:

```
【検証結果に基づく修正指示】

以下の改善点を踏まえて、ゴール記述モデルを再作成してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-goal-description` の実行を案内する。
