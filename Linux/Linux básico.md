Cuando inicias Linux, por lo general estarás en el directorio home de tu usuario.

Lo compruebas si ves este símbolo al final de la ruta en la terminal ``~``

##### Comando: ``clear``

Este comando limpia la pantalla

##### Comando: ``pwd``

Te dice donde estás posicionado, es decir, toda la ruta de directorios hasta tu posición actual.

##### Comando: ``ls``

Te muestra los archivos y directorios en tu posición actual.

**Nota:** Una flag es esto → ``-texto`` Son como funciones "adicionales" al comando que se usará.

Adicional, puedes añadir las siguientes flags para hacer acciones adicionales:
- ``-l`` → Información sobre permisos.
- ``-a`` → Muestra todos los archivos y directorios, incluso los ocultos.

##### Comando: ``echo``

Muestra información en pantalla, imagínatelo cómo un ``print("texto")`` de Python

Adicional, podemos usar este comando para crear y escribir algo en un archivo:
- ``echo "Hola, soy Diego" > saludo.txt`` → creamos el archivo y asignamos el contenido con ``>``
- ``echo "Tengo 21 años" >> saludo.txt`` → añadimos contenido, manteniendo el contenido anterior con ``>>``

**Nota:** Si solo usas ``>`` y tenías algo en el archivo, se sobrescribirá perdiendo el contenido anterior

##### Comando: ``cat``

Muestra el contenido del archivo en la terminal.

##### Comando: ``man [otro_comando]``

Este comando nos brinda información sobre el ``[otro_comando]``:

**Ejemplo:** ``man cat`` → Eso no solo nos dice que hace cat, sino también nos indica las flags que podemos utilizar con él. Alguno incluso con ejemplo de uso. 


#### Redireccionamiento y directorios

##### Comando: ``cd [carpeta]``

El comando ``cd`` nos permite navegar entre directorios -  carpetas. 

Es importante recordar que este accede a directorios que estén dentro del directorio actual

Por ejemplo, estoy en ``Documentos`` → Dentro tiene la carpeta ``Diego``

Solo puedo acceder a esta carpeta, porque es la única dentro del directorio en la que estoy posicionado → ``cd Diego``

**Importante**
Puedes navegar hasta ``home``, usando este símbolo ``~`` → Este representa la carpeta ``home`` que es universal.

Es decir, no importa donde estés parado, si haces → ``cd ~`` Te va a llevar a ``home``, que es la carpeta raíz del usuario.

- Aprovecha esto para entrar a directorios del home → ``cd ~/Imagenes``

Adicionalmente, puedes hacer referencia a la carpeta actual o a la carpeta padre:
- ``.`` → Indica la carpeta actual.
-  ``..`` → Indica la carpeta padre.

Entonces si yo hago → ``cd ..`` me voy a la carpeta padre de donde estoy posicionado.
O también → ``cd ./Diego`` → para indicar que quiero entrar a esta carpeta que está dentro del directorio actual

También puedes usar estas referencias para ver los archivos con ``ls`` → ``ls ..``  

##### Comando: ``mkdir [nombre]``

Con este comando creas un directorio.

Ejemplo: ``mkdir Imagenes`` 

#### Eliminando archivos y directorios

##### Comando: ``rmdir [nombre]``

Este comando elimina directorios. Pero solo directorios.

