Los eventos en Spring nos sirven para reaccionar a acciones realizadas por otros componentes, para así ejecutar lógica después de que cierto evento a ocurrido.

Por ejemplo, cada que se cree una tarea, quiero que se cree una notificación. Esto lo puedo hacer emitiendo un evento en la tarea, y escuchando este evento en mis notificaciones para la creación.

Por lo mencionado arriba necesitamos por lo menos dos componentes pero siempre habrá:

- **Emitter**
- **Listeners**

Veamos primero la parte del emitter
#### Emitter

Para que se pueda emitir un evento, el componente que va a emitir debe inyectar un objeto de tipo ``ApplicationEventPublisher``.

Este se encargará de emitir el evento.

``eventPublisher.publishEvent(Object eventObject);``
#### Listeners

Cada listener debe tener un método con la anotación ``@EventListener``. Este método debe recibir por parámetro el mismo tipo de objeto que emite el Emitter.