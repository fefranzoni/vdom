# vdom

🌲 Virtual DOM Tree to render and apply changes between two state changes into the real DOM.

## Motivation

The need to update only the actual changes between two states of an element within the real DOM. Something like reactive frameworks, such as React.js.

Some libraries offer the same or similar service, but do not always have a small file size to distribute your code. With this in mind, a small code <b>(4KB)</b> has been developed capable of performing the necessary work.

## Public API

#### create(vtree)
Receives an virtual tree and returns the real DOM Element for that tree.

##### Example
```javascript
var tree = vdom.h(...);
var el = vdom.create(tree);
document.body.appendChild(el);
```

#### vtree(type, props, children)
Creates Virtual DOM Tree.

```javascript
@param {String} type
// If "text" is used, then will create an "Virtual Text Node" instead of normal Node.
// If only this argument is passed to the function and it type is equals to string, then
// it will automatically return an Virtual Text Node with this value as text.

@param {Object} props
// A list of properties that will be seted inside the element attributes.

@param {Array} children
// Array of elements that will be nested inside the element.
```

##### Example
```javascript
var tree = vdom.h('ul', null, [
  vdom.h('li', { data: 'B' }, [ vdom.h('B') ])
]);

console.log(tree);
```


#### vnode(type, props, children)
Returns the Virtual Node for the given parameters.

```javascript
@param {String} type
The type of tagname of the element.

@param {Object} props
Object of attributes/propreties that will be set as the element attributes.

@param {Array} children
Array of sub-elements that will be contained inside the element.
```

##### Example

```javascript
var vnode = vdom.vnode('div', { someData: 1 }, [
  vdom.vnode('div')
]);
```

#### vtext(text)
Returns the Virtual Text Node for the given text.

##### Example
```javascript
var text = vdom.vtext('Some text here.');
```

#### render(root, newTree, oldTree)
Renders the created html for the given virtual tree(s).

This function must receive an rendered element in the real DOM, where it will be mounted after the trees mount.

When two trees are passed as argument, the function will calculate the differences between the two trees and <b>will only re-render the differences in the Real DOM.</b>

---

<b>The root element for the render function must be an different element from the body element of the page.</b>

---

##### Example

```javascript
var root = document.querySelector('#root');

var treeA = vdom.h('ul', null, [
  vdom.h('li', { data: 'A' }, [ vdom.h('A') ])
]);

vdom.render(root, treeA);

var treeB = vdom.h('ul', null, [
  vdom.h('li', { data: 'B' }, [ vdom.h('B') ])
]);

vdom.render(root, treeB, treeA);
```

#### parse2Tree(html)
Parses an html element or html string representation to a new Virtual DOM Tree.

##### Example

```javascript
var html = document.querySelector('.container') || '<ul>\
  <li>A</li>\
  <li>B</li>\
</ul>';

var tree = vdom.parse2Tree(html);
```

#### h(type, props, children)
Use hyperscript style to create Virtual DOM Trees.

Calls the "vtree" method.