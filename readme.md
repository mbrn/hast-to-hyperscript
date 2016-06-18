# hast-to-hyperscript [![Build Status][travis-badge]][travis] [![Coverage Status][codecov-badge]][codecov]

<!--lint disable heading-increment list-item-spacing no-duplicate-headings-->

Transform [HAST][] to something else through a [hyperscript][] DSL.

## Installation

[npm][]:

```bash
npm install hast-to-hyperscript
```

**hast-to-hyperscript** is also available as an AMD, CommonJS, and globals
module, [uncompressed and compressed][releases].

## Usage

Dependencies:

```javascript
var toH = require('hast-to-hyperscript');
var h = require('hyperscript');
```

AST:

```javascript
var tree = { type: 'element',
   tagName: 'p',
   properties: { id: 'alpha', className: [ 'bravo' ] },
   children:
    [ { type: 'text',
        value: 'charlie ' },
      { type: 'element',
        tagName: 'strong',
        properties: { style: 'color: red;' },
        children:
         [ { type: 'text',
             value: 'delta' } ] },
      { type: 'text',
        value: ' echo.' } ] }
```

Transform (`hyperscript` needs `outerHTML` to stringify):

```javascript
var doc = toH(h, tree).outerHTML;
```

Yields:

```html
<p class="bravo" id="alpha">charlie <strong>delta</strong> echo.</p>
```

## API

### `toH(h, node[, prefix])`

Transform [HAST][] to something else through a [hyperscript][] DSL.

###### Parameters

*   `h` ([`Function`][h]);
*   `node` ([`Element`][element]);
*   `prefix` (`string` or `boolean`, optional)
    — Prefix to use as a prefix for keys passed in `attrs` to `h()`,
    this behaviour is turned off by passing `false`, turned on by passing
    a `string`.  By default, `h-` is used as a prefix if the given `h`
    is detected as being `virtual-dom/h` or `React.createElement`.

###### Returns

`*` — Anything returned by invoking `h()`.

### `function h(name, attrs, children)`

Transform [HAST][] to something else through a hyperscript DSL.

###### Parameters

*   `name` (`string`) — Tag-name of element to create.
*   `attrs` (`Object.<string>`) — Attributes to set.
*   `children` (`Array.<* | string>`) — List of children and text,
    where children are the result of invoking `h()` previously.

###### Returns

`*` — Anything.

###### Caveats

Although there are lots of libs mentioning support for this interface,
there are significant differences between them.  For example, hyperscript
doesn’t support classes in `attrs`, `virtual-dom/h` needs an `attributes`
object inside `attrs` most of the time.  `hast-to-hyperscript` works
around these differences for:

*   [`React.createElement`][react];
*   [`virtual-dom/h`][vdom];
*   [`hyperscript`][hyperscript].

## Related

*   [`hastscript`][hastscript].

## License

[MIT][license] © [Titus Wormer][author]

<!-- Definitions -->

[travis-badge]: https://img.shields.io/travis/wooorm/hast-to-hyperscript.svg

[travis]: https://travis-ci.org/wooorm/hast-to-hyperscript

[codecov-badge]: https://img.shields.io/codecov/c/github/wooorm/hast-to-hyperscript.svg

[codecov]: https://codecov.io/github/wooorm/hast-to-hyperscript

[npm]: https://docs.npmjs.com/cli/install

[releases]: https://github.com/wooorm/hast-to-hyperscript/releases

[license]: LICENSE

[author]: http://wooorm.com

[hast]: https://github.com/wooorm/hast

[element]: https://github.com/wooorm/hast#element

[vdom]: https://github.com/Matt-Esch/virtual-dom/tree/master/virtual-hyperscript

[hyperscript]: https://github.com/dominictarr/hyperscript

[h]: #function-hname-attrs-children

[react]: https://facebook.github.io/react/docs/glossary.html#react-elements

[hastscript]: https://github.com/wooorm/hastscript
