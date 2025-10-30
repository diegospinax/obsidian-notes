### Concurrencia

La concurrencia es la capacidad de un sistema de ejecutar múltiples tareas de forma independiente. 

-> Haciendo una analogía con la vida real; Cuando lavamos ropa en una lavadora mientras que cocinamos algo en la estufa.

En este ejemplo se están haciendo dos tareas de manera independiente.

Para prender la lavadora no es necesario que se apague la estufa.

---
### I/O 

Significa **Input/Output** (Entrada/Salida) -> Son operaciones hacia el mundo exterior al lenguaje de programación. Por ejemplo cuando queremos crear un archivo en el sistema operativo desde Java, o cuando consultamos una base de datos.

### Por qué acabo de mencionar operaciones I/O?

En Java, estas operaciones I/O suelen bloquear el [[Threads|Thread]] (donde está corriendo nuestro programa) ocasionando que toda la ejecución se congele hasta que finalice el proceso.

Sin embargo, no se puede bloquear todo el sistema (que en este caso, corre en ese único [[Threads|Thread]]) para esperar los datos. Necesitamos crear un nuevo Thread y ejecutar esta operación bloqueante ahí, así mantenemos el sistema disponible.

---
### Corrupción de memoria

^5c325f

Ocurre cuando varios Threads manipulan el mismo recurso simultáneamente, haciendo así que se corrompa su estado.

Para evitar esto, necesitamos garantizar que el acceso al recurso se hace de manera segura, sin que los Threads se estén pisando los unos a los otros.

- ==Lock== -> Mecanismo de control de concurrencia. Nos garantiza que el acceso a un recurso compartido se haga de manera uniforme y segura. ==Tiene métodos para bloquear el acceso al recurso y para liberarlo.==

La palabra ``synchronized`` en la declaración de una función nos ayuda a controlar el acceso al recurso.

```JAVA
        public synchronized void accumulate() {
            this.value += 1;
        } 
```

O en bloque dentro de una función.
Esto hace que únicamente se controle el acceso de los Threads a este bloque. ^19104b

```JAVA
        public void accumulate() {        
            synchronized (this) {
	            this.value += 1;
            }
        } 
```

Así nos aseguramos de que dos Threads no acceden al mismo recurso en simultáneo.

---
### Deadlocks

Un deadlock se produce cuando todos los Threads de un programa se quedan congelados al esperar por recursos compartidos que nunca se liberan.

-> Por ejemplo, al usar `synchronized` y dentro tener un bucle infinito.

-> Dos Threads que necesitan usar dos recursos, sin embargo cada Thread tomó un recurso y perdió el control del otro, así que el sistema se bloquea.

![[concurrency-deadlock.png]]

---
### Executors

Una clase que sirve para crear Executors, los Executors nos ayudan a manejar Threads y concurrencia de manera más sencilla. Lee sobre cómo usarlos para crear Thread Pools [[Threads#Thread Pools|aquí]].

---
### Monitor

El monitor es una "propiedad" de todos los objetos (==instancia==) a la cual no se puede acceder. 

-> Su propósito es controlar el acceso al recurso por medio de un bloqueo. 

Su relación con `synchronized` es que este último le indica a el monitor del objeto que debe bloquear ese recurso para evitar [[#Corrupción de memoria|corrupción de memoria.]] 

> *Piénsalo así, cada que instancias un objeto, este nace con un "angel guardian" que lo protege sin que el se de cuenta.*

> [!INFO]
> Otra nota importante es que cuando utilizas `synchronized` en bloque ([[#^19104b|click aquí]] para ver el ejemplo) lo que estableces entre paréntesis `()`
es el objeto del cuál quieres proteger el acceso.

Sin embargo, se puede sabotear este comportamiento mediante los métodos:

- `.wait()` -> Duerme el Thread, el monitor libera el recurso. Se recomienda llamarlo en un `while(condición)` o si no se puede despertar sin querer *(cosas random de Java)*.

- `.notify()` -> Despierta un Thread.

- `.notifyAll()` -> Despierta todos los Threads afectados por `.wait()`.

> -> Todos los objetos tienen estos métodos.
> -> Solo pueden llamarse desde el objeto bloqueado.
> -> Solo pueden usarse dentro de un `synchronized` ya sea método o bloque.

### Volatile

Cuando hay datos que son accesibles desde múltiples hilos, puede haber veces donde el procesador aplica optimizaciones que pueden corromper la memoria.

-> Puede guardar en su cache información que ya cambiado. Y utilizarla para una operación, lo que ocasiona *corrupción de memoria*.

Para evitar que el procesador realice estas optimizaciones, podemos añadir en la declaración de la variable la palabra `volatile`.

```JAVA
public volatile String text = "Papaya";
```

