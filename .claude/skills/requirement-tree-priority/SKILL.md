---
name: requirement-tree-priority
description: MSP計画に基づいて要求分析ツリーの優先要素を色分けハイライト表示
---

# 要求分析ツリー優先度ハイライト

**追加指示（引数）**: $ARGUMENTS

## 概要

MSP（Minimum Sellable Product）計画で特定された優先要素を、要求分析ツリーのDrawIOモデル上で色分けハイライト表示します。

**目的**:
- MSPの実現に必要な要素を視覚的に識別可能にする
- 優先的に取り組むべき業務要求・IT要求・活動を明確化する
- 必須要件と差別化要件を色で区別する

**前提条件**:
- Phase 4（要求分析ツリー）が完了している
- `/msp-plan` が実行済みである
- `output/requirement-tree.json` が存在する
- `output/msp-plan.md` が存在する
- `output/drawio/requirement-tree.drawio` が存在する

---

## 色分けルール

| 優先度 | 対象 | fillColor | strokeColor |
|--------|------|-----------|-------------|
| 必須要件（Must Have） | IT要求・活動・業務要求・目的 | `#DC143C`（クリムゾン） | `#8B0D1C`（濃いクリムゾン） |
| 差別化要件（Should Have） | IT要求・活動・業務要求・目的 | `#4169E1`（ロイヤルブルー） | `#1E3A8A`（濃いロイヤルブルー） |
| 変更なし | ビジョン・コンセプト | - | - |

**重要**:
- 上位要素（業務要求、目的）も、配下にMSP要素がある場合は同じ色に設定する
- ただし、ビジョンとコンセプトは変更しない
- **優先順位**: 同じ要素が必須要件と差別化要件の両方に該当する場合は、必須要件（クリムゾン）を優先し、ロイヤルブルーには変更しない

---

## 実行手順

### 手順1: 前提条件の確認

`Glob` ツールで以下のファイルの存在を確認する：
- `input/idea.md`（必須）
- `output/requirement-tree.json`（必須）
- `output/msp-plan.md`（必須）
- `output/drawio/requirement-tree.drawio`（必須）

存在しない場合は、先に該当するコマンドを実行するようユーザーに通知する。

### 手順2: 既存ファイルの確認

`output/drawio/requirement-tree.drawio` が存在することを確認する（このコマンドは既存ファイルを上書き更新するため、削除不要）。

### 手順3: 入力ファイルの読み込み

`Read` ツールで以下を読み込む：
- `output/msp-plan.md` - MSP計画（優先要素の特定に使用）
- `output/requirement-tree.json` - 要求分析ツリーの構造データ（階層関係の把握に使用）

`Read` ツールで以下を読み込む：
- `output/drawio/requirement-tree.drawio` - DrawIOファイル

### 手順4: MSP優先要素の特定

`output/msp-plan.md` を分析し、以下の2つのカテゴリに分類する：

#### 4-1. 必須要件（Must Have）の特定
「必須要件（Must Have）」セクションから以下を抽出：
- IT要求の名前リスト
- 活動の名前リスト

#### 4-2. 差別化要件（Should Have）の特定
「差別化要件（Should Have）」セクションから以下を抽出：
- IT要求の名前リスト
- 活動の名前リスト

### 手順5: 上位要素の特定

`output/requirement-tree.json` を使用して、MSP要素の上位階層を特定する：

1. **必須要件（Must Have）の上位要素**:
   - 必須要件のIT要求・活動が属する「業務要求」を特定
   - その業務要求が属する「目的」を特定
   - これらも必須要件（クリムゾン）の対象に追加

2. **差別化要件（Should Have）の上位要素**:
   - 差別化要件のIT要求・活動が属する「業務要求」を特定
   - その業務要求が属する「目的」を特定
   - **ただし、既に必須要件（クリムゾン）として特定されている要素は除外する**
   - 除外されなかった要素のみ差別化要件（ロイヤルブルー）の対象に追加

