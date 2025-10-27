Permite ***cargar contenido de forma diferida*** según una condición → Mejora el rendimiento. ***Aplica LazyLoading*** ya que retrasa la carga de partes NO críticas.

Sintaxis ↓
`@defer (when isImageLoaded) {`
    `<img src="image.png" alt="My Image" />`
`}`
`@if (!isImageLoaded) {`
    `<p>Loading...</p>`
    `{{ loadImage() }}`
`}`

El método `loadImage()` solo tiene un **timeout**, que lo que hace es cambiar `isImageLoaded` de `false` a `true` después de 5 segundos.

También podemos agregar un **placeholder** mientras carga el contenido. ↓

`@defer (when isImageLoaded) {`
    `<img src="image.png" alt="My Image" />`
`}` `@placeholder {`
	`<div> Loading content...</ div>`
`}`

`@loading` != `@placeholder` → Loading se usa para controlar la carga una vez que la condición del `@defer` ya se cumple, es decir, si lo que se quiere cargar ya está pero es muy grande y esta tomando tiempo. 

**PLACEHOLDER** → Se muestra si la condición NO se cumple

`@loading` acepta dos parámetros ↓
- **after** → Cuánto tiempo se debe esperar antes de mostrar el contenido?
- **minimum** → Lo mínimo que debe verse el contenido del `@loading`.

Ejemplo de loading ↓
`@defer (when isImageLoaded) {`
    `<img src="image.png" alt="My Image" />`
`}` `@loading (after 2000ms; minimum 4000ms) {`
	`<div> Loading content...</ div>`
`}` `@placeholder {`
	`<div> No content yet. </ div>`
`}`

--- 
### Error

Para manejar errores.→ `@error`

`@defer (when isImageLoaded) {`
    `<img src="image.png" alt="My Image" />`
`}` `@loading (after 2000ms; minimum 4000ms) {`
	`<div> Loading content...</ div>`
`}` `@error {`
`<p> Sorry, we couldn't  load the content. </ p>`
`}`

- Así el componente **maneja sus propios errores** ↑

---

Hay un montón de cosas que puedes hacer con `@defer`. Te recomiendo investigar más.

