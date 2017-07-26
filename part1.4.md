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

De hecho, podemos ver el número total de veces que el inodo 5120 se referenciado usando el comando

<code>ls -dl</code>

Comando:

<code>$ ls -dl /usr/local</code>

<code>drwxr-xr-x    8 root     root          240 Dec 22 20:57 /usr/local</code>

Si echamos un vistazo a la segunda columna de la izquierda, vemos que el directorio / usr / local (inode 5120) se hace referencia ocho veces. En mi sistema, aquí están los varios caminos que hacen referencia a este inodo:

/usr/local
/usr/local/.
/usr/local/bin/..
/usr/local/games/..
/usr/local/lib/..
/usr/local/sbin/..
/usr/local/share/..
/usr/local/src/..

### mkdir

Echemos un rápido vistazo al comando mkdir, que se puede utilizar para crear nuevos directorios. El siguiente ejemplo crea tres nuevos directorios, tic, tac y toe, todos bajo /tmp:

$ cd /tmp
$ mkdir tic tac toe

De forma predeterminada, el comando mkdir no crea directorios principales para usted; toda la ruta desde el primer elemento hasta el último necesita existir. Por lo tanto, si desea crear los directorios ganados won/der/ful, necesitará emitir tres comandos mkdir independientes:

$ mkdir won/der/ful
mkdir: cannot create directory won/der/ful: No such file or directory
$ mkdir won
$ mkdir won/der
$ mkdir won/der/ful

'Sin embargo, mkdir tiene una opción práctica -p que le dice a mkdir que cree cualquier directorio padre faltante, como puede ver aquí:'

$ mkdir -p easy/as/pie

En general, es bastante sencillo. Para obtener más información sobre el comando mkdir, escriba man mkdir para leer la página de manual. Esto funcionará para casi todos los comandos cubiertos aquí (por ejemplo, man ls), excepto para cd, que está incorporado en bash.

### touch

Ahora, vamos a echar un vistazo rápido a los comandos cp y mv, utilizados para copiar, cambiar el nombre y mover archivos y directorios. Para comenzar esta descripción, primero usaremos el comando touch para crear un archivo en /tmp:

$ cd /tmp
$ touch copyme

El comando touch actualiza el "mtime" de un archivo si existe (recuerde la sexta columna en la salida ls -l). Si el archivo no existe, se creará un nuevo archivo vacío. Ahora debe tener un archivo /tmp/copyme con un tamaño de cero.

### echo

Ahora que el archivo existe, vamos a agregar algunos datos al archivo. Podemos hacerlo usando el comando echo, que toma sus argumentos y los imprime a la salida estándar. En primer lugar, el comando de eco en sí mismo:

$ echo "firstfile"
firstfile

Ahora, el mismo comando de eco con redirección de salida:

$ echo "firstfile" > copyme

El signo mayor que indica al shell que escriba la salida de eco en un archivo llamado copyme. Este archivo se creará si no existe y se sobrescribirá si existe. Escribiendo ls -l, podemos ver que el archivo copyme tiene 10 bytes de largo, ya que contiene la palabra firstfile y el caracter newline:

$ ls -l copyme
-rw-r--r--    1 root     root           10 Dec 28 14:13 copyme

### cat y cp

Para mostrar el contenido del archivo en el terminal, utilice el comando cat:

$ cat copyme
firstfile

Ahora, podemos usar una invocación básica del comando cp para crear un archivo copiedme copiado del archivo original:

$ cp copyme copiedme

Tras la investigación, encontramos que son archivos verdaderamente separados; sus números de inodo son diferentes:

$ ls -i copyme copiedme
  648284 copiedme   650704 copyme
  
### mv

Ahora, vamos a usar el comando mv para cambiar el nombre de "copiedme" a "movedme". El número de inodo permanecerá igual; sin embargo, el nombre de archivo que apunta al inodo cambiará.

$ mv copiedme movedme
$ ls -i movedme
  648284 movedme

El número de inodo de un archivo movido permanecerá igual mientras el archivo de destino resida en el mismo sistema de archivos que el archivo de origen. Echaremos un vistazo a los sistemas de archivos en Fundamentos de Linux parte 3 de esta serie de tutoriales.

Mientras hablamos de mv, veamos otra forma de usar este comando. mv, además de permitirnos cambiar el nombre de los archivos, también nos permite mover uno o más archivos a otra ubicación en la jerarquía de directorios. Por ejemplo, para mover /var/tmp/myfile.txt a 
/home/drobbins (que pasa a ser mi directorio personal), podría escribir:

$ mv /var/tmp/myfile.txt /home/drobbins

Después de escribir este comando, myfile.txt se moverá a /home/drobbins/myfile.txt. Y si /home/drobbins está en un sistema de archivos diferente de /var/tmp, el comando mv controlará la copia de myfile.txt al nuevo sistema de archivos y lo borrará del antiguo sistema de archivos. Como se puede adivinar, cuando myfile.txt se mueve entre sistemas de archivos, myfile.txt en la nueva ubicación tendrá un nuevo número de inodo. Esto se debe a que cada sistema de archivos tiene su propio conjunto independiente de números de inodo.

También podemos usar el comando mv para mover varios archivos a un único directorio de destino. Por ejemplo, para mover myfile1.txt y myarticle3.txt a /home/drobbins, podría escribir:

$ mv /var/tmp/myfile1.txt /var/tmp/myarticle3.txt /home/drobbins























