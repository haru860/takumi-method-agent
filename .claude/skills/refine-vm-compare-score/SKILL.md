---
name: refine-vm-compare-score
description: 検証結果に基づいてスコア乖離検証結果を洗練・修正する
---

# スコア乖離検証結果の洗練

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-vm-compare-score` が完了している
- `output/verify-vm-compare-score-result.md` が存在する

**出力ファイル**: `output/vm-compare-score.md`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-vm-compare-score-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-vm-compare-score-result.md

先に `/verify-vm-compare-score` を実行して、スコア乖離検証結果の検証を行ってください。
```

### 手順2: 検証結果の読み込み

`Read` ツールで `output/verify-vm-compare-score-result.md` を読み込み、以下の情報を抽出する：

- **悪い点・改善点**: 現在のスコア乖離検証結果の問題点
- **改善のための問い**: スコア乖離検証結果を改善するためのヒント

### 手順3: スコア乖離検証の再実行

`Skill` ツールで `vm-compare-score` スキルを呼び出す。

**引数として以下を渡す**:

```
【検証結果に基づく修正指示】

以下の改善点を踏まえて、スコア乖離検証を再実行してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-vm-compare-score` の実行を案内する。
