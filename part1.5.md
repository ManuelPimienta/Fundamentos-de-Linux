## Creación de vínculos y eliminación de archivos
### Enlaces duros

Hemos mencionado el término "enlace" cuando nos referimos a la relación entre las entradas de directorio (los "nombres" que escribimos) y los inodos (los números de índice en el sistema de archivos subyacente que normalmente podemos ignorar). En realidad hay dos tipos de enlaces disponibles en Linux. El tipo que hemos discutido hasta ahora se llama enlaces duros. Un inodo dado puede tener cualquier número de enlaces duros, y el inodo persistirá en el sistema de archivos hasta que todos los enlaces duros desaparezcan. Cuando el último vínculo duro desaparezca y ningún programa mantenga abierto el archivo, Linux eliminará el archivo automáticamente. Se pueden crear nuevos vínculos duros mediante el comando ln:

<code>$ cd /tmp</code>

<code>  $ touch firstlink</code>

<code>  $ ln firstlink secondlink</code>

<code>  $ ls -i firstlink secondlink</code>

<code>15782 firstlink    15782 secondlink</code>

Como puede ver, los enlaces duros funcionan en el nivel de inodo para apuntar a un archivo en particular. En sistemas Linux, los enlaces duros tienen varias limitaciones. Por un lado, sólo puede hacer enlaces duros a los archivos, no a los directorios. Está bien; aunque . y .. son enlaces duros a los directorios creados por el sistema, usted (incluso como el usuario "root") no están autorizados a crearlos por cuenta propia. La segunda limitación de los enlaces duros es que no pueden abarcar los sistemas de archivos; que sería el caso si los sistemas de archivos se encuentran en particiones de disco independientes. Esto significa que no puede crear un enlace desde /usr/bin/bash a /bin/bash si sus directorios / y /usr existen en particiones de disco separadas.

### Enlaces simbólicos

En la práctica, los enlaces simbólicos (o symlinks) se utilizan con más frecuencia que los enlaces duros. Los enlaces simbólicos son un tipo de archivo especial donde el vínculo se refiere a otro archivo por nombre, en lugar de directamente al inodo. Los enlaces simbólicos no impiden que se elimine un archivo; Si el archivo de destino desaparece, entonces el enlace simbólico sólo será inutilizable o roto.

Se puede crear un enlace simbólico pasando la opción -s a ln.

$ ln -s secondlink thirdlink
$ ls -l firstlink secondlink thirdlink
-rw-rw-r--    2 agriffis agriffis        0 Dec 31 19:08 firstlink
-rw-rw-r--    2 agriffis agriffis        0 Dec 31 19:08 secondlink
lrwxrwxrwx    1 agriffis agriffis       10 Dec 31 19:39 thirdlink -> secondlink

Los enlaces simbólicos se pueden distinguir en ls -l salida de archivos normales de tres maneras. En primer lugar, observe que la primera columna contiene un carácter l para indicar el enlace simbólico. En segundo lugar, el tamaño del enlace simbólico es el número de caracteres en el destino (segundo enlace, en este caso). En tercer lugar, la última columna de la salida muestra el nombre de archivo de destino precedido por una flecha ->.

### Symlinks en profundidad

Los enlaces simbólicos son generalmente más flexibles que los enlaces duros. Puede crear un vínculo simbólico con cualquier tipo de objeto del sistema de archivos, incluidos los directorios. Y debido a que la implementación de enlaces simbólicos se basa en rutas (no en inodos), está perfectamente bien crear un enlace simbólico que apunte a un objeto en otro sistema de archivos físico; es decir, una partición de disco diferente. Sin embargo, este hecho también puede hacer que los enlaces simbólicos sean difíciles de entender.

Considere una situación donde queremos crear un enlace en /tmp que apunte a /usr/local/bin. Deberíamos escribir esto:

$ ln -s /usr/local/bin bin1
$ ls -l bin1
lrwxrwxrwx    1 root     root           14 Jan  1 15:42 bin1 -> /usr/local/bin

