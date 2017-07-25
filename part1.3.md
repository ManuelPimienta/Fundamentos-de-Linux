## Paths(Rutas)

Para ver el directorio de trabajo actual de bash, puede escribir:

<code>$ pwd</code>

<code>$ 
/
</code>

En el ejemplo anterior, el argumento / a cd se llama ruta. Le dice a cd dónde queremos ir. En particular, el argumento / es una ruta absoluta, lo que significa que especifica una ubicación relativa a la raíz del árbol del sistema de archivos.

### Rutas absolutas

Aquí hay otras rutas absolutas:

<code>/dev</code>

<code>/usr</code>

<code>/usr/bin</code>

<code>/usr/local/bin</code>

Como puede ver, la única cosa que todos los rutas absolutas tienen en común es que comienzan con /. Con una ruta de acceso a 
/usr/local/bin, estamos diciendo a cd que entre en el directorio /, a continuación al directorio usr, luego local y bin. Las rutas absolutas se evalúan siempre comenzando en / primero.

### Rutas relativas

El otro tipo de ruta se llama una ruta relativa. Bash, cd y otros comandos siempre interpretan estas rutas en relación con el directorio actual. Las rutas relativas nunca comienzan con un /. Por lo tanto, si estamos en /usr:

<code>$ cd /usr</code>

Entonces, podemos usar una ruta relativa para cambiar al directorio /usr/local/bin:


<code>$ cd local/bin</code>

<code>$ pwd</code>

<code>/usr/local/bin</code>

### Utilizando ..

Las rutas relativas también pueden contener uno o más directorios. El directorio .. es un directorio especial que apunta al directorio padre. Así, continuando desde el ejemplo anterior:

<code>$ pwd</code>

<code>/usr/local/bin</code>

<code>$ cd ..</code>

<code>$ pwd</code>

<code>/usr/local</code>

Como puede ver, nuestro directorio actual es ahora /usr/local. Pudimos ir "al revés" un directorio, relativo al directorio actual en el que estábamos.

Además, también podemos añadir .. a una ruta relativa existente, lo que nos permite entrar en un directorio que está junto a uno en el  que ya estamos, por ejemplo:

<code>$ pwd</code>

<code>/usr/local</code>

<code>$ cd ../share</code>

<code>$ pwd</code>

<code>/usr/share</code>

### Ejemplos de ruta relativa

Las rutas relativas pueden ser bastante complejas. Aquí hay algunos ejemplos, todos sin el directorio de destino resultante mostrado. Trate de averiguar dónde terminará después de escribir estos comandos:

$ cd /bin
$ cd ../usr/share/zoneinfo


$ cd /usr/X11R6/bin
$ cd ../lib/X11


$ cd /usr/bin
$ cd ../bin/../bin

Ahora, probarlos y ver si los tienes bien :)

### Entendiendo el "."

Antes de terminar nuestra cobertura de cd, hay algunas cosas más que necesito mencionar. En primer lugar, hay otro directorio especial llamado., Que significa "el directorio actual". Aunque este directorio no se utiliza con el comando cd, a menudo se utiliza para ejecutar algún programa en el directorio actual, de la siguiente manera:

$ ./myprog

En el ejemplo anterior, se ejecutará el ejecutable myprog residente en el directorio de trabajo actual.

### cd y el directorio de inicio

Si queremos cambiar a nuestro directorio personal, podríamos escribir:

$ cd

Sin argumentos, cd cambiará a su directorio de inicio, que es /root para el superusuario y normalmente /home/nombre de usuario para un usuario normal. Pero ¿qué pasa si queremos especificar un archivo en nuestro directorio personal? Tal vez queramos pasar un argumento de archivo al comando myprog. Si el archivo reside en nuestro directorio personal, podemos escribir:

$ ./myprog /home/drobbins/myfile.txt

Sin embargo, usar un camino absoluto como ese no siempre es conveniente. Afortunadamente, podemos usar el carácter ~ (tilde) para hacer lo mismo:

$ ./myprog ~/myfile.txt

### Directorios de inicio de otros usuarios

Bash expandirá un solo ~ para apuntar a su directorio personal, pero también puede usarlo para apuntar a los directorios de inicio de otros usuarios. Por ejemplo, si queremos hacer referencia a un archivo llamado fredsfile.txt en el directorio personal de Fred, podríamos escribir:

$ ./myprog ~fred/fredsfile.txt

## Usando comandos de Linux

### Introduciendo ls

Ahora, echaremos un vistazo al comando ls. Es muy probable que ya esté familiarizado con ls y sabe que al escribirlo por sí mismo se lista el contenido del directorio de trabajo actual:

$ cd /usr
$ ls
X11R6      doc         i686-pc-linux-gnu  lib      man          sbin   ssl
bin        gentoo-x86  include            libexec  portage      share  tmp
distfiles  i686-linux  info               local    portage.old  src

Al especificar la opción -a, puede ver todos los archivos de un directorio, incluidos los archivos ocultos: los que comienzan con (.). Como se puede ver en el ejemplo siguiente, ls -a revela los archivo . y .. directorio especial de enlaces:

$ ls -a
.      bin        gentoo-x86         include  libexec  portage      share  tmp
..     distfiles  i686-linux         info     local    portage.old  src
X11R6  doc        i686-pc-linux-gnu  lib      man      sbin         ssl

### Listados largos del directorio

También puede especificar uno o más archivos o directorios en la línea de comandos de ls. Si especifica un archivo, ls mostrará ese archivo solamente. Si especifica un directorio, ls mostrará el contenido del directorio. La opción -l resulta muy útil cuando necesita ver los permisos, la propiedad, la hora de modificación y la información de tamaño en su lista de directorios.

En el ejemplo siguiente, usamos la opción -l para mostrar una lista completa de mi directorio /usr.

$ ls -l /usr
drwxr-xr-x    7 root     root          168 Nov 24 14:02 X11R6
drwxr-xr-x    2 root     root        14576 Dec 27 08:56 bin
drwxr-xr-x    2 root     root         8856 Dec 26 12:47 distfiles
lrwxrwxrwx    1 root     root            9 Dec 22 20:57 doc -> share/doc
drwxr-xr-x   62 root     root         1856 Dec 27 15:54 gentoo-x86
drwxr-xr-x    4 root     root          152 Dec 12 23:10 i686-linux
drwxr-xr-x    4 root     root           96 Nov 24 13:17 i686-pc-linux-gnu
drwxr-xr-x   54 root     root         5992 Dec 24 22:30 include
lrwxrwxrwx    1 root     root           10 Dec 22 20:57 info -> share/info
drwxr-xr-x   28 root     root        13552 Dec 26 00:31 lib
drwxr-xr-x    3 root     root           72 Nov 25 00:34 libexec
drwxr-xr-x    8 root     root          240 Dec 22 20:57 local
lrwxrwxrwx    1 root     root            9 Dec 22 20:57 man -> share/man
lrwxrwxrwx    1 root     root           11 Dec  8 07:59 portage -> gentoo-x86/
drwxr-xr-x   60 root     root         1864 Dec  8 07:55 portage.old
drwxr-xr-x    3 root     root         3096 Dec 22 20:57 sbin
drwxr-xr-x   46 root     root         1144 Dec 24 15:32 share
drwxr-xr-x    8 root     root          328 Dec 26 00:07 src
drwxr-xr-x    6 root     root          176 Nov 24 14:25 ssl
lrwxrwxrwx    1 root     root           10 Dec 22 20:57 tmp -> ../var/tmp

La primera columna muestra información de permisos para cada elemento del listado. Voy a explicar cómo interpretar esta información más adelante. La siguiente columna muestra el número de enlaces a cada objeto del sistema de archivos, que pasaremos por alto ahora, pero volveremos a ello más tarde. Las columnas tercera y cuarta listan el propietario y el grupo, respectivamente. La quinta columna muestra el tamaño del objeto. La sexta columna es el tiempo de "última modificación" o "mtime" del objeto. La última columna es el nombre del objeto. Si el archivo es un enlace simbólico, verá un apuntador -> y la ruta a la que apunta el enlace simbólico.

### Mirando los directorios

A veces, usted querrá mirar un directorio, en lugar de dentro de él. Para estas situaciones, puede especificar la opción -d, que le dirá a ls que busque en cualquier directorio que normalmente buscaría en su interior:

$ ls -dl /usr /usr/bin /usr/X11R6/bin ../share
drwxr-xr-x    4 root     root           96 Dec 18 18:17 ../share
drwxr-xr-x   17 root     root          576 Dec 24 09:03 /usr
drwxr-xr-x    2 root     root         3192 Dec 26 12:52 /usr/X11R6/bin
drwxr-xr-x    2 root     root        14576 Dec 27 08:56 /usr/bin

### Listados recursivos e inode

Así que puede usar -d para buscar en un directorio, pero también puede usar -R para hacer lo contrario: no sólo mirar dentro de un directorio, sino recursivamente buscar dentro de todos los archivos y directorios dentro de ese directorio! No incluiremos ningún ejemplo de salida para esta opción (ya que generalmente es voluminosa), pero es posible que desee probar algunos comandos ls -R y ls -Rl para obtener una idea de cómo funciona.

Finalmente, la opción ls -i  se puede usar para mostrar los números de inodo de los objetos del sistema de archivos en el listado:

$ ls -i /usr
   1409 X11R6        314258 i686-linux           43090 libexec        13394 sbin
   1417 bin            1513 i686-pc-linux-gnu     5120 local          13408 share
   8316 distfiles      1517 include                776 man            23779 src
     43 doc            1386 info                 93892 portage        36737 ssl
  70744 gentoo-x86     1585 lib                   5132 portage.old      784 tmp

### Comprensión de los inodos

A cada objeto de un sistema de archivos se le asigna un índice único, denominado número de inodo. Esto puede parecer trivial, pero entender los inodes es esencial para entender muchas operaciones del sistema de archivos. Por ejemplo, considere los enlaces . y ..  que aparecen en cada directorio. Para entender completamente lo que realmente es un directorio, primero echaremos un vistazo al número de inodo de /usr/local:

$ ls -id /usr/local
   5120 /usr/local
   
El directorio /usr/local tiene un número de inodo de 5120. Ahora echemos un vistazo al número de inodo de /usr/local/bin/ ..:

$ ls -id /usr/local/bin/..
   5120 /usr/local/bin/..
   
Como puede ver, /usr/local/bin/ tiene el mismo número de inode que /usr/local! Así es como podemos enfrentarnos a esta sorprendente revelación. En el pasado, hemos considerado a / usr / local como el propio directorio. Ahora, descubrimos que el inode 5120 es de hecho el directorio, y hemos encontrado dos entradas de directorio (llamadas "enlaces") que apuntan a este inodo. Ambos /usr/local y /usr/local/bin/.. son enlaces a inode 5120. Aunque inode 5120 sólo existe en un lugar en el disco, varias cosas enlazan a él. Inode 5120 es la entrada real en el disco.




