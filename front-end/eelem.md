# Eelem

**Elem** works similar to jQuery:

```
let e = elem('#selector');
let e = elem('.selector');
```

Then we can use this object for multiple utilities:

```
let e = elem('.selector');

e.element

e.attr('src', value);
let attrs = e.getAttributes();
if (e.hasAttr('src'))

e.style({
    'background-color': 'black',
    'color': 'white'
});

<input type="file" id="filepicker">
let e = elem('#filepicker');
let file = e.getFile();
let files = e.getFiles();

e.tag;  // 'input'

e.offset.top
e.width
e.height
e.scroll.height
e.scroll.top
```

### Scroll animations

The elem object also has methods to control scrolling:

```
e.scrollHere(); // Scroll page to this element
e.scrollHere(false); // Without animation

// If the element has scroll itself:
e.scrollToTop(animated?);
e.scrollToBottom(animated?);
e.scrollTo(Y, animated?);
e.scrollToChild('#selector', animated?);
```
