## Introducing bash
### The shell

If you've used a Linux system, you know that when you log in, you are greeted by a prompt that looks something like this:

<code>$</code>

The particular prompt that you see may look quite different. It may contain your systems host name, the name of the current working directory, or both. But regardless of what your prompt looks like, there's one thing that's certain. The program that printed that prompt is called a "shell," and it's very likely that your particular shell is a program called bash.

### Are you running bash?

You can check to see if you're running bash by typing:

<code>$ echo $SHELL
/bin/bash</code>

If the above line gave you an error or didn't respond similarly to our example, then you may be running a shell other than bash. In that case, most of this tutorial should still apply, but it would be advantageous for you to switch to bash for the sake of preparing for the 101 exam.

### About bash

Bash, an acronym for "Bourne-again shell," is the default shell on most Linux systems. The shell's job is to obey your commands so that you can interact with your Linux system. When you're finished entering commands, you may instruct the shell to exit or logout, at which point you'll be returned to a login prompt.

By the way, you can also log out by pressing control-D at the bash prompt.

### Using "cd"

As you've probably found, staring at your bash prompt isn't the most exciting thing in the world. So, let's start using bash to navigate around our file system. At the prompt, type the following (without the $):

<code>$ cd /</code>

We've just told bash that you want to work in /, also known as the root directory; all the directories on the system form a tree, and / is considered the top of this tree, or the root. cd sets the directory where you are currently working, also known as the "current working directory."

### Traducción 

## Presentación de bash
### El shell
Si has utilizado un sistema Linux, sabes que cuando inicias sesión, te recibe un mensaje que se parece a esto:

<code>$</code>

El indicador particular que ve puede verse muy diferente. Puede contener el nombre de host del sistema, el nombre del directorio de trabajo actual o ambos. Pero independientemente de lo que su mensaje muestre, hay una cosa cierta. El programa que imprimió ese mensaje se denomina "shell", y es muy probable que su shell particular sea un programa llamado bash.

### ¿Está ejecutando bash?

Puede comprobar si está ejecutando bash escribiendo:

<code>$ echo $SHELL
/bin/bash</code>

Si la línea anterior le dio un error o no respondió de manera similar a nuestro ejemplo, puede estar ejecutando un shell que no sea bash.
En ese caso, la mayor parte de este tutorial todavía debe aplicarse, pero sería ventajoso que usted cambie a bash para una buena preparación del examen 101.

### Acerca de bash

Bash, un acrónimo de "Bourne-again shell", es el shell por defecto en la mayoría de los sistemas Linux. El trabajo de la shell es obedecer sus comandos para que pueda interactuar con su sistema Linux. Cuando haya terminado de introducir los comandos, puede indicar al shell que salga o cierre la sesión, momento en el que se le devolverá a un indicador de inicio de sesión.

Por cierto, también puedes cerrar la sesión pulsando control-D en el prompt de bash.

### Usando "cd"

Como usted probablemente ha encontrado, mirar la salida de bash no es la cosa más emocionante en el mundo. Por lo tanto, vamos a empezar a usar bash para navegar por nuestro sistema de archivos. En el indicador, escriba lo siguiente (sin el $):

<code>$ cd /</code>

Acabamos de decirle a bash que quieres trabajar en /, también conocido como el directorio raíz; todos los directorios en el sistema forman un árbol, y / se considera la parte superior de este árbol, o la raíz. cd establece el directorio en el que está trabajando actualmente, también conocido como el "directorio de trabajo actual".
