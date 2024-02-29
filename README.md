# @viegg/ed2k-link

> This is a fork of [https://github.com/lightrabbit/ed2k-link](https://github.com/lightrabbit/ed2k-link)

> The original code will throw an `0308010C:digital envelope routines::unsupported` error in nodejs v17+ while calling `crypto.createHash('md4')`, see [this](https://juejin.cn/post/7202639428132044858) for detail.

> This fork fixed it by using a wasm `md4` hash function which stole from [webpack](https://github.com/webpack/webpack/blob/main/lib/util/hash/md4.js)

> The wasm version is almost as fast as nodejs's original `crypto` module, took 3 seconds to calculate a 2GB file's ed2k link in my MBP-2018.

---

A simple module to parse/generate ed2k link for nodejs.   

## Installation
You can use this command to install:

    npm install @viegg/ed2k-link

## Usage
You should require the module first:
```JavaScript
ed2k = require('@viegg/ed2k-link');
```

## Example

#### Parse a ed2k url

Code:
```JavaScript
ed2k.parse("ed2k://|file|foo.bar|123|0123456789ABCDEF0123456789ABCDEF|/");
```
Output:
```Javascript
{ filename: 'foo.bar',
  ed2k: '0123456789ABCDEF0123456789ABCDEF',
  aich: '',
  hashset: [],
  sources: { client: [], url: [] },
  length: 123 }
```

#### Convert `Ed2kLink` to ed2k url string

Code:
```JavaScript
var link = ed2k.parse("ed2k://|file|foo.bar|123|0123456789ABCDEF0123456789ABCDEF|/");
link.toString();
```
Output:
```JavaScript
ed2k://|file|foo.bar|123|0123456789ABCDEF0123456789ABCDEF|/
```

#### Generate `Ed2kLink` from file:

Code:

```JavaScript
//node-like callback
ed2k.generate("./foo.bar", function(err, link) {
  console.log(link);
});
//Promise
ed2k.generate("./foo.bar").then(function(link) {
  console.log(link);
});
```
Output:
```Javascript
{ filename: 'foo.bar',
  ed2k: '0123456789ABCDEF0123456789ABCDEF',
  aich: '',
  hashset: [],
  sources: { client: [], url: [] },
  length: 123 }
```


## License
The project is released under the [MIT license](http://www.opensource.org/licenses/MIT).

## Credit
Original author: lightpacerabbit@gmail.com
