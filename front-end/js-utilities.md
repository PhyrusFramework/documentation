# JS Utilities

```
URL.current();
URL.host();
URL.hostname();
URL.parameters();
URL.parameter( name, default? );

// /page --> /page?offset=3
URL.setParameters( {offset: 3} );

// /page/?offset=3&limit2 --> /page/?offset=7&limit=2&search=abc
URL.addParameters( {offset: 7, search: 'abc'} );

// Change browser URL path
//  /page --> /contact
URL.set( '/contact' );
URL.set( '/contact', 'Contact page');
```

```
// Force object to have default values:
let obj = { filename: 'abc' }

obj = force( obj, {
    filename: '',
    format: 'jpg'
} );
// Result:  {filename: 'abc', format: 'jpg'}
```

```
// Iterate object:
let obj = { a: 12, b: 16, c: 19 }
iterate(obj, (key, value) => { });
```

```
// Empty PHP equivalent:
if (empty( variable ))  // variable = false, '', 0, null, undefined
if (empty( array ))  // length = 0
```

```
// Hex -> RGB
let rgb = HexToRGB( '#4e4e4e' );  //  {r: 78, g: 78, b: 78}

// RGB -> Hex
let hex = RGBToHex( 78, 78, 78 );  // #4e4e4e
```

```
let text = "There are {{ count }} products in the category: {{ category }}";

text = replacer( text, '{{', '}}', (content) => {

    let key= content.trim();  // Remove white spaces around

    if (key == 'count') return 34;
    if (key == 'category') return 'sport';

});

// Result: There are 34 products in the category sport.
```

```
let text = "This is the title";
let id = sanitize(text); // "this-is-the-title"
```
