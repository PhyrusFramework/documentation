# JS Utilities

### URL Utilities

```
URL.current();
URL.host();
URL.hostname();
URL.parameters();
URL.parameter( name, default? );

URL.setParameters( {offset: 3} );
/page --> /page?offset=3

URL.addParameters( {offset: 7, search: 'abc'} );
?offset=3&limit2 --> ?offset=7&limit=2&search=abc

// Change browser URL path without redirecting
//  /page --> /contact
URL.set( '/contact' );
URL.set( '/contact', 'Contact page');
```

### Object management

```
// Iterate object:
iterate(obj, (key, value) => {
    //...
});

// Force object to have default values:
let obj = { filename: 'abc' }

obj = force( obj, {
    filename: '',
    format: 'jpg'
} );
// Result:  {filename: 'abc', format: 'jpg'}
```

```
// PHP Empty equivalent:
if (empty( variable ))  // variable = false, '', 0, null, undefined
if (empty( array ))  // length = 0
```

### Colors

```
// Hex -> RGB
let rgb = HexToRGB( '#4e4e4e' );  //  {r: 78, g: 78, b: 78}

// RGB -> Hex
let hex = RGBToHex( 78, 78, 78 );  // #4e4e4e
```

### Strings

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
