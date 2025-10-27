Los Triggers son "funciones" SQL que nos ayudan a ejecutar una lógica después o antes de que ocurra un evento en la base de datos, por ejemplo, eventos como la inserción de datos, actualización de registros o la eliminación de registros.

#### Cómo crear un Trigger?

Para crear un Trigger, primero necesitamos declarar los delimitadores de nuestro trigger, lo que esté dentro será la definición del Trigger como tal:

`DELIMITER //` → Esto: ``//`` lo usaremos después al final de nuestro trigger.

`DELIMITER ;` → Nota que hay un espacio entre ``DELIMITER`` y el ``;`` → **MUY IMPORTANTE**

Dentro, ya podemos definir nuestro trigger:

`DELIMITER //`

`create trigger nombreDelTrigger`
	`after insert on nombreDeLaTabla`
	`for each row`
			`begin`
				_Aquí va la acción que queremos realizar cuando ocurra la acción mencionada arriba._
			`end //`

`DELIMITER ;`

#### Notas adicionales

En el ejemplo anterior usamos ``after,`` para decir después, pero también se puede usar ``before`` para indicar que el trigger debe dispararse antes del evento mencionado.

``for each row`` indica que para cada fila de la tabla afectada vamos a realizar la acción dentro del ``begin`` y  ``end`` 

Podemos acceder a los valores de la fila afectada vieja y nueva.

- **Vieja** → ``old``
- **Nueva** → ``new``

Esto nos sirve para manejar los datos viejos o nuevos para nuestra lógica del trigger.


