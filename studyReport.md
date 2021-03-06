# CSS入門

[CSS入門](https://dotinstall.com/lessons/basic_css_v4)のレポート。

## CSSの基本スタイル
```css
/* セレクタ(どこにあてるか) */
.selector {
  /* プロパティ: 値; (何をどのぐらいあてるか) */
  width: 70vw;
}
```

### 書ける場所
主に3つ書ける場所がある。
1. htmlタグのstyle属性として  
  ex) `<h1 style="color: #114514; line-height: 1.5;">`
1. htmlの `head > style` 内にべた書き  
1. htmlの `head > link` でCSSファイルを別途指定  
  ex)
```html
<head>
  <link rel="stylesheet" type="text/css" href="./css/style.css">
</head>
```

## セレクタ
セレクタにはhtmlタグ、class属性、id属性など使用できる。  
classやidはhtmlタグに属性として`class="クラス名"`と記述する。  
classは`.class名`、idは`#id名`と記述する。  
原則、**タグに直接指定をしない**こと。  

### 指定の種類
- 複数を一度に指定  
`,`(カンマ)区切り `h1, h2, h3`  
- 子要素(孫以降も全て)に適用  
` `(スペース)区切り `#id p`(id以下**すべて**のp)  
- 1つ下の階層の子要素にのみ  
`>`(不等号)区切り `#id p`(id**直下の**pのみ)  
- n番目の要素のみ (:nth-child)  
模擬クラスを用いて指定。  
`:first-child` 最初の要素のみ  
`:last-child` 最後の要素のみ  
`:nth-child(奇数か偶数)` oddで奇数、evenで偶数の指定
`:nth-child(自然数nの数式)` 3nなら3の倍数など

### CSSの適用順序
CSSの順序は、  

- 指定が重複した際は**後のプロパティ**が使われる。
- **classよりidの指定が優先**される。  
- さらに、**具体的・局所的なスタイルが優先**される。  

つまるところ、  

1. `p#id` (要素を特定したid)
1. `#id` (要素を特定しないid)
1. `p.class` (要素を特定したclass)
1. `.class` (要素を特定しないclass)
1. `p` (タイプセレクタ)
1. `*` (全称セレクタ)  

の順序で適用される。  
がしかし、  
`!important`が値に指定されると、どれよりも最優先になる。  
ex) `p {color: #114514 !important;}`

## 各種プロパティ

### 色指定
color系の指定では様々な指定方法がある。  
1. 色名指定  
ex) `color: red;`  
1. 16進数  
ex) `#FFF` `#114514` 3or6桁で指定  
1. rgb指定  
ex) `rgb(255, 0, 0)` 0-255で指定 `rgba(114, 36, 4, 0.8)` 透明度は0-1で指定  

※ただし、弊社では`rgb()`や色名での表記はせず、基本#16進数で記述する。  
透明度指定をする必要がある場合にのみ`rgba()`で指定。  

なお透明度のみ指定したい場合は、  
`opacity: 0から1;` を用いる。

### 余白(margin, padding)
余白については、プロパティで四方個別に指定↓  
ex)  
```css
margin-top: 0px;
margin-right: 0px;
margin-bottom: 0px;
margin-left: 0px;
```
のほか、ショートハンドでの指定↓  
ex)  
```css
/* 基本順序は時計回り */
margin: 0; /* 四方 0 */
margin: 0 10px; /* 上下0, 左右10px */
margin: 0 10px 20px; /* 上0, 左右10px, 下20px */
margin: 0 10px 20px 100px; /* 上0, 右10px, 下20px, 左100px */
/* paddingも同様 */
```
が可能。  
※弊社では1つ指定の場合、topなどで指定するが、2つ以上はすべてショートハンド指定。  

- marginの相殺  
marginは**上下方向に限り**、marginが隣接した場合、marginの小さい方が大きいほうに吸収される。  
ex) div.1+div.2のとき  
```css
.1 {margin-bottom: 30px;}
.2 {margin-top: 40px;}
```
このとき、.1と.2の間隔は.1のmargin-bottomが吸収されて40pxになる。

### リスト関係
ex) `ul>li` のとき  
- `list-style-type` \[none, disc(黒丸), circle(白丸), square(四角) など...\]  
マーカー文字の指定。消したいときはnoneで。  
- liを横に並べる (`li {display: inline-block;}`)  
liはブロック要素なので、横に並べるためにインライン要素にする。  

### aタグ(リンク系)
- リンクにしたときの色や下線を消す  
`test-decoration` noneで色を消せる  
`color: inherit;` 親要素の色の値を強制的に引き継ぐ  

- 擬似クラス  
特定の状態にあることを表現するためのセレクタ。  
ex) `a:hover {color: #F00;}` (a要素にマウスオーバーした状態で文字を赤に)  

### 文字の指定
`color:` 文字色  
`text-align:` \[center, left, right\] 文字寄せ(画像も寄る)  
`font-weight:` 太さの指定

### 背景の設定
`background` 基本。色などまとめて指定できる。  
- 背景画像を中央に寄せたい  
```css
background-image: url(./パス/指定);
backgorund-position: 50% 50%;
```

### ブロックに対して
- ブロックの角を丸くしたい、ブロック自体を丸くしたい  
`border-radius:` px指定でも、%指定でも使える。  
- ブロックの境界を指定したい  
`border: 幅 スタイル 色;` 個別指定はそれぞれ、-width -style -colorをつけて指定  
- 影をつける  
`box-shadow: x位置 y位置 ブラーの大きさ 色;` x, y位置はプラス方向がそれぞれ下と右  
- ブロックの左,右,中央寄せ  
`text-aligh: center;` などではインライン要素しか動かないので、marginにautoを指定する。  
ex)  
```css
margin-left: auto; /* 右寄せ */
margin-right: auto; /* 左寄せ */
margin: 0 auto; /* 中央寄せ */
```

### ボックスを横並びにする
1. floatを使う方法  
ex) div.cf>div.1+div.2 を横並びにする場合  
```css
div.1 {
  width: 200px;
  float: left;
}
div.2 {
  width: 300px;
  float: right;
}
```
- width指定が必須  
- 3個以上は煩雑になりがち  
- 親要素でclearfixしないと他の要素まで回り込む。(親要素に`overflow: hidden;`を指定する方法も)  
※弊社の使うreset.cssでは、親要素に`.cf`をつけてclearfixできる。  

1. inline-blockを使う方法  
ex) `ul>li*複数` のとき  
```css
ul {font-size: 0;}
li {display: inline-block;}
```
- 幅指定なしでよい  
- 回り込みの解除を設定することもない。  
- 隙間が空くので、親要素に`text-size: 0;`を指定する。  
- 要素の縦がバラバラのときは`vertical-align: top;`で上揃えで並ぶ。  

## CSSの確認(Chromeの開発者ツール)
chromeで `⌘ + Shift + i` (Winは `Ctrl + Shift + i` ) で開く開発者ツールを使う。  
※見たい要素を選び`右クリック → 検証`で、ハイライトされた状態で開発者ツールが開く。  

- Elements > Styles  
選択した要素に対して、どこでどんなプロパティが指定されているか見られる。  
user agent stylesheetsはブラウザ既定のもの。
- Elements > Computed  
最終的な出力をすべて見られる。  
Show allで親要素分まで見える。  

### 余白の探し方
開発者ツールのElementsで要素をマウスオーバーすると、ページがハイライトされる。  
緑: padding  
橙: margin  
なので、細かい要素から親の親の親...とたどって探していく。
