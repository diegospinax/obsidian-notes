---

---

---

**Para crear tus propias directivas** → [[Como crear directivas personalizadas]]

---

Son aquellas que brindan funcionalidad extra a algo que antes no la tenía.

Las directivas se utilizan en elementos del DOM.

- Elementos del DOM → **div, p, h1, section, etc.**

Tenemos dos tipos de directivas
- **Estructurales** → Es aquella que modifica la estructura del elemento en el cual se aplica.
- **Atributos** → Modifican los atributos de un elemento.

**Estructurales**
- `*ngIf` → Depende de una condición si el elemento del DOM se renderiza o no.
- `*ngFor` → Itera una lista para renderizar un elemento del DOM múltiples veces.
**Atributos**
- `[ngClass]` → Depende de una condición si el elemento del DOM tiene una clase o no.
- `[ngStyle]` → Recibe un objeto con estilos CSS para asignar en el elemento.

---
### Nueva sintaxis

Recuerdas que para usar una directiva `if `debías hacer esto? → `*ngIf`

Pues ya no lo necesitas, la nueva sintaxis de Angular nos permite hacer todo de manera más sencilla con el **@**.

Más o menos, sería así:

Antes ↓
`<div *ngIf="isActivated"> Se muestra si true </ div>`

`<div *ngIf="!isActivated"> Se muestra si false </ div>`

Ahora ↓
`@if (isActivated) {`
	`<div> Se muestra si true</ div>`
`} @else {`
	`<div> Se muestra si false</ div>`
`}`

**En mi opinión, MUCHO mejor.**

**Ahora**, para el `for` sería parecido.

Antes ↓
`<ul>`
    `<li *ngFor="let item of items; let i = index">`
        `{{ item }}
    `</li>`
`</ul>`

Ahora ↓
`<ul>`
    `@for (item of items; track $index) {`
	    `<li>{{ item }}</li>`
    `} @empty {`
	    `<li>No items</li>`
    `}`
`</ul>`

### Switch

Es exactamente un switch.

`@switch (value) {`
	`@case ("option 1"){`
		`<div> Opcion 1</ div>`
	`}`
	`@case ("option 2"){`
		`<div> Opcion 2</ div>`
	`}`
	`@default {`
		`<div> Default Case</ div>`
	`}`
`}`