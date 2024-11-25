jconv
=====

> Pure JavaScript Iconv for Japanese encodings.

[![Build Status][travis-image]][travis-url]
[![Npm Modules][npm-image]][npm-url]
[![MIT Licensed][license-image]][license-url]

[travis-image]: https://img.shields.io/travis/narirou/jconv.svg?style=flat-square
[travis-url]: https://travis-ci.org/narirou/jconv
[npm-image]: http://img.shields.io/npm/v/jconv.svg?style=flat-square
[npm-url]: https://www.npmjs.org/package/jconv
[license-image]: http://img.shields.io/badge/license-MIT-blue.svg?style=flat-square
[license-url]: http://opensource.org/licenses/MIT


 * This module supports the encodings commonly used in the Japanese Language:  
   *Shift_JIS(CP932), ISO-2022-JP(-1), EUC-JP, UTF8, UNICODE(UCS2)* conversion.
 * Pure Javascript, no need to compile.
 * Much faster than [node-iconv](https://github.com/bnoordhuis/node-iconv).

[[Japanese 日本語]](https://github.com/narirou/jconv/blob/master/READMEja.md)



Installation
------------

```bash
$ npm install jconv
```



Usage
-----

For example simply convert from **EUC-JP** to **Shift_JIS**:

```javascript
var jconv = require( 'jconv' );

var SJISBuffer = jconv.convert( EUCJPBuffer, 'EUCJP', 'SJIS' );
```

Also available **iconv-lite** syntax:

```javascript
var str = jconv.decode( buffer, fromEncoding );

var buf = jconv.encode( 'string', toEncoding );
```



API
---

 * **jconv( input, fromEncoding, toEncoding )**  
 * **jconv.convert( input, fromEncoding, toEncoding )**  
    * `input` {Buffer} or {String}  
    * `fromEncoding`, `toEncoding` {String}:  
       *Shift_JIS(SJIS), ISO-2022-JP(JIS), EUCJP, UTF8, UNICODE(UCS2, UTF16LE)* are available.  
    * `return` {Buffer}  

 * **jconv.decode( inputBuffer, fromEncoding )**  
    * `return` {String}  

 * **jconv.encode( inputString, toEncoding )**  
    * `return` {Buffer}  

 * **jconv.encodingExists( encodingName )**  
    * `return` {Boolean}



Performance
-----------

Comparison with node-iconv@2.0.7 by converting [Japanese text](http://www.aozora.gr.jp/cards/000148/files/773_14560.html)
using [Benchmark.js](https://github.com/bestiejs/benchmark.js).  
Environment is *Windows7, core i5 2405-S, mem8G, Node 0.10.22*.
(Please check on your hardware.)  
`Gray`: iconv, `Blue`: jconv (higher is better)  

![jconv - encoding speed test chart](https://raw.github.com/narirou/jconv/master/test/chart/speedLog.png)
[[latest log]](https://github.com/narirou/jconv/blob/master/test/chart/speedLog.txt)  



Encodings
---------

 * Supported: Shift_JIS(CP932), ISO-2022-JP(-1), EUC-JP, UTF8, UNICODE(UCS2).  
 
 * Supported Windows Dependent Characters <-> JIS Conversion.  
[(problem details)](http://support.microsoft.com/default.aspx?scid=kb;ja;JP170559)  

 * "JIS X 0208", "JIS X 0212" and "CP932" have the Unicode Mapping Table Differences,
  so the specific characters ( ～￠￡∥ etc... ) cannot be round-trip converted by default.  
 This module corrects this difference as much as possible when converting.  
[(problem details)](http://www8.plala.or.jp/tkubota1/unicode-symbols-map2.html)  



Development 
-----------

 * Clone Repository  
```
git clone https://github.com/narirou/jconv.git  
cd jconv  
npm install
```

 * Generate Tables  
```
# generates the unicode mapping table module in "tables" folder.
node generators/generate-source  
node generators/generate
```

 * Minify
```
npm run minify
```

 * Test
```
npm run test
```

 * Speed Test  
```
node test/speed  
# This results are visualized by chart.js.  
# Plese open "chart/index.html".
```



Based on
--------

 * [iconv-lite](https://github.com/ashtuchkin/iconv-lite) by ashtuchkin.
 * [Encoding.js](https://github.com/polygonplanet/Unzipper.js) by polygonplanet.
 * [iconv-js](https://github.com/Hikaru02/iconv-js) by Hikaru02.
 * [node-iconv](https://github.com/bnoordhuis/node-iconv) by bnoordhuis.
 * [libiconv-1.9.1-ja-patch Description](http://www2d.biglobe.ne.jp/~msyk/software/libiconv-1.9.1-patch.html) by 森山 将之.

Thank you so much!



Note
----

Pull requests are welcome.



Todo
----

 * Streaming API support
 * Support more encodings and languages.
 * Cleanup the code and more speed.
