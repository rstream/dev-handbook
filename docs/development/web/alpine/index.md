# Alpine development

[← back](../../../index.md)

## init

The `init` method (of the object referenced by `x-data`) is called automatically!

So if you also put it in `x-init` - it will run **TWICE!**  
This snippet:
```html
<div x-data="app" x-init="init"></div>
```
Will run `app.init()` two times:
* first time because it is referenced in `x-init`
* second time because of the method naming - `init` (!)