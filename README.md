# japanese-regulation

日本語の規程文書を、Typst標準の構造を活かして記述するための小さなパッケージです。

- 章・節：標準の見出し（`=`、`==`）
- 条：`article`
- 項・号：標準の入れ子列挙（`+`）
- 参照：標準のラベルと `@ラベル`
- 目次：章・節・条から自動生成

## 使用例

```typst
#import "@preview/japanese-regulation:0.1.0": article, regulation

#show: regulation.with(
  title: "就業規則",
  config: (
    short-chapter-gap: 2em,
    short-section-gap: 2em,
    toc-depth: 3,
  ),
)

= 総則

#article(<目的>)[
  + この規則の目的を定めます。
]

#article(<適用範囲>)[
  + #ref(<目的>)に基づき、適用範囲を定めます。
]
```

日本語がラベル名の続きとして解釈される場合があるため、参照の直後へ助詞などを
続けるときは `#ref(<目的>)に` のように参照範囲を明示します。

リポジトリ内のexampleは、パッケージディレクトリをproject rootに指定して確認できます。

```sh
typst compile --root . examples/basic.typ /tmp/basic.pdf
```

（上のコマンドは `packages/japanese-regulation` で実行します。Noto CJKを
利用環境へインストールしてください。）

既定では本文に `Noto Serif CJK JP`、見出しに `Noto Sans CJK JP` を指定します。
パッケージにはフォントを同梱しないため、利用環境でフォントを用意してください。

書式の既定値は `default-config` に集約されています。変更する値だけを
`regulation(config: (...))` へ渡せます。

文書メタデータは `title` / `author`、フォントは `config` の `body-font` /
`heading-font`、表紙と目次は `cover` / `toc` で設定できます。
1つのコンパイル単位では `regulation` を1回だけ使用してください。
目次はコンパイル単位全体の見出しを検索するため、複数文書の結合には対応しません。

サポート対象の公開APIは `regulation`、`article`、`default-config` です。
アンダースコアで始まる名前は内部実装であり、互換性の対象外です。

条番号は `article` の出現順だけで決まります。番号を明示する引数はありません。
枝番条（`第96条の2`）にも対応しません。

## ライセンス

MIT-0
