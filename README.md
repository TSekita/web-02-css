# web-02-css

## 1. このリポジトリの目的

`web-02-css` は、Azure Cloud App 開発へ段階的に進むための、CSS 基礎学習用リポジトリです。
前段階の `web-01-html` で作った Machine Monitor の文書構造を保ちながら、外部 CSS を追加します。

この段階で重視する役割分担は次のとおりです。

- **HTML**: 文書の構造と意味を表す
- **CSS**: 表示、レイアウト、装飾を指定する

完成したデザインの複雑さではなく、「HTML に CSS を加えると表示がどう変わるか」を追跡できることを目標にしています。

## 2. `web-01-html` との違い

`web-01-html` では、ブラウザは HTML を解析して DOM（Document Object Model）を作り、ブラウザ標準のスタイルで表示していました。

```text
web-01-html

Browser
   ↓
index.html
   ↓
HTMLを解析
   ↓
DOM
   ↓
ブラウザ標準スタイルで表示
```

`web-02-css` では、同じ文書構造に `style.css` の CSS ルールを適用します。CSS は文書の内容を追加するものではなく、DOM の各要素をどのように表示するかを指定します。

```text
web-02-css

Browser
   ├── index.html
   │       ↓
   │      DOM
   │
   └── style.css
           ↓
       CSSルール
           ↓
   DOM + CSS
           ↓
         表示
```

CSS を無効にしても、見出し、説明、機器情報、表、ボタンという HTML の構造と内容は残ります。

## 3. HTML と CSS の役割

`index.html` では、`header`、`main`、`section`、`article`、`table` などを使って情報の意味と関係を表現します。
色、余白、枠線、要素の並び方は `style.css` に記述します。

役割を分けることで、次のことが分かりやすくなります。

- HTML だけを読んで文書の構造を理解できる
- 見た目を変更するときは CSS を探せばよい
- 同じ CSS ルールを複数の HTML 要素で再利用できる

## 4. ファイル構成

```text
web-02-css/
├── index.html   # Machine Monitor の構造と内容
├── style.css    # 表示、レイアウト、装飾
└── README.md    # CSS 基礎の学習ノート
```

`index.html` をブラウザで開けば動作を確認できます。ビルドやサーバー起動は不要です。

## 5. CSS の読み込み方法

`index.html` の `head` にある `link` 要素が、外部 CSS ファイルを読み込みます。

```html
<link rel="stylesheet" href="style.css">
```

- `link`: HTML と外部リソースの関係を示す要素
- `rel="stylesheet"`: 読み込むファイルがスタイルシートであることを示す
- `href="style.css"`: 読み込むファイルの場所を示す

CSS は HTML 内の `style` 要素や `style` 属性には書かず、`style.css` に分離しています。

## 6. CSS ルールセットとセレクタ

CSS は「どの要素に」「何を」「どの値で」適用するかを記述します。

```css
.machine {
  border: 1px solid #cbd5e1;
}
```

- `.machine`: 対象を指定する**セレクタ**
- `border`: 変更する項目を示す**プロパティ**
- `1px solid #cbd5e1`: プロパティに設定する**値**
- `{` から `}` まで: ひとまとまりの**ルールセット**
- `border: 1px solid #cbd5e1;`: ひとつの**宣言**

このリポジトリでは、3種類の基本的なセレクタを確認できます。

### 要素セレクタ

```css
body {
  color: #1e293b;
}
```

同じ名前の HTML 要素すべてを対象にします。本文全体や、すべての見出し・表・ボタンに共通する基本スタイルに使っています。

### class セレクタ

```css
.machine {
  padding: 24px;
}
```

`class="machine"` を持つ要素を対象にします。同じ役割を持つ Machine-A と Machine-B の両方に再利用できます。

### id セレクタ

```css
#machine-monitor {
  max-width: 960px;
}
```

`id="machine-monitor"` を持つ一意な要素を対象にします。このページでは、監視画面全体を表す `main` にだけ使用しています。

## 7. class と id の違い

| 種類 | 主な用途 | 再利用 |
| --- | --- | --- |
| `class` | 同じ役割や状態を持つ要素をまとめる | 複数要素で使用できる |
| `id` | ページ内の一意な要素を識別する | 同じ値はページ内で1回だけ |

機器カードには `.machine`、状態表示には `.machine-status` のような class を使います。Online と Offline には、それぞれの状態という意味を表す `.status-online` と `.status-offline` を使います。

id セレクタは class セレクタより詳細度が高く、上書き関係が複雑になりやすいため、多用しません。繰り返し使う装飾には class を優先します。