**重要**: 色分けは以下の順序で処理し、必須要件を優先する：
1. まず必須要件（Must Have）の全要素（IT要求、活動、業務要求、目的）を特定
2. 次に差別化要件（Should Have）の要素を特定する際、必須要件に含まれる要素は除外
3. 結果として、同じ要素が両方に該当する場合は必ずクリムゾン（必須要件）が適用される

### 手順6: DrawIO XMLの更新

Pythonスクリプトを使用してDrawIOファイルのXMLを編集する：

```python
import re

# ファイルを読み込み
with open('output/drawio/requirement-tree.drawio', 'r', encoding='utf-8') as f:
    content = f.read()

# 必須要件（Must Have）の要素IDリスト（IT要求、活動、業務要求、目的）
must_have_ids = set([
    # ここにMSP計画から抽出した必須要件の要素IDを列挙
    # 例: "it1_2_1", "act1_1_1", "br1_2_1", "obj1_2"
])

# 差別化要件（Should Have）の要素IDリスト（IT要求、活動、業務要求、目的）
# 注意: must_have_idsに含まれるIDは除外すること
should_have_ids = set([
    # ここにMSP計画から抽出した差別化要件の要素IDを列挙
    # 例: "it2_2_1", "act1_3_4", "br2_2_1", "obj2_2"
])

# 差別化要件から必須要件と重複するIDを除外（必須要件を優先）
should_have_ids = should_have_ids - must_have_ids

def get_id(line):
    """id属性を取得"""
    match = re.search(r'id="([^"]+)"', line)
    return match.group(1) if match else ""

def update_colors(line, fill_color, stroke_color):
    """色を更新"""
    if 'fillColor=#' in line:
        line = re.sub(r'fillColor=#[a-fA-F0-9]+', f'fillColor={fill_color}', line)
    if 'strokeColor=#' in line:
        line = re.sub(r'strokeColor=#[a-fA-F0-9]+', f'strokeColor={stroke_color}', line)
    return line

# 行ごとに処理
lines = content.splitlines()
new_lines = []

for line in lines:
    if 'mxCell' in line and 'id=' in line:
        cell_id = get_id(line)

        # ビジョンとコンセプトはスキップ
        if cell_id == "vision" or cell_id.startswith("concept"):
            new_lines.append(line)
            continue

        # 必須要件（クリムゾン）を先に処理
        if cell_id in must_have_ids:
            line = update_colors(line, "#DC143C", "#8B0D1C")
        # 差別化要件（ロイヤルブルー）は必須要件に含まれない場合のみ
        elif cell_id in should_have_ids:
            line = update_colors(line, "#4169E1", "#1E3A8A")

    new_lines.append(line)

content = '\n'.join(new_lines)

# 結果を出力
with open('output/drawio/requirement-tree.drawio', 'w', encoding='utf-8') as f:
    f.write(content)
```

**変更例**:
```xml
<!-- 変更前（通常の業務要求） -->
<mxCell id="xxx" value="対象の業務要求名" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" ...>

<!-- 変更後（必須要件 - クリムゾン） -->
<mxCell id="xxx" value="対象の業務要求名" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DC143C;strokeColor=#8B0D1C;" ...>

<!-- 変更後（差別化要件 - ロイヤルブルー） -->
<mxCell id="xxx" value="対象の業務要求名" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#4169E1;strokeColor=#1E3A8A;" ...>
```

### 手順7: ファイル出力

Pythonスクリプト内でファイルを直接更新する。

### 手順8: 出力確認

`Glob` ツールで `output/drawio/requirement-tree.drawio` の存在を確認。
ファイルが存在しない場合は、手順6に戻り再実行する。

---

## 完了時の動作

- 出力したファイル名を報告
- ハイライトされた要素のリストを優先度別に表示：

### 必須要件（Must Have）- クリムゾン
- 目的: X件
- 業務要求: X件
- IT要求: X件
- 活動: X件

### 差別化要件（Should Have）- ロイヤルブルー
- 目的: X件
- 業務要求: X件
- IT要求: X件
- 活動: X件
