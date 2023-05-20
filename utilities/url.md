# URL

```
URL::current();  
// https://mysite.com/user/profile?param=value

URL::host( $url? = current);   
// https://mysite.com

URL::hostname( $url? = current);  
// mysite.com

URL::parameters( $url? = current );  
// ['param' => 'value']

URL::protocol( $url? = current );  
// https://

if (URL::isHttps( $url? = current) )

URL::page( $url? = current );  
//  profile

URL::uri( $url? = current );  
//  user/profile?param=value

URL::route( $url? = current );  
//  user/profile

URL::path( $url? = current );  
//  [ 'user', 'profile' ]
```
