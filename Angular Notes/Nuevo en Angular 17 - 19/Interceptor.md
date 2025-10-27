Intercepta algo y ejecuta una lógica sobre eso.

Comando para la creación ↓

> `ng g interceptor name`

Es recomendable guardar los interceptores en una carpeta de *"interceptors"*.

Para que los interceptores estén disponibles en nuestra aplicación debemos añadir el provider de ***httpClient*** a nuestro `app.config.ts` → Y dentro, establecer qué interceptores usaremos.

`providers: [provideHttpClient(withInterceptors([authIterceptor])]`

**Todas las peticiones** de nuestra aplicación van a pasar por acá.

> Por ejemplo, en un **interceptor de autenticación**, el interceptor nos ayudaría al manejo de tokens.

### Refresh token

Sirven para solicitar un nuevo token de autenticación basado en uno ya existente sin que el usuario tenga q volver a autenticarse.