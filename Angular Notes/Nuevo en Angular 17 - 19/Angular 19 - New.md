
---
- [[Defer]]
- [[Interceptor]]
---

***Server Side Rendering***

**Hidratación** → Agarrar el template y conecta los elementos interactuables al JavaScript. → Conecta el HTML con el JavaScript

- **Hidratación incremental** → Con `@defer`. → No se carga el JavaScript hasta que se *necesite*. 

> Yo le digo cuando hidratarse *(Lazy Loading)*. ↑

A veces, el JavaScript no llega a tiempo, por lo que se pueden perder las interacciones del usuario.

- **Event Replay** → Es un buffer donde se guardan esas interacciones, para que cuando ya se hidrate no se pierdan.

***Zoneless***

La idea detrás de zoneless es prescindir del archivo **zone.js** → El archivo encargado de la detección de de cambios. 

***Hot Module Replacement (HMR) instantáneo***

**Application Running** *(ng serve)* → No se carga toda la aplicación si hay cambios. → Solo se carga el pedacito que cambió. 

→ Funciona tanto para estilos como para plantillas.

`NG_HMR_TEMPLATES=1 ng serve`


> ***Standalone Components are default and doesn't need to be specified in decorator object***


***Mayor Seguridad***

- `angular.json` → **build >** `"options": {` `"autoCsp": false` `}`

Para prevenir inyecciones de código en nuestra aplicación.


> **Convertir todo a signals** → `ng generate @angular/core:signals`


***Variables en la plantilla***

> `@let greeting = "Hola " + greeting`
> 
> `<p> {{ greeting}} </p>`