## 8. 基本的なプロパティと値

実際の表示では、次のプロパティを確認できます。

| 目的 | プロパティ例 |
| --- | --- |
| 文字色 | `color: #1e293b;` |
| 背景色 | `background-color: #ffffff;` |
| フォントサイズ | `font-size: 32px;` |
| 文字の太さ | `font-weight: 700;` |
| 外側の余白 | `margin: 24px;` |
| 内側の余白 | `padding: 24px;` |
| 枠線 | `border: 1px solid #cbd5e1;` |
| 幅 | `width: 100%;` |
| 高さ | `height: 44px;` |

プロパティは「何を変更するか」、値は「どのように変更するか」を表します。

## 9. Box Model

ブラウザは、多くの HTML 要素を四角い箱として扱います。この仕組みを **Box Model** と呼びます。

```text
margin（ほかの要素との外側の間隔）
  └─ border（箱の枠線）
       └─ padding（枠線と内容の間隔）
            └─ content（文字などの内容）
```

このページでは `.machine` が分かりやすい確認対象です。

- **content**: 機器名、説明、状態
- **padding**: 内容とカードの枠線との間
- **border**: カードを囲む線
- **margin**: 機器一覧と次のセクションとの間など、要素の外側の空間

`width` や `height` は基本的にcontent領域を指定します。`box-sizing: border-box` が指定された要素では、指定した幅や高さにpaddingとborderも含まれます。

## 10. Flexbox の基本

Flexbox は、複数の要素を一方向に並べ、位置や間隔を調整するレイアウト方法です。機器カードの一覧 `.machine-list` と操作ボタンの `.actions` で使用しています。

```css
.machine-list {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: stretch;
  gap: 24px;
}
```

- `display: flex`: 子要素をFlexboxで配置する
- `flex-direction`: 子要素を並べる方向を決める
- `justify-content`: 並べる方向に沿った配置を決める
- `align-items`: 並べる方向と交差する方向の配置を決める
- `gap`: 子要素同士の間隔を決める

画面が狭い場合は、読みやすさを保つためにカードとボタンを縦方向へ並べます。

## 11. Developer Tools で CSS を確認する方法

ブラウザによって名称は多少異なりますが、Chrome や Edge では次の手順で確認できます。

1. `index.html` をブラウザで開きます。
2. ページ上で右クリックし、**検証**を選んでDeveloper Toolsを開きます。
3. **Elements**パネルで `header`、`main`、`.machine-list`、`.machine` などのDOM構造を確認します。
4. Machine-Aの `.machine` 要素を選択します。
5. **Styles**パネルで、`style.css` のどのCSSルールが適用されているか確認します。
6. **Computed**パネルのBox Model図で、content、padding、border、marginを確認します。
7. **Styles**パネルで `background-color` や `padding` のチェックを一時的に外し、表示の変化を確認します。
8. 値をダブルクリックして、たとえば `padding: 24px` を `padding: 4px` に一時変更します。
9. ページを再読み込みし、Developer Tools上の一時変更が元に戻ることを確認します。

Developer Toolsでの変更は元の `style.css` へ保存されないため、安全に比較できます。

## 12. CSS を無効にして HTML だけの表示へ戻す方法

CSS適用前後を比較するには、`index.html` の次の行を一時的にコメントアウトします。

```html
<!-- <link rel="stylesheet" href="style.css"> -->
```

保存して再読み込みすると、HTMLの内容は変わらず、ブラウザ標準スタイルの表示へ戻ります。確認後はコメントを外してください。

Developer ToolsのElementsパネルで `link` 要素を一時的に削除する方法や、Networkパネルのリクエストブロック機能で `style.css` を止める方法でも比較できます。これらの変更も再読み込みすれば元に戻ります。

## 13. 今回意図的に使用していない技術

この段階ではHTMLとCSSだけに集中するため、次の技術は使用していません。

- JavaScript / TypeScript
- React / Vue / Angular
- Bootstrap / Tailwind CSSなどのCSSフレームワーク
- Node.js / Python / FastAPIなどの実行環境やWebフレームワーク
- 外部ライブラリ / CDN
- データベース
- Docker
- Azureサービス

操作ボタンはHTML要素として表示しますが、クリックによる状態変更は行いません。

## 14. 次段階で追加する予定の技術

次段階以降ではJavaScriptを追加し、ボタン操作、イベント、DOMの変更、Machineの状態更新などを学習する予定です。このリポジトリでは先行して実装せず、静的なHTMLとCSSの関係だけを扱います。
