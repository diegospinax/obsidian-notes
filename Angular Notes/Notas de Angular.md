Angular es una plataforma ya que está conformado por un conjunto de frameworks.
## TABLA DE CONTENIDO

- [[#Reactive programming]]
- [[#Estructura del componente]]
- [[#Módulos]]
- [[#Standalone]]
- [[#Router Outlet]]
- [[#Ciclo de vida del componente]]
- [[#Data Binding]]
- [[Directivas]]
- [[#Comunicación Padre - Hijo]]
- [[#Comunicación Hijo - Padre]]
- [[#Signals]]
- [[#Computed States]]
- [[#Servicios]]
- [[#Referencias locales]]
- [[#Diferencia entre promise y observable]]

---

***Nuevas características de Angular 19*** → [[Angular 19 - New]]

---
### Reactive programming

-  **Canales** → Tubo que tiene agujeritos.
-  **Espectadores** → Van a mirar a través de esos agujeritos.
-  **Eventos** → Se pasa un objeto por el tubo.

***Cada componente reacciona a como ocurren los eventos.***

***Las Signals*** en Angular son este canal mediante el cual se pasa información de un evento.

-  **Observables** → Canal unidireccional.
-  **Subject** → Canal bidireccional.
-  **BehaviorSubject** → Canal bidireccional con cache (Almacena la ultima información enviada).

---
### Estructura del componente

Un **Componente** es la unidad lógica mínima de Angular. → Solo debe hacer **UNA** cosa. 

*Composición ↓* 
- **HTML** → El template del componente.
- **CSS** → Los estilos del componente.
- **TypeScript** → La lógica del componente.

Hay dos tipos de componentes: 
- ~~Dumb Component~~ → **Presentational:** Usado para mostrar datos y manejar la UI.
- ~~Smart Component~~ → **Container:** Maneja la lógica de negocios y también la comunicación con entidades externas.

A esto se le llama ***patrón contenedor - presentacional***

***El archivo TypeScript Exporta una clase ↓*** 

Angular recomienda utilizar el modificador de acceso `protected` para los atributos de la clase que se vayan a mostrar en el template. Si no, `private`.

**CommonModule**  → Exporta prácticamente todas las directivas y pipes que tiene Angular por defecto.

Si quieres importar módulos en tu componente [[#Standalone]] ↓

`imports: [CommonModule] `

---
### Módulos

Los módulos podemos entenderlos como cajas que contienen  las herramientas necesarias para una funcionalidad.

Estos se caracterizan por agrupar declarar y agrupar componentes, importar otros módulos e implementar proveedores de servicios.

Cómo elemento de Angular, es necesario que un módulo tenga el decorador `@NgModule()` encima del nombre de la clase. 

Antes no existía el concepto de **standalone**, por lo tanto todo debía ser declarado en algún módulo para que se pudieran utilizar. 

- ***Ya no usamos módulos*** → Los módulos hacían que la aplicación fuera mucho más compleja de lo que realmente debía ser.

---
### Standalone

A partir de angular 17 ya no es necesario vincular nuestros componentes a módulos. 

Para establecer un componente como **standalone**, debemos incluir la propiedad `standalone: true` dentro del objeto del decorador `@Component({})`. 

Gracias a esto también podemos importar otros componentes que necesitemos directamente en el componente, sin necesidad de un módulo.

`imports: [MyComponent, UserComponent]`

`providers: [LocalService]`

- **Módulos** → Complejidad innecesaria.
- **Standalone** → Importas solo lo necesario, donde es necesario.

---
### Router Outlet

Es el encargado del enrutamiento de nuestra aplicación. Este se utiliza como una etiqueta en la plantilla `<router-outlet/>` → y renderiza cada una de las rutas declaradas en el `app.routes`.

---
### Ciclo de vida del componente

- **Constructor** → Declarar variables. **(Asignar valores por defecto)** → NO código async.
	- **Ejecución:** Antes del render.
	
- **ngOnChanges** → Es para cambios y reaccionar a cambios.
	- **Ejecución:** Antes y durante el render.
	- **Recibimos los cambios** → `ngOnChanges(changes: SimpleChanges) {}`
	
- **ngOnInit** →  Qué se ejecuta después de inicializar un componente? → **No tiene reactividad.**
	- **Ejecución:** Después de renderizar el componente, solo se ejecuta una vez.
	
- **ngAfterViewInit**  → Ejecutar lógica una vez que los elementos hijos ya fueron renderizados.
	- **Ejecución:** Después del render.
	
- **ngOnDestroy** →  Se ejecuta una vez que el componente se destruye. 

---
### Data Binding

El data binding es la manera en la que conecto los datos de mi ***clase*** con la ***plantilla***.

- **Interpolación** → `{{ }}` → `<p> {{ title }} </p>`
- **Property Binding** → `[ ]` → `<img [src]='imgUrl' />`
- **Event Binding** → `( )` → `<button (click)='clickHandler()' > Click me! </ button>`


> **Detalles → Event Binding**
> Los eventos pueden recibir como parámetro el evento. Desde la plantilla sería pasando como parámetro lo siguiente → `(click)='clickHandler($event)'`. 
> 
> Desde la clase ↓
> `clickHandler(event: Event) {`
> 	`console.log(event)`
> `}`
> 
> Para manejar eventos de teclado → `KeyboardEvent`

---
### Comunicación Padre - Hijo 

Esta comunicación se hace por medio de `@input`.

Mediante signals ↓

- `title = input<string>('')`

En la plantilla del padre → `<app-hijo [title]="titleForChild"> Soy el hijo </app-hijo>`

### Comunicación Hijo - Padre

Esta comunicación se hace por medio de `@output`

Mediante signals ↓

**En el hijo ↓**

`message = output<string>()`

`messageEmitter(){`
	`this.message.emit('Hola');`
`}`

- En la plantilla → `<div (click)="messageEmitter()"> Click me to emit </div>`

**En el padre ↓**

`messageReceiver(event: string){`
	`console.log(event);`
`}`

- En la plantilla → `<app-hijo (messageEmitter)="messageReceiver($event)"> Soy el componente hijo </ app-hijo>`

**NOTAS** → El método del padre que recibe el evento debe recibir por parámetro el mismo tipo de dato que tiene el output en el hijo. ***En el caso anterior*** → `string`.

---
### Signals

Las Signals son una manera más precisa y por lo tanto rápida de reaccionar a cambios en el DOM.
Ya que los cambios se detectan mediante señales.

Antes de este modelo de reactividad estaba algo llamado **zone.js**.

- **zone.js** → Un elemento que leía eventos del DOM. → Cuando algo cambiaba este no sabía específicamente qué, entonces Angular cargaba todo desde 0.
- **Signals** → Reactividad granular, ya que ahora se sabe exactamente que fue lo que cambió. Entonces no es necesario hacer todo el recorrido del DOM.

**Variables con Signals**

Las variables creadas con Signals se manejan cómo si fueran funciones.

Normal → `const myName = "Diego";` → **invocación** → `console.log(myName);`
Signals → `const myName = signal("Diego");` → **invocación** → `console.log(myName());`

**Para qué nos sirve** → Mejora la reactividad → convertimos una variable en una señal que avisa al DOM cuando se realiza un cambio.

**Cómo realizar cambios en una Signal** → con el método `.set()` de las signals → `myName.set(newValue);` → Esto hace que en todos los lados que fuese llamado` myName()` se visualice este cambio. **ESTO RESETA TODA LA SEÑAL**

**Para actualizarla** (actualizar su contenido sin resetearlo) → `.update()`

---
### Computed States

Son estados que derivan de otros estados. Cómo una especie de ***reacción en cadena de signals***.

> ***Calcula un estado y genera una nueva señal a partir de ese estado.***

Sintaxis ↓

`const quantity = computed (() => {`
	`const mySignal = this.mySignal();`

	`return mySignal ? 'hola' : 'adios';`
`})`

---
### Effect

Vigila cada que un estado cambia, y nos permite ejecutar una lógica en base a ese cambio.

Sintaxis ↓
`constructor() {`
    `effect(() => {`
      `const tasks = this.tasks();`
      `localStorage.setItem('tasks', JSON.stringify(tasks));`
    `})`
  `}`
 
---
### Referencias locales

- **Con la almohadilla** → `#` → Sirve para identificar un elemento de la plantilla. → `<p #miParrafo> Este es un parrafo. </p>`

Para ***obtener esta referencia en el componente*** debemos usar el decorador `@ViewChild()`. Así → `@ViewChild('miParrafo') miParrafo!: ElementRef;`

---
### Servicios

- **Lógica de negocios.** 
- **Conectarse con entidades externas.**
- **Para compartir información.**

Un servicio existe para mantener el patrón singleton, haciendo que la aplicación pueda compartir una única instancia del servicio.

- Servicio → **Singleton** → ~~Ciclo de vida~~

Para declarar un servicio simplemente se debe utilizar el decorador `@Injectable({})` como parámetro recibe un objeto, que dentro, como propiedad debe tener `providedIn: 'root'`.

Tipo de valor que recibe `providedIn` para definir la instancia.
- `'root'` → En toda la aplicación.
- `'any'` → En el módulo más cercano de donde se solicita por primera vez.

---

### Diferencia entre promise y observable

**Promise** → Promete que algo va a suceder, aunque termine bien o mal. ***¿Cuántas veces se cumple una promesa?*** → Solo una vez.

**Observable** → Es un canal de comunicación, por lo que los elementos observan el contenido que pasa por ese canal. ***¿Cuántas veces se ejecuta una petición Http?*** → Solo una vez.

> Pero, el observable tiene un método llamado `.pipe()` que nos permite tratar la respuesta a la solicitud.

