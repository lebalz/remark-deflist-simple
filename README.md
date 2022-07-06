# remark-deflist

Built for docusaurus v2 s.t. it can be required (docusaurus is not yet ESM ready...).

## Syntax

```md
Definition 1
: Explanation 1a
: Explanation 1b

Definition 2
: Explanation 2
```

## AST (see [mdast](https://github.com/syntax-tree/mdast/blob/master/readme.md) specification)

For example, the following markdown:

```
Definition 1
: Explanation 1a
```

Yields:

```js
{
    type: 'dl',
    data: {
        hName: 'dl'
    },
    children: [
        {
            type: 'dt',
            data: {
                hName: 'dt'
            },
            children: [{
                type: 'text',
                value: 'Definition 1'
            }]
        },
        {
            type: 'dd',
            data: {
                hName: 'dd'
            },
            children: [{
                type: 'text',
                value: 'Explanation 1a'
            }]
        }
    ]
}
```

## Rehype

This plugin is compatible with [rehype][https://github.com/rehypejs/rehype]. `deflist` mdast nodes will become

```html
<dl>
    <dt>Definition</dt>
    <dd>Explanation</dd>
    <dd>...</dd>
</dl>
```

## Installation

```bash
yarn add remark-deflist-simple
```

## Usage

Dependencies:

```javascript
const unified = require('unified')
const remarkParse = require('remark-parse')
const stringify = require('rehype-stringify')
const remark2rehype = require('remark-rehype')

const remarkDeflist = require('remark-deflist-simple')
```

Usage:

```javascript
unified()
  .use(remarkParse)
  .use(remarkDeflist)
  .use(remark2rehype)
  .use(stringify)
```
