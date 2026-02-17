---
name: refine-planning-proposal-make
description: 検証結果に基づいて企画書を洗練・修正する
---

# 企画書の洗練

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-planning-proposal-make` が完了している
- `output/verify-planning-proposal-make-result.md` が存在する

**出力ファイル**: `output/proposal-format1.md` または `output/proposal-format2.md`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-planning-proposal-make-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-planning-proposal-make-result.md

先に `/verify-planning-proposal-make` を実行して、企画書の検証を行ってください。
```

### 手順2: 検証結果の読み込みとフォーマット確認

1. `Read` ツールで `output/verify-planning-proposal-make-result.md` を読み込み、以下の情報を抽出する：
   - **悪い点・改善点**: 現在の企画書の問題点
   - **改善のための問い**: 企画書を改善するためのヒント
   - **使用フォーマット**: 検証対象のフォーマット（format1 または format2）

2. フォーマットが検証結果から判別できない場合は、`Glob` で `output/proposal-format1.md` と `output/proposal-format2.md` の存在を確認して特定する。

### 手順3: 企画書の再作成

`Skill` ツールで `planning-proposal-make` スキルを呼び出す。

**引数として以下を渡す**:

```
[使用フォーマット（format1 または format2）]

【検証結果に基づく修正指示】

以下の改善点を踏まえて、企画書を再作成してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-planning-proposal-make` の実行を案内する。