[[#^da485e|Cómo eliminar directorios y su contenido]]

##### Comando: ``rm [nombre]``

Este comando elimina archivos, necesitas pasarle también la extensión del archivo.

Ejemplo: ``rm my-photo.png``

Adicionalmente, podemos borrar directorios y todos los archivos dentro con:
- ``rm -R Imagenes`` → Este flag ``-R`` indica que se debe eliminar de manera recursiva el contenido. ^da485e

#### Comodines

Los comodines son útiles cuando queremos referirnos a un conjunto de archivos que siguen una estructura en común.
##### Comodín: ``*``

Indica todo, no importa que haya después mientras cumpla la estructura.

**Ejemplo**

Tengo 3 archivos: ``my-text-1.txt``, ``my-text-abc.txt`` y ``my-text-2.txt``

``ls -l my-text-*.txt`` → Va a devolver todo lo que coincida con la estructura fuera del comodín.

Tanto ``my-text-1.txt``, ``my-text-abc.txt`` y ``my-text-2.txt``→ Todos cumplen la estructura.

##### Comodín: ``?``

Indica que solo un character puede ser aleatorio y estrictamente solo uno, además se debe cumplir la estructura.

Ejemplo

Tengo 3 archivos: ``my-text-1.txt``, ``my-text-abc.txt`` y ``my-text-2.txt``

``ls -l my-text-?.txt`` → Va a devolver todo lo que coincida con la estructura completa.

Es decir, solo ``my-text-1.txt`` y ``my-text-2.txt``→ Cumplen la estructura.

Pero yo puedo acumular este comodín → ``ls -l my-text-???.txt``

Ahora solo devuelve ``my-text-abc.txt`` → Cumple con la estructura.

#### Manipulando archivos

##### Comando: ``cp [origen] [destino]``

Este comando nos permite copiar el contenido de un archivo a otro.

También podemos copiar el contenido de un directorio de manera recursiva a otro directorio

Ejemplo

``cp -R ./folder-one/ ./folder-two``

Esto copia el contenido del primer directorio en el segundo, gracias a la flag ``-R``

##### Comando: ``mv [origen] [destino]``

Con este comando podemos hacer dos cosas, mover un archivo a otro directorio, o renombrar archivos.

Esto depende de como lo usemos:

**Mover** → ``mv my_file.txt ./files``

**Renombrar** → ``mv my_file.txt my_document.txt``

Puedes mover y renombrar indicando el nuevo nombre al final de la ruta del directorio:

Ejemplo

``mv my_file.txt ./files/renamed_file.txt``

#### Comprimiendo y descomprimiendo ZIP

##### Comando: ``zip [nombre].zip [ruta]``

Este comando nos permite comprimir directorios o archivos. Primero indicamos el nombre que tendrá el archivo zip final, después la ruta del archivo o directorio.

Si lo que estás comprimiendo son directorios, debes usar la flag de recursividad ``-r`` para copiar también el contenido. → ``zip -r [nombre].zip [ruta]``

##### Comando: ``unzip [nombre].zip``

Este comando nos permite descomprimir archivos zip.

Podemos usar la flag de listar ``-l`` para ver el contenido, sin descomprimir. 
→ ``unzip -l work.zip`` → lista el contenido del zip.

#### Comprimiendo y descomprimiendo TAR

##### Comando: ``tar``

Este comando nos permite comprimir y descomprimir archivos ``.tar``

**Para comprimir** → ``tar -vczf directorio.tar.gz ./directorio``
Para descomprimir → ``tar -vxzf directorio.tar.gz``

**Flags:**
- ``-v`` → Para ver información de la operación.
- ``-c`` → Indica que queremos comprimir.
- ``-z`` → Indica que también queremos compresión ZIP
- ``-f`` → Nos permite no usar redirección ``>`` Sino solo tratar los archivos.


**Nota**

El comando ``tar`` no comprime, solo empaqueta archivos. Por eso podemos usarlo junto con otros compactadores para comprimir.

Podemos usar **gzip** → ``-z`` extensión → ``.tar.gz`` → Más rápido
O usar **bzip2** → ``-j`` extensión → ``.tar.bz2`` → Más eficiente, archivos más pequeños

#### Visualizando contenido de  archivos

##### Comando: ``head``, ``less`` y ``tail``

Estos comandos nos permiten visualizar una porción del archivo sin necesidad de mostrarlo todo por pantalla cómo haríamos con ``cat``.

- ``head`` → Muestra el principio del archivo
- ``tail`` → Muestra el final del archivo
- ``less`` → Nos permite navegar por el archivo

Adicionalmente, podemos especificar la cantidad de líneas que queremos visualizar con la flag
``-n [numero]``:

- ``head -n 4 file.txt`` → Nos muestra las primeras 4 líneas del archivo.

