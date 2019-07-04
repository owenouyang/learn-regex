<p align="center">
    <br/>
    <a href="https://github.com/ziishaned/learn-regex">
        <img src="https://i.imgur.com/bYwl7Vf.png" alt="Learn Regex">
    </a>
    <br /><br />
    <p>
        <a href="https://twitter.com/home?status=Learn%20regex%20the%20easy%20way%20by%20%40ziishaned%20http%3A//github.com/ziishaned/learn-regex">
            <img src="https://img.shields.io/badge/twitter-tweet-blue.svg?style=flat-square"/>
        </a>
        <a href="https://twitter.com/ziishaned">
            <img src="https://img.shields.io/badge/feedback-@ziishaned-blue.svg?style=flat-square" />
        </a>
    </p>
</p>

## Translations:

* [English](../README.md)
* [Español](../translations/README-es.md)
* [Français](../translations/README-fr.md)
* [Português do Brasil](../translations/README-pt_BR.md)
* [中文版](../translations/README-cn.md)
* [日本語](../translations/README-ja.md)
* [한국어](../translations/README-ko.md)
* [Turkish](../translations/README-tr.md)
* [Greek](../translations/README-gr.md)
* [Magyar](../translations/README-hu.md)
* [Polish](../translations/README-pl.md)

## 什麼是正則表達式?
 
> 正則表達式是一組由字母和符號組成的特殊文本, 它可以用來從文本中找出滿足你想要的格式的句子.


一個正則表達式是在一個主體字符串中從左到右匹配字符串時的一種樣式.
例如"Regular expression"是一個完整的句子, 但我們常使用縮寫的術語"regex"或"regexp".
正則表達式可以用來替換文本中的字符串,驗證形式,提取字符串等等.

想象你正在寫一個應用, 然後你想設定一個用戶命名的規則, 讓用戶名包含字符,數字,下划線和連字符,以及限制字符的個數,好讓名字看起來沒那麼醜.
我們使用以下正則表達式來驗證一個用戶名:

<br/><br/>
<p align="center">
  <img src="../img/regexp-cn.png" alt="Regular expression">
</p>

以上的正則表達式可以接受 `john_doe`, `jo-hn_doe`, `john12_as`.
但不匹配`Jo`, 因為它包含了大寫的字母而且太短了.

