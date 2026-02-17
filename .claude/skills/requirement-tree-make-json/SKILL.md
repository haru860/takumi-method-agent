---
name: requirement-tree-make-json
description: 要求分析ツリーのJSON出力と構造検証
---

# Phase 4-5: 要求分析ツリーのJSONの作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 2, 3, 4が完了している
- `output/value-design.tsv` が存在する
- `output/value-analysis-objective.tsv` が存在する
- `output/requirement-tree-business.tsv` が存在する
- `output/requirement-tree-it.tsv` が存在する
- `output/requirement-tree-activity.tsv` が存在する

---

## 実行手順

### 手順1: 知識の読み込み

`Read` ツールで `.claude/skills/takumi-method/requirement-tree.md` を読み込み、要求ツリーの構造を理解する。

**ツリー構造**:
```
ビジョン
└── コンセプト（1〜3）
    └── 目的
        └── 業務要求
            ├── IT要求
            └── 活動
```

### 手順2: 入力ファイルの読み込み

`Read` ツールで以下のファイルを読み込む：

1. `output/value-design.tsv` - ビジョン・コンセプトを取得
2. `output/value-analysis-objective.tsv` - 目的を取得（コンセプトとの紐付けあり）
3. `output/requirement-tree-business.tsv` - 業務要求を取得（目的との紐付けあり）
4. `output/requirement-tree-it.tsv` - IT要求を取得（業務要求との紐付けあり）
5. `output/requirement-tree-activity.tsv` - 活動を取得（業務要求との紐付けあり）

### 手順3: JSONツリー構造の作成

入力ファイルのデータを基に、以下の構造でJSONを作成する：

```json
{
  "vision": {
    "name": "ビジョン名"
  },
  "concepts": [
    {
      "name": "コンセプト名",
      "objectives": [
        {
          "name": "目的名",
          "businessRequirements": [
            {
              "name": "業務要求名",
              "itRequirements": [
                {
                  "name": "IT要求名",
                  "description": "説明"
                }
              ],
              "activities": [
                {
                  "name": "活動名",
                  "description": "説明"
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

**作成ルール**:
- ビジョン: `value-design.tsv` の「要素」が「ビジョン」の行から取得
- コンセプト: `value-design.tsv` の「要素」が「コンセプト」の行から取得
- 目的: `value-analysis-objective.tsv` から取得し、コンセプトに紐付け
- 業務要求: `requirement-tree-business.tsv` から取得し、目的に紐付け
- IT要求: `requirement-tree-it.tsv` から取得し、業務要求に紐付け
- 活動: `requirement-tree-activity.tsv` から取得し、業務要求に紐付け

### 手順4: 既存ファイルの削除

`output/requirement-tree.json` が存在する場合は削除する。

### 手順5: JSONファイルの出力

`Write` ツールで以下を作成：

- **パス**: `output/requirement-tree.json`
- **形式**: JSON（整形済み、インデント2スペース）
- **文字コード**: UTF-8

### 手順6: 構造検証

入力ファイルの全データがJSONツリーに含まれているか検証する。

**検証対象**:
1. **コンセプト**: `value-design.tsv` のコンセプトがすべてJSONに含まれているか
2. **目的**: `value-analysis-objective.tsv` の目的がすべてJSONに含まれているか
3. **業務要求**: `requirement-tree-business.tsv` の業務要求がすべてJSONに含まれているか
4. **IT要求**: `requirement-tree-it.tsv` のIT要求がすべてJSONに含まれているか
5. **活動**: `requirement-tree-activity.tsv` の活動がすべてJSONに含まれているか

**検証方法**:
- 各TSVファイルのデータを取得
- JSONツリー内の対応するノードを検索
- 親ノード（紐付け先）が存在しない場合、ツリーに含められないと判定

### 手順7: 検証結果の出力

ツリー構造に含まれていない要素がある場合、以下の形式でリストアップする：

```markdown
## 検証結果

### ツリーに含まれていない要素

#### コンセプト（親: ビジョン）
- なし

#### 目的（親: コンセプト）
- 「○○目的」: 紐付け先のコンセプト「△△」がビジョンに存在しない

#### 業務要求（親: 目的）
- 「○○要求」: 紐付け先の目的「△△」がコンセプト配下に存在しない

#### IT要求（親: 業務要求）
- 「○○機能」: 紐付け先の業務要求「△△」が目的配下に存在しない

#### 活動（親: 業務要求）
- 「○○作業」: 紐付け先の業務要求「△△」が目的配下に存在しない
```

すべての要素がツリーに含まれている場合は「すべての要素がツリー構造に正しく含まれています」と報告する。

---

## 完了時の動作

1. 出力したJSONファイル名を報告: `output/requirement-tree.json`
2. 検証結果を報告（ツリーに含まれていない要素のリスト、または「すべて正常」）
