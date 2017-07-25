Paths(Rutas)

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









