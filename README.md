# markdown-toc [![NPM version](https://badge.fury.io/js/markdown-toc.svg)](http://badge.fury.io/js/markdown-toc)

> Generate a markdown TOC (table of contents) with Remarkable.

## Install with [npm](npmjs.org)

```bash
npm i markdown-toc --save
```

## Usage

```js
var toc = require('markdown-toc');

toc('# One\n\n# Two').content;
// Results in:
// - [One](#one)
// - [Two](#two)
```

To allow customization of the output, an object is returned with the following properties:

 - `content` **{String}**: The generated table of contents. Unless you want to customize rendering, this is all you need.
 - `highest` **{Number}**: The highest level heading found. This is used to adjust indentation. 
 - `tokens` **{Array}**: Headings tokens that can be used for custom rendering


### toc.json

Object for creating a custom TOC. 

```js
toc('# AAA\n## BBB\n### CCC\nfoo').json;

// results in
[ { content: 'AAA', lvl: 1 },
  { content: 'BBB', lvl: 2 },
  { content: 'CCC', lvl: 3 } ]
```


### toc.insert

Insert a table of contents immediately after an _opening_ `<!-- toc -->` code comment, or replace an existing TOC if both an _opening_ comment and a _closing_ comment (`<!-- tocstop -->`) are found. 

_(This strategy works well since code comments in markdown are hidden when viewed as HTML, like when viewing a README on GitHub README for example)._

**Example**

```markdown
<!-- toc -->
- old toc 1
- old toc 2
- old toc 3
<!-- tocstop -->

## abc
This is a b c.

## xyz
This is x y z.
```

Would result in something like:

```markdown
<!-- toc -->
- [abc](#abc)
- [xyz](#xyz)
<!-- tocstop -->

## abc
This is a b c.

## xyz
This is x y z.
```

### Utility functions

As a convenience to folks who wants to create a custom TOC, markdown-toc's internal utility methods are exposed:

```js
var toc = require('markdown-toc');
```
- `toc.bullets()`: render a bullet list from an array of tokens
- `toc.linkify()`: linking a heading `content` string
- `toc.slugify()`: slugify a heading `content` string 
- `toc.strip()`: strip words or characters from a heading `content` string 

**Example**

```js
var result = toc('# AAA\n## BBB\n### CCC\nfoo');
var str = '';

result.json.forEach(function(heading) {
  str += toc.linkify(heading.content);
});
```


## Options


### options.bullet

Type: `String|Array`

Default: `*`

The bullet to use for each item in the generated TOC. If passed as an array (`['*', '-', '+']`), the bullet point strings will be used based on the header depth.


### options.maxDepth

Type: `Number`

Default: `3`

Use headings whose depth is at most maxDepth.


### options.firsth1

Type: `Boolean`

Default: `true`

Exclude the first h1-level heading in a file. For example, this prevents the first heading in a README from showing up in the TOC.


## Running tests
Install dev dependencies.

```bash
npm i -d && npm test
```



## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/markdown-toc/issues)

## Author

**Jon Schlinkert**
 
+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert) 

## License
Copyright (c) 2014-2015 Jon Schlinkert  
Released under the  license

***

_This file was generated by [verb](https://github.com/assemble/verb) on February 20, 2015._