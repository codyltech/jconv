jconv
====================
> Iconv.js for Japanese characters.

 * This module supported the encoding commonly used in japanese:  
   *Shift_JIS(CP932), ISO-2022-JP(-1), EUC-JP, UTF8* conversion.
 * Pure Javascript, no compile needed.
 * Almost much faster than node-iconv.

### Install
```
npm install jconv
```

### Usage
An example simply convert **EUC-JP** to **Shift_JIS** :

```javascript
var jconv = require( 'jconv' );

var converted = jconv.convert( buffer, 'EUCJP', 'SJIS' );
```

<!-- Also available **node-iconv-lite** syntax:
```javascript
var string = jconv.decode( buffer, fromEncoding );
```
```javascript
var buffer = jconv.encode( string, toEncoding );
``` -->

### API

* **jconv( input, from, to )**  
* **jconv.convert( input, from, to )**  
`input` is {Buffer} or {String}.  
`from`, `to` are {String}: *Shift_JIS(SJIS), ISO-2022-JP(JIS), EUCJP, UTF8* are available.  
`return` value is {Buffer}.

<!-- * #####`jconv.decode( inputBuffer, from )`

* #####`jconv.encode( inputString, to )` 

 -->

### Speed
Comparison with node-iconv@ 2.0.7 by converting ["Kokoro by NatsumeSoseki(夏目 漱石)"](http://www.aozora.gr.jp/cards/000148/files/773_14560.html)
using [Benchmark.js](https://github.com/bestiejs/benchmark.js).  
Environment is Windows7, core i5 2405-S, mem8G, Node 0.10.22.
(Please check on your hardware.)  
`Gray` is iconv and `Blue` is jconv.  

![jconv - encoding speed test chart](https://dl.dropboxusercontent.com/s/rz14axy7ie96o71/speedLog.png?dl=1&token_hash=AAH0Cmp7uzDES2aj9VtQaYI1rKDxcLhqs5YbBY0ZKF0ksw)
[[log]](https://raw.github.com/narirou/jconv/master/test/chart/speedLog.txt)  

### Encodings
 * Supported Windows Dependent Characters <-> JIS Conversion.  
[(problem details)](http://support.microsoft.com/default.aspx?scid=kb;ja;JP170559)  

 * "JIS X 0208", "JIS X 0212" and "CP932" have Unicode Table Differences, the specific characters(～￠￡∥ etc...) cannot be round-trip converted by default.  
 So this module fix this defference as possible when converting.  
[(problem details)](http://www8.plala.or.jp/tkubota1/unicode-symbols-map2.html)  

### Based on
 * [iconv-lite](https://github.com/ashtuchkin/iconv-lite) by ashtuchkin.
 * [node-iconv](https://github.com/bnoordhuis/node-iconv) by bnoordhuis.
 * [Encoding.js](https://github.com/polygonplanet/Unzipper.js) by polygonplanet.
 * [libiconv-1.9.1-ja-patch Description](http://www2d.biglobe.ne.jp/~msyk/software/libiconv-1.9.1-patch.html)

Thank you so much!

### Note
Pull requests are welcome.

### TODO
 * native encoding support
 * unit test
