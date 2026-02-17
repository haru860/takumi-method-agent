---
name: refine-vm-it-activity-impact-score
description: 検証結果に基づいてIT要求・活動インパクトスコアを洗練・修正する
---

# IT要求・活動インパクトスコアの洗練

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-vm-it-activity-impact-score` が完了している
- `output/verify-vm-it-activity-impact-score-result.md` が存在する

**出力ファイル**: `output/vm-it-requirement-impact-score.tsv`, `output/vm-activity-impact-score.tsv`, `output/vm-it-requirement-activity-impact-score.tsv`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-vm-it-activity-impact-score-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-vm-it-activity-impact-score-result.md

先に `/verify-vm-it-activity-impact-score` を実行して、IT要求・活動インパクトスコアの検証を行ってください。
```

### 手順2: 検証結果の読み込み

`Read` ツールで `output/verify-vm-it-activity-impact-score-result.md` を読み込み、以下の情報を抽出する：

- **悪い点・改善点**: 現在のIT要求・活動インパクトスコアの問題点
- **改善のための問い**: IT要求・活動インパクトスコアを改善するためのヒント

### 手順3: IT要求・活動インパクトスコアの再作成

`Skill` ツールで `vm-it-activity-impact-score` スキルを呼び出す。

**引数として以下を渡す**:

```
【検証結果に基づく修正指示】

以下の改善点を踏まえて、IT要求・活動インパクトスコアを再作成してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-vm-it-activity-impact-score` の実行を案内する。
