### Hilo (Thread)

Un hilo es un contexto de ejecución.

Tienen su propio estado, prioridades, grupos y nombres.

---
### Cómo crear un Thread en Java?

1. Implementar la interfaz Runnable en una clase y definir el comportamiento del método `run()`.

```Java
public class ThreadOne implements Runnable {
    
    @Override
    public void run() {
        IO.println("Greetings from Thread One!");
    }
} 
```

> `IO.println()` -> Está disponible desde Java 25+. En versiones previas usa el clásico `System.out.println()`  

2. Instanciar la clase Thread y cómo pasarle cómo parámetro nuestra implementación de Runnable (ThreadOne).

3. Finalmente iniciamos la ejecución con `.start();`

```Java
public class Main {
    static void main() {
        Thread one = new Thread(new ThreadTwo()); //Paso 2

        one.start(); //Paso 3
    }
} 
```

-> Hay otras maneras, cómo pasar por parámetro una Lambda (función flecha) o simplemente extender una clase de Thread (No recomendado)

> Los Threads tienen métodos útiles que proporcionan información sobre su ejecución, estado, etc. -> **Recomiendo investigarlo**.

---
### Cómo dormir un Thread?

- **De qué sirve?** -> Para simular eventos que toman tiempo.

- **Que ocurre?** -> El Thread pausa la ejecución, queda en estado de reposo, cómo si estuviera =="dormido"==.

Podemos dormir un Thread usando el método `.sleep(time)` de la clase Thread. Recibe por parámetro el tiempo que dormirá el Thread.

> Investiga que tipos recibe `.sleep()` por parámetro.

---
### Cómo interrumpir un Thread?

- **De qué sirve?** -> Detener un Thread para limpiar recursos o cancelar su ejecución.

- **Que ocurre?** -> El Thread cambia su estado a interrupted.

Podemos interrumpir un Thread usando el método `.interrupt()` de la clase Thread. `.interrupt()` -> Cambia el estado a interrupted.

Consultar si un Thread está interrupted con -> `.isInterrupted()`

Limpiar el estado de interrupción de un Thread con -> `.interrupted()`

### Cómo puedo coordinar Threads en Java?

- **De qué sirve?** -> Sirve para coordinar Threads.

- **Qué ocurre?** -> El Thread actual espera a que el Thread objetivo termine su ejecución.

Podemos coordinar Threads con el Thread actual mediante el método `.join()` de la clase Thread. `.join()` -> Espera a un hilo por un tiempo definido o indeterminado. 

> Investiga qué tipos recibe `.join()` por parámetro.

### Thread Pools

**Pool** -> Agrupación de algo.

- **De qué sirve?** -> Para controlar el uso de Threads de manera segura dentro de límites predefinidos (==Evitan que algún desquiciado empiece a crear un hilo por tarea== ocasionando que la maquina se quede sin recursos).

- **Qué ocurre?** -> Se crea un Pool con un numero definido de Threads de los cuales podemos controlar su ciclo de vida y reutilizar para distintas tareas en una cola (queue).

Una analogía perfecta es cuando vamos a pagar en un supermercado, si vemos una caja que está vacía vamos hacia ella, sino, hacemos fila hasta llegar a la caja.

Pero el número de cajas es limitado, no se crea una caja (Thread) por cada persona, de ser así sería colapsaría el supermercado.

*Para crear un Thread Pool lo hacemos de la siguiente manera*

```JAVA
    ExecutorService executorService = Executors.newFixedThreadPool(16);
```

> Hay más opciones para crear un Thread Pool para distintos casos de uso. 

