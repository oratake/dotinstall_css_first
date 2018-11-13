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
CSSでは上のプロパティからどんどん適用されるので、  
指定が重複した際は**後のプロパティ**が使われる

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

### セレクタ
セレクタにはhtmlタグ、class属性、id属性など使用できる

### CSSの確認(Chromeの開発者ツール)
chromeで `⌘ + Shift + i` (Winは `Ctrl + Shift + i` ) で開く開発者ツールを使う。  
※見たい要素を選び`右クリック → 検証`で、ハイライトされた状態で開発者ツールが開く。  

- Elements > Styles  
選択した要素に対して、どこでどんなプロパティが指定されているか見られる。  
user agent stylesheetsはブラウザ既定のもの。
- Elements > Computed  
最終的な出力をすべて見られる。  
Show allで親要素分まで見える。

### 色指定
color系の指定では様々な指定方法がある。  
1. 色名指定  
ex) `color: red;`  
1. 16進数  
ex) `#FFF` `#114514` 3or6桁で指定  

※ただし、弊社では`rgb()`や色名での表記はせず、#16進数で記述する。透明度指定をする場合にのみ`rgba()`で指定。