O alternativamente:

$ ln -s ../usr/local/bin bin2
$ ls -l bin2
lrwxrwxrwx    1 root     root           16 Jan  1 15:43 bin2 -> ../usr/local/bin

Como puede ver, ambos enlaces simbólicos apuntan al mismo directorio. Sin embargo, si nuestro segundo enlace simbólico es movido a otro directorio, se "romperá" debido a la ruta relativa:

$ ls -l bin2
lrwxrwxrwx    1 root     root           16 Jan  1 15:43 bin2 -> ../usr/local/bin
$ mkdir mynewdir
$ mv bin2 mynewdir
$ cd mynewdir
$ cd bin2
bash: cd: bin2: No such file or directory

Debido a que el directorio /tmp/usr/local/bin no existe, ya no podemos cambiar los directorios en bin2; en otras palabras, bin2 está ahora roto.

Por esta razón, a veces es una buena idea evitar crear enlaces simbólicos con la información de ruta relativa. Sin embargo, hay muchos casos donde los enlaces simbólicos relativos son muy útiles. Considere un ejemplo en el que desea crear un nombre alternativo para un programa en /usr/bin:

<code> # ls -l /usr/bin/keychain </code>
-rwxr-xr-x    1 root     root        10150 Dec 12 20:09 /usr/bin/keychain

Como usuario root, puede crear un nombre alternativo para "llavero", como "kc". En este ejemplo, tenemos acceso de root, como lo demuestra nuestro indicador bash cambiando a "#". Necesitamos acceso root porque los usuarios normales no pueden crear archivos en /usr/bin. Como root, podríamos crear un nombre alternativo para keychain de la siguiente manera:

# cd /usr/bin
# ln -s /usr/bin/keychain kc
# ls -l keychain
-rwxr-xr-x    1 root     root        10150 Dec 12 20:09 /usr/bin/keychain
# ls -l kc       
lrwxrwxrwx    1 root     root           17 Mar 27 17:44 kc -> /usr/bin/keychain

En este ejemplo, creamos un enlace simbólico llamado kc que apunta al archivo /usr/bin/keychain.

Si bien esta solución funcionará, creará problemas si decidimos que queremos mover ambos archivos, /usr/bin/keychain y /usr/bin/kc a /usr/local/bin:

# mv /usr/bin/keychain /usr/bin/kc /usr/local/bin
# ls -l /usr/local/bin/keychain
-rwxr-xr-x    1 root     root        10150 Dec 12 20:09 /usr/local/bin/keychain
# ls -l /usr/local/bin/kc
lrwxrwxrwx    1 root     root           17 Mar 27 17:44 kc -> /usr/bin/keychain

Debido a que usamos un camino absoluto en nuestro enlace simbólico, nuestro enlace simbólico kc sigue apuntando a /usr/bin/ keychain, que ya no existe desde que movimos /usr/bin/keychain a /usr/local/bin.

Eso significa que kc es ahora un enlace simbólico roto. Tanto las rutas relativas como las absolutas en los enlaces simbólicos tienen sus méritos, y debe usar un tipo de ruta que sea apropiado para su aplicación particular. A menudo, un camino relativo o absoluto funcionará bien. El ejemplo siguiente habría funcionado incluso después de mover ambos archivos:

# cd /usr/bin
# ln -s keychain kc
# ls -l kc
lrwxrwxrwx    1 root     root            8 Jan  5 12:40 kc -> keychain
# mv keychain kc /usr/local/bin
# ls -l /usr/local/bin/keychain
-rwxr-xr-x    1 root     root        10150 Dec 12 20:09 /usr/local/bin/keychain
# ls -l /usr/local/bin/kc
lrwxrwxrwx    1 root     root           17 Mar 27 17:44 kc -> keychain

Ahora, podemos ejecutar el programa keychain escribiendo /usr/local/bin/kc. /usr/local/bin/kc apunta al llavero del programa en el mismo directorio que kc.












