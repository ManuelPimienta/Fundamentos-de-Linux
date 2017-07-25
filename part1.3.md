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

Sin argumentos, cd cambiará a su directorio de inicio, que es /root para el superusuario y normalmente /home/nombre de usuario para un usuario normal. Pero ¿qué pasa si queremos especificar un archivo en nuestro directorio personal? Tal vez queramos pasar un argumento de archivo al comando myprog. Si el archivo vive en nuestro directorio personal, podemos escribir:




