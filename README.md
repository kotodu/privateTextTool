# privateTextTool
私的なテキスト置換ツールです。

# テキスト置換メモ
## 置換前イメージ

```md:before
# [TAG]TEXT H1
- リスト1
- リスト2
    1. 項目1
    1. 項目2
    1. 項目3
## TEXT H2
- これはH2のテキストです。
    - 詳細1
    - 詳細2

### TEXT H3
- `詳細3`



```

- 空白インデント
- マークダウン記法
- 数字リストアップは1のみと1,2,3混在
- 見出しは1-3まで
- リストのネストは1-3まで
- 任意の見出しにTAGを付与できる

## 置換後イメージ

```text:after

●TAG●
TEXT H1
	・項目1
	・項目2

	○TEXT H2○


```

- TAGを●●で囲む
- TAGは見出しのネスト位置に合わせ、直前に配置する
- 見出しの前(TAGがある場合はTAGの前)に行を空ける
- タブインデント
- 置換前の見出し・リストレベルは維持する
- 見出しにあわせてリストのネスト開始位置もずらす
    - つまり、最も深い箇所は5段階インデント
- インデント段階に応じて記号を変更する

# 期限
- 6月中にちまちま作る。
    - 多少遅くてもOK

# ルール仕様
1. `[`と`]`がある場合、それぞれ`●`と`●\t`に置換する
    - 置換後、該当行の前に新たな行を作り、そこへ`●TAG●`を移動する
1. 見出し1の中身は、タブで1つインデントする
    - 見出しの`# `は削除する
1. 見出し2の中身は、タブで1つインデントする
    - 見出しの`## `は削除する
1. 見出し3の中身は、タブで1つインデントする
    - 見出しの`### `は削除する
1. `- `は・に置換する
1. `    `は`\t`に置換する
1. 数字リストアップの重複を修正する
    - もし今操作中の行と前行、どちらも数字でリストアップしているなら
    - かつ、どちらも数値が同じか、操作中の行が小さいなら
    - 操作中の行のリスト番号を、前の行+1にする
