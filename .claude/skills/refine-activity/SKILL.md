---
name: refine-activity
description: 検証結果に基づいて活動を洗練・修正する
---

# 活動の洗練

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-activity` が完了している
- `output/verify-activity-result.md` が存在する

**出力ファイル**: `output/requirement-tree-activity.tsv`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-activity-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-activity-result.md

先に `/verify-activity` を実行して、活動の検証を行ってください。
```

### 手順2: 検証結果の読み込み

`Read` ツールで `output/verify-activity-result.md` を読み込み、以下の情報を抽出する：

- **悪い点・改善点**: 現在の活動の問題点
- **改善のための問い**: 活動を改善するためのヒント

### 手順3: 活動の再作成

`Skill` ツールで `requirement-tree-activity` スキルを呼び出す。

**引数として以下を渡す**:

```
【検証結果に基づく修正指示】

以下の改善点を踏まえて、活動を再作成してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-activity` の実行を案内する。
