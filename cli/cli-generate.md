# CLI Generate

The **generate** command automates the task of creating Controllers, Components, Middlewares and Classes:

```
php cli generate page /auth/login

// will generate /src/pages/auth/pages/login

~/login.controller.php
class LoginPageController extends Controller { ... }

~/login.view.php
~/login.vue
```

```
php cli generate component /web/menu
// src/components/web/menu

~/menu.controller.php
class MenuComponent extends ComponentController { ... }

~/menu.view.php
~/menu.vue --> VueController
-------------------------------------------------------

php cli generate vueComponent /widgets/calendar
// src/components/widgets/calendar

~calendar.controller.php
~calendar.vue --> VueComponent
```

```
php cli generate middleware api-authenticated
// src/middlewares/api-authenticated
~/api-authenticated.controller.php
class ApiAuthenticatedMiddleware extends Middleware { ... }
```

```
php cli generate class models/Product --extend=ORM
// src/code/models/product.php

class Product extends ORM { }
```