目錄
=================

 * [1. 基本匹配](#1-基本匹配)
 * [2. 元字符](#2-元字符)
 	* [2.1 點運算符 .](#21-點運算符-)
 	* [2.2 字符集](#22-字符集)
		* [2.2.1 否定字符集](#221-否定字符集)
	* [2.3 重復次數](#23-重復次數)
		* [2.3.1 * 號](#231--號)
		* [2.3.2   號](#232--號)
		* [2.3.3 ? 號](#233--號)
	* [2.4 {} 號](#24--號)
	* [2.5 (...) 特徵標群](#25--特徵標群)
	* [2.6 | 或運算符](#26--或運算符)
	* [2.7 轉碼特殊字符](#27-轉碼特殊字符)
	* [2.8 錨點](#28-錨點)
		* [2.8.1 ^ 號](#281--號)
		* [2.8.2 $ 號](#282--號)
* [3. 簡寫字符集](#3-簡寫字符集)
* [4. 前後關聯約束(前後預查)](#4-前後關聯約束前後預查)
	* [4.1 ?=... 前置約束(存在)](#41--前置約束存在)
	* [4.2 ?!... 前置約束-排除](#42--前置約束-排除)
	* [4.3 ?&lt;= ... 後置約束-存在](#43---後置約束-存在)
	* [4.4 ?&lt;!... 後置約束-排除](#44--後置約束-排除)
* [5. 標誌](#5-標誌)
	* [5.1 忽略大小寫 (Case Insensitive)](#51-忽略大小寫-case-insensitive)
	* [5.2 全局搜索 (Global search)](#52-全局搜索-global-search)
	* [5.3 多行修飾符 (Multiline)](#53-多行修飾符-multiline)
* [額外補充](#額外補充)
* [貢獻](#貢獻)
* [許可證](#許可證)

## 1. 基本匹配

正則表達式其實就是在執行搜索時的格式, 它由一些字母和數字組合而成.
例如: 一個正則表達式 `the`, 它表示一個規則: 由字母`t`開始,接著是`h`,再接著是`e`.

<pre>
"the" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat. 
</pre>

[在線練習](https://regex101.com/r/dmRygT/1)

正則表達式`123`匹配字符串`123`. 它逐個字符的與輸入的正則表達式做比較.

正則表達式是大小寫敏感的, 所以`The`不會匹配`the`.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[在線練習](https://regex101.com/r/1paXsy/1)

## 2. 元字符

正則表達式主要依賴於元字符.  
元字符不代表他們本身的字面意思, 他們都有特殊的含義. 一些元字符寫在方括號中的時候有一些特殊的意思. 以下是一些元字符的介紹:

|元字符|描述|
|:----:|----|
|.|句號匹配任意單個字符除了換行符.|
|[ ]|字符種類. 匹配方括號內的任意字符.|
|[^ ]|否定的字符種類. 匹配除了方括號里的任意字符|
|*|匹配>=0個重復的在*號之前的字符.|
|+|匹配>1個重復的+號前的字符.
|?|標記?之前的字符為可選.|
|{n,m}|匹配num個中括號之前的字符 (n <= num <= m).|
|(xyz)|字符集, 匹配與 xyz 完全相等的字符串.|
|&#124;|或運算符,匹配符號前或後的字符.|
|&#92;|轉義字符,用於匹配一些保留的字符 <code>[ ] ( ) { } . * + ? ^ $ \ &#124;</code>|
|^|從開始行開始匹配.|
|$|從末端開始匹配.|

## 2.1 點運算符 `.`

`.`是元字符中最簡單的例子. 
`.`匹配任意單個字符, 但不匹配換行符.
例如, 表達式`.ar`匹配一個任意字符後面跟著是`a`和`r`的字符串.

<pre>
".ar" => The <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[在線練習](https://regex101.com/r/xc9GkU/1)

## 2.2 字符集

字符集也叫做字符類.
方括號用來指定一個字符集.
在方括號中使用連字符來指定字符集的範圍.
在方括號中的字符集不關心順序.
例如, 表達式`[Tt]he` 匹配 `the` 和 `The`.

<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[在線練習](https://regex101.com/r/2ITLQ4/1)

方括號的句號就表示句號.
表達式 `ar[.]` 匹配 `ar.`字符串

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

[在線練習](https://regex101.com/r/wL3xtE/1)

### 2.2.1 否定字符集

一般來說 `^` 表示一個字符串的開頭, 但它用在一個方括號的開頭的時候, 它表示這個字符集是否定的.
例如, 表達式`[^c]ar` 匹配一個後面跟著`ar`的除了`c`的任意字符.

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[在線練習](https://regex101.com/r/nNNlq3/1)

## 2.3 重復次數

後面跟著元字符 `+`, `*` or `?` 的, 用來指定匹配子模式的次數. 
這些元字符在不同的情況下有著不同的意思.

### 2.3.1 `*` 號

`*`號匹配 在`*`之前的字符出現`大於等於0`次.
例如, 表達式 `a*` 匹配以0或更多個a開頭的字符, 因為有0個這個條件, 其實也就匹配了所有的字符. 表達式`[a-z]*` 匹配一個行中所有以小寫字母開頭的字符串.

<pre>
"[a-z]*" => T<a href="#learn-regex"><strong>he</strong></a> <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>parked</strong></a> <a href="#learn-regex"><strong>in</strong></a> <a href="#learn-regex"><strong>the</strong></a> <a href="#learn-regex"><strong>garage</strong></a> #21.
</pre>

[在線練習](https://regex101.com/r/7m8me5/1)

`*`字符和`.`字符搭配可以匹配所有的字符`.*`.
`*`和表示匹配空格的符號`\s`連起來用, 如表達式`\s*cat\s*`匹配0或更多個空格開頭和0或更多個空格結尾的cat字符串.

<pre>
"\s*cat\s*" => The fat<a href="#learn-regex"><strong> cat </strong></a>sat on the <a href="#learn-regex">con<strong>cat</strong>enation</a>.
</pre>

[在線練習](https://regex101.com/r/gGrwuz/1)

### 2.3.2 `+` 號

`+`號匹配`+`號之前的字符出現 >=1 次個字符.
例如表達式`c.+t` 匹配以首字母`c`開頭以`t`結尾,中間跟著任意個字符的字符串.

<pre>
"c.+t" => The fat <a href="#learn-regex"><strong>cat sat on the mat</strong></a>.
</pre>

[在線練習](https://regex101.com/r/Dzf9Aa/1)

### 2.3.3 `?` 號

在正則表達式中元字符 `?` 標記在符號前面的字符為可選, 即出現 0 或 1 次.
例如, 表達式 `[T]?he` 匹配字符串 `he` 和 `The`.

<pre>
"[T]he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[在線練習](https://regex101.com/r/cIg9zm/1)

<pre>
"[T]?he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in t<a href="#learn-regex"><strong>he</strong></a> garage.
</pre>

[在線練習](https://regex101.com/r/kPpO2x/1)

## 2.4 `{}` 號

在正則表達式中 `{}` 是一個量詞, 常用來一個或一組字符可以重復出現的次數.
例如,  表達式 `[0-9]{2,3}` 匹配 2~3 位 0~9 的數字.


<pre>
"[0-9]{2,3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[在線練習](https://regex101.com/r/juM86s/1)

我們可以省略第二個參數.
例如, `[0-9]{2,}` 匹配至少兩位 0~9 的數字.

如果逗號也省略掉則表示重復固定的次數. 
例如, `[0-9]{3}` 匹配3位數字

<pre>
"[0-9]{2,}" => The number was 9.<a href="#learn-regex"><strong>9997</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[在線練習](https://regex101.com/r/Gdy4w5/1)

<pre>
"[0-9]{3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to 10.0.
</pre>

[在線練習](https://regex101.com/r/Sivu30/1)

## 2.5 `(...)` 特徵標群

特徵標群是一組寫在 `(...)` 中的子模式. 例如之前說的 `{}` 是用來表示前面一個字符出現指定次數. 但如果在 `{}` 前加入特徵標群則表示整個標群內的字符重復 N 次. 例如, 表達式 `(ab)*` 匹配連續出現 0 或更多個 `ab`.

我們還可以在 `()` 中用或字符 `|` 表示或. 例如, `(c|g|p)ar` 匹配 `car` 或 `gar` 或 `par`.

<pre>
"(c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[在線練習](https://regex101.com/r/tUxrBG/1)

## 2.6 `|` 或運算符

或運算符就表示或, 用作判斷條件.

例如 `(T|t)he|car` 匹配 `(T|t)he` 或 `car`.

<pre>
"(T|t)he|car" => <a href="#learn-regex"><strong>The</strong></a> <a href="#learn-regex"><strong>car</strong></a> is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[在線練習](https://regex101.com/r/fBXyX0/1)

## 2.7 轉碼特殊字符

反斜線 `\` 在表達式中用於轉碼緊跟其後的字符. 用於指定 `{ } [ ] / \ + * . $ ^ | ?` 這些特殊字符. 如果想要匹配這些特殊字符則要在其前面加上反斜線 `\`.

例如 `.` 是用來匹配除換行符外的所有字符的. 如果想要匹配句子中的 `.` 則要寫成 `\.`.

<pre>
"(f|c|m)at\.?" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> sat on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[在線練習](https://regex101.com/r/DOc5Nu/1)

## 2.8 錨點

在正則表達式中, 想要匹配指定開頭或結尾的字符串就要使用到錨點. `^` 指定開頭, `$` 指定結尾.

### 2.8.1 `^` 號

`^` 用來檢查匹配的字符串是否在所匹配字符串的開頭.

例如, 在 `abc` 中使用表達式 `^a` 會得到結果 `a`. 但如果使用 `^b` 將匹配不到任何結果. 應為在字符串 `abc` 中並不是以 `b` 開頭.

例如, `^(T|t)he` 匹配以 `The` 或 `the` 開頭的字符串.

<pre>
"(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[在線練習](https://regex101.com/r/5ljjgB/1)

<pre>
"^(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[在線練習](https://regex101.com/r/jXrKne/1)

### 2.8.2 `$` 號

同理於 `^` 號, `$` 號用來匹配字符是否是最後一個.

例如, `(at\.)$` 匹配以 `at.` 結尾的字符串.

<pre>
"(at\.)" => The fat c<a href="#learn-regex"><strong>at.</strong></a> s<a href="#learn-regex"><strong>at.</strong></a> on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[在線練習](https://regex101.com/r/y4Au4D/1)

<pre>
"(at\.)$" => The fat cat. sat. on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[在線練習](https://regex101.com/r/t0AkOd/1)

##  3. 簡寫字符集

正則表達式提供一些常用的字符集簡寫. 如下:

|簡寫|描述|
|:----:|----|
|.|除換行符外的所有字符|
|\w|匹配所有字母數字, 等同於 `[a-zA-Z0-9_]`|
|\W|匹配所有非字母數字, 即符號, 等同於: `[^\w]`|
|\d|匹配數字: `[0-9]`|
|\D|匹配非數字: `[^\d]`|
|\s|匹配所有空格字符, 等同於: `[\t\n\f\r\p{Z}]`|
|\S|匹配所有非空格字符: `[^\s]`|

## 4. 前後關聯約束(前後預查)

前置約束和後置約束都屬於**非捕獲簇**(用於匹配不在匹配列表中的格式).
前置約束用於判斷所匹配的格式是否在另一個確定的格式之後.

例如, 我們想要獲得所有跟在 `$` 符號後的數字, 我們可以使用正向向後約束 `(?<=\$)[0-9\.]*`.
這個表達式匹配 `$` 開頭, 之後跟著 `0,1,2,3,4,5,6,7,8,9,.` 這些字符可以出現大於等於 0 次.

前後關聯約束如下:

|符號|描述|
|:----:|----|
|?=|前置約束-存在|
|?!|前置約束-排除|
|?<=|後置約束-存在|
|?<!|後置約束-排除|

### 4.1 `?=...` 前置約束(存在)

`?=...` 前置約束(存在), 表示第一部分表達式必須跟在 `?=...`定義的表達式之後.

返回結果只瞞住第一部分表達式.
定義一個前置約束(存在)要使用 `()`. 在括號內部使用一個問號和等號: `(?=...)`. 

前置約束的內容寫在括號中的等號後面.
例如, 表達式 `[T|t]he(?=\sfat)` 匹配 `The` 和 `the`, 在括號中我們又定義了前置約束(存在) `(?=\sfat)` ,即 `The` 和 `the` 後面緊跟著 `(空格)fat`.

<pre>
"[T|t]he(?=\sfat)" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[在線練習](https://regex101.com/r/IDDARt/1)

### 4.2 `?!...` 前置約束-排除

前置約束-排除 `?!` 用於篩選所有匹配結果, 篩選條件為 其後不跟隨著定義的格式
`前置約束-排除`  定義和 `前置約束(存在)` 一樣, 區別就是 `=` 替換成 `!` 也就是 `(?!...)`. 

表達式 `[T|t]he(?!\sfat)` 匹配 `The` 和 `the`, 且其後不跟著 `(空格)fat`.

<pre>
"[T|t]he(?!\sfat)" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[在線練習](https://regex101.com/r/V32Npg/1)

### 4.3 `?<= ...` 後置約束-存在

後置約束-存在 記作`(?<=...)` 用於篩選所有匹配結果, 篩選條件為 其前跟隨著定義的格式.
例如, 表達式 `(?<=[T|t]he\s)(fat|mat)` 匹配 `fat` 和 `mat`, 且其前跟著 `The` 或 `the`.

<pre>
"(?<=[T|t]he\s)(fat|mat)" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[在線練習](https://regex101.com/r/avH165/1)

### 4.4 `?<!...` 後置約束-排除

後置約束-排除 記作 `(?<!...)` 用於篩選所有匹配結果, 篩選條件為 其前不跟著定義的格式.
例如, 表達式 `(?<!(T|t)he\s)(cat)` 匹配 `cat`, 且其前不跟著 `The` 或 `the`.

<pre>
"(?&lt;![T|t]he\s)(cat)" => The cat sat on <a href="#learn-regex"><strong>cat</strong></a>.
</pre>

[在線練習](https://regex101.com/r/8Efx5G/1)

## 5. 標誌

標誌也叫修飾語, 因為它可以用來修改表達式的搜索結果.
這些標誌可以任意的組合使用, 它也是整個正則表達式的一部分.

|標誌|描述|
|:----:|----|
|i|忽略大小寫.|
|g|全局搜索.|
|m|多行的: 錨點元字符 `^` `$` 工作範圍在每行的起始.|

### 5.1 忽略大小寫 (Case Insensitive)

修飾語 `i` 用於忽略大小寫.
例如, 表達式 `/The/gi` 表示在全局搜索 `The`, 在後面的 `i` 將其條件修改為忽略大小寫, 則變成搜索 `the` 和 `The`, `g` 表示全局搜索.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[在線練習](https://regex101.com/r/dpQyf9/1)

<pre>
"/The/gi" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[在線練習](https://regex101.com/r/ahfiuh/1)

### 5.2 全局搜索 (Global search)

修飾符 `g` 常用語執行一個全局搜索匹配, 即(不僅僅返回第一個匹配的, 而是返回全部). 
例如, 表達式 `/.(at)/g` 表示搜索 任意字符(除了換行) + `at`, 並返回全部結果.

<pre>
"/.(at)/" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the mat.
</pre>

[在線練習](https://regex101.com/r/jnk6gM/1)

<pre>
"/.(at)/g" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> <a href="#learn-regex"><strong>sat</strong></a> on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[在線練習](https://regex101.com/r/dO1nef/1)

### 5.3 多行修飾符 (Multiline)

多行修飾符 `m` 常用語執行一個多行匹配. 

像之前介紹的 `(^,$)` 用於檢查格式是否是在待檢測字符串的開頭或結尾. 但我們如果想要它在每行的開頭和結尾生效, 我們需要用到多行修飾符 `m`.

例如, 表達式 `/at(.)?$/gm` 表示在待檢測字符串每行的末尾搜索 `at`後跟一個或多個 `.` 的字符串, 並返回全部結果.

<pre>
"/.at(.)?$/" => The fat
                cat sat
                on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[在線練習](https://regex101.com/r/hoGMkP/1)

<pre>
"/.at(.)?$/gm" => The <a href="#learn-regex"><strong>fat</strong></a>
                  cat <a href="#learn-regex"><strong>sat</strong></a>
                  on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[在線練習](https://regex101.com/r/E88WE2/1)

## 額外補充

* *正整數*: `^\d+$`
* *負整數*: `^-\d+$`
* *手機國家號*: `^+?[\d\s]{3,}$`
* *手機號*: `^+?[\d\s]+(?[\d\s]{10,}$`
* *整數*: `^-?\d+$`
* *用戶名*: `^[\w\d_.]{4,16}$`
* *數字和英文字母*: `^[a-zA-Z0-9]*$`
* *數字和應為字母和空格*: `^[a-zA-Z0-9 ]*$`
* *密碼*: `^(?=^.{6,}$)((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.*$`
* *郵箱*: `^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4})*$`
* *IP4 地址*: `^((?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?))*$`
* *純小寫字母*: `^([a-z])*$`
* *純大寫字母*: `^([A-Z])*$`
* *URL*: `^(((http|https|ftp):\/\/)?([[a-zA-Z0-9]\-\.])+(\.)([[a-zA-Z0-9]]){2,4}([[a-zA-Z0-9]\/+=%&_\.~?\-]*))*$`
* *VISA 信用卡號*: `^(4[0-9]{12}(?:[0-9]{3})?)*$`
* *日期 (MM/DD/YYYY)*: `^(0?[1-9]|1[012])[- /.](0?[1-9]|[12][0-9]|3[01])[- /.](19|20)?[0-9]{2}$`
* *日期 (YYYY/MM/DD)*: `^(19|20)?[0-9]{2}[- /.](0?[1-9]|1[012])[- /.](0?[1-9]|[12][0-9]|3[01])$`
* *MasterCard 信用卡號*: `^(5[1-5][0-9]{14})*$`

## 貢獻

* 報告問題
* 開放合併請求
* 傳播此文檔
* 直接和我聯繫 ziishaned@gmail.com 或 [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/ziishaned.svg?style=social&label=Follow%20%40ziishaned)](https://twitter.com/ziishaned)

## 許可證

MIT &copy; [Zeeshan Ahmad](https://twitter.com/ziishaned)
