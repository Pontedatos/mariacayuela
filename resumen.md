# Resumen de los contenidos de la asignatura

*María Cayuela. Grupo 63*

En este apartado, haremos un resumen de lo que hemos aprendido y puesto en práctica a lo largo del cuatrimestre en Periodismo de datos: desde instalar y configurar nuestro programa de emulación de la terminal a usar `git` como software de control de versiones y vincular nuestros repositorios locales con aquellos en nuestro [GitHub](https://www.github.com/).

## 1. Instalación de un programa de emulación de la terminal

A lo largo del curso, las estudiantes que usamos Windows hemos instalado y configurado dos programas diferentes de emulación de la terminal. 

Por un lado, WSL (*[Windows Subsystem for Linux](https://docs.microsoft.com/es-es/windows/wsl/)*), una herramienta nativa de Microsoft Windows, que es una suerte de virtualización de una distribución de Linux, que en nuestro caso ha sido Ubuntu. Todo ello, sin optar por las clásicas máquinas virtuales, por lo que de esta forma, hemos accedido a Ubuntu en su versión `cli` , sin interfaz gráfica sino solo a través de la terminal. 

Por otro lado, también hemos instalado *[Cygwin](https://www.cygwin.com/)*, un programa que emula los sistemas Unix dentro del sistema operativo Windows. A diferencia de *WSL*, no instalamos un sistema operativo, sino solo una terminal Unix dentro de nuestro sistema. 

### WSL: instalación de Ubuntu

En el caso de WSL, su instalación se lleva a cabo a través de la PowerShell de Windows, la terminal desarrollada por Microsoft. Para hacerlo, tenemos que abrir una nueva sesión de la misma como administradores, y ejecutar el comando `wsl --install -d Ubuntu`. De esta forma, estaremos especificando que queremos instalar (`--install`) la distribución (`-d`) [Ubuntu](https://ubuntu.com/), una de las distribuciones de Linux [más populares](https://distrowatch.com/dwres.php?resource=popularity). 

Una vez se ha instalado, Windows nos pedirá que reiniciemos nuestro ordenador. Una vez de vuelta a nuestro escritorio, ya podremos ejecutar Ubuntu, que se encontrará disponible en el menú de Inicio. La primera vez que lo iniciemos, nos pedirá crear un usuario y una contraseña para el usuario UNIX, para evitar acceder al sistema como «superusuarios» (*root*), que tiene todos los privilegios como administrador. Cuando lo hagamos, ya tenemos una instalación nueva de Ubuntu a través de WSL.

### Cygwin: Unix en Windows
También hemos instalado *Cygwin*, cuyo instalador ejecutable tendremos que descargar de su [web](https://www.cygwin.com/), ya que no es una herramienta nativa de Microsoft, sino un programa desarrollado por Cygnus Solutions en un primer momento, y posteriormente por [Red Hat](https://www.redhat.com/es) cuando esta compró a la primera.

Cuando ejecutamos el archivo instalador de *Cygwin* (`setup-x86_64.exe`), este nos guiará por el proceso. En primer lugar, nos preguntará desde dónde queremos instalarlo, y seleccionamos la opción «Instalar desde Internet». Lo siguiente será elegir dónde instalar *Cygwin*: desde [su documentación](https://www.cygwin.com/faq.html#faq.setup.c) nos sugieren instalarla en una partición diferente a `C:\`, la raíz de Windows, pero para aquellas que solo tenemos una partición, no podemos instalarlo fuera de la raíz del sistema, así que dejamos la ruta por defecto.

La siguiente pantalla nos mostrará una lista con todos los *mirrors* desde donde podemos descargar *Cygwin*: los *mirrors* son servidores espejos repartidos por todo el mundo para garantizar la máxima velocidad y disponibilidad a cualquier usuario del planeta, así que podemos elegir uno cercano a España. Para ello, buscamos en la lista algún dominio `.es` o de otro país cercano, como Portugal (`.pt`), Francia (`.fr`) o Italia (`.it`).

Una vez completado este proceso, *Cygwin* nos preguntará si queremos instalar paquetes antes de terminar la instalación. Para hacerlo, en la pantalla que nos aparezca, tenemos que marcar la opción *Full* dentro de la pestaña *View*. Mediante el recuadro de búsqueda, instalamos los siguientes paquetes: `libcurl4`, `wget`, `ca-certificates-letsencrypt`, `lynx`, `nano` y `openssl`. Para instalarlos, en cada paquete, bajo la columna *New*, le damos a la flecha de nuestro paquete y seleccionamos la última opción/versión. Ya habríamos terminado la instalación.

## 2. Configuración del programa

Una vez instalados, hemos configurado algunos parámetros tanto de WSL como de *Cygwin*, como algún alias, cambiar la *home* o configurar `git`.

### Establecer alias

Vamos a crear un alias en la terminal para ahorrarnos escribir toda la ruta de nuestra carpeta de Periodismo de datos entera. Es decir, que en vez teclear, por ejemplo, `cd ‘/mnt/c/Users/usuaria/Documentos/Apuntes/Periodismo de Datos/’`, si tecleamos `micasa`, nos hará la misma acción.

Para hacerlo, tenemos que editar el archivo de configuración de Bash. Está en el directorio «casa» u «hogar» de nuestro usuario: `$HOME/.bashrc`. Tenemos dos maneras de hacerlo: desde la línea de comandos directamente o editando el archivo `.bashrc` desde `nano`. 

Desde la línea de comandos, hacemos uso de `echo` y enviamos la salida con `>>` al final del archivo `.bashrc`: `echo “alias micasa=“cd ‘/mnt/c/Users/usuaria/Documentos/Apuntes/Periodismo de Datos/’” >> $HOME/.bashrc`.

Cerramos la sesión actual de nuestra terminal y podemos hacerlo con el comando `exit`. Al volver a abrir Ubuntu o Cygwin, verificamos que funciona tecleando el alias (`micasa`) en la terminal: si nos lleva a la carpeta está bien hecho. Podemos ver el archivo de configuración con `cat $HOME/.bashrc` y vemos esta línea del alias al final. Podemos corregir o editar el archivo con `nano $HOME/.bashrc`. 

### Cambiar la home de Cygwin a la de Windows

En Cygwin, vamos a cambiar la ruta de «hogar» o «casa» de nuestro usuario para que sea la de Windows. Lo hacemos editando el archivo `nsswith.conf` con `nano`: `nano /etc/nsswith.conf`. Al final del archivo, ponemos `db_home: windows`.

Guardamos (CTRL + O) y cerramos (CTRL + X). Cerramos Cygwin y volvemos a entrar para que se actualice. Comprobamos con `pwd`: nos tiene que salir `/cygdrive/c/Users/usuaria`.  

### Configurar git

Tenemos que configurar nuestro usuario de GitHub en la terminal para vincular los cambios que hagamos en nuestros archivos en local con nuestros repositorios en la nube (GitHub). Para ello, en nuestra terminal, tenemos que escribir `git config --global user.name nuestrousuario` (sustituyendo `nuestrousuario` por el nuestro), y luego `git config --global user.email correogithub` (sustituyendo igualmente `correogithub` por el email con el que nos hayamos dado de alta en la plataforma). 

Si hemos hecho algún *commit* antes de hacer estas configuraciones, tenemos que deshacerlos para que no se suben los cambios con un usuario local. Usamos `git commit --amend --reset-author`. Luego configuraremos nuestro usuario y correo que hemos puesto en GitHub, como hemos hecho antes: `git config --global user.name nuestrousuario` , y luego, `git config --global user.email correogithub`.



## Configuración de un programa de edición de texto

Podemos editar el comportamiento de nuestro editor de texto `nano` a través de su archivo de configuración. En nuestro caso, vamos a hacer que se ajuste el texto a la resolución de la pantalla y que aparezca el número de las líneas para poder visualizar y localizar mejor el contenido del archivo. Para ello, lo editamos de la siguiente forma: `nano $HOME/.nanorc` y ponemos lo siguiente:

`# Ajustar el texto a pantalla`

`set softwrap`

`# Numerar las líneas`

`set linenumbers`

Con Cygwin el método es algo diferente. Tenemos que copiar el archivo de configuración de `nano` que se sitúa en el directorio `/etc`. Lo copiamos a nuestro directorio *home* con `cp /etc/nanorc .nanorc`, y lo editamos: `nano .nanorc`. 
Buscamos con CTRL + W “linenumbers” (sin comillas), y en su línea (`# set linenumbers`) le quitamos la #. Volvemos a buscar con CTRL + W “softwrap” (sin las comillas), y en su línea (`# set softwrap`) le quitamos la #. Guardamos con CTRL + O y salimos con CTRL + X.

## Configuración y funcionamiento de un gestor de paquetes/programas del emulador de la terminal

Un gestor de paquetes, tal y como se explica en la Wikipedia, «es una colección de herramientas que sirven para automatizar el proceso de instalación, actualización, configuración y eliminación de paquetes de software», principalmente para instalar programas y herramientas en sistemas Unix como GNU/Linux. En el caso de Ubuntu es `apt` y Cygwin tiene el suyo propio, `apt-cyg`, que no viene de fábrica con el programa, a diferencia del primero.

El proceso para instalar `apt-cyg` está disponible en la documentación de su [GitHub](https://github.com/transcode-open/apt-cyg#quick-start). Lo instalamos con `lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg` y luego `install apt-cyg /bin`.

Luego podremos usarlo para instalar herramientas, como `nano`, mediante la sintaxis `apt-cyg install herramienta`, como `apt-cyg install nano`.

## Versión del lenguaje de SHELL utilizado

Para comprobar la versión del lenguaje de Shell utilizado, tenemos dos comandos que nos pueden indicar la misma, tanto para Cygwin como para WSL. Podemos usar la variable de entorno `$0`, que la consultaremos con `echo $0` y nos devolverá qué Shell utilizamos, que en ambos casos es Bash. 

Para comprobar la versión de Bash, tenemos dos opciones (tanto en WSL como en Cygwin): la primera, usar la variable de entorno `$BASH_VERSION`, a través de `echo`; la segunda, a través del propio `bash`, especificando la opción `--help`: `bash --help`. 

### Shell en Cygwin

`$ echo $0`

`-bash`

```$ echo $BASH_VERSION```
```4.4.12(3)-release```

`$ bash --version`
`GNU bash, version 4.4.12(3)-release (x86_64-unknown-cygwin)`

### Shell WSL

`echo $0`

`-bash`

`echo $BASH_VERSION`
`5.0.17(1)-release`

`bash --version`
`GNU bash, version 5.0.17(1)-release (x86_64-pc-linux-gnu)`

## Valor de la variable de entorno PATH

Para consultar la variable de entorno `$PATH`, lo hacemos con `echo $PATH`. La terminal nos devolverá las rutas en las que se encuentran los programas instalados que puede ejecutar la terminal. Separados por dos puntos (`:`), aparecen los directorios donde la terminal va a buscar los programas para ejecutarlos cuando lo indiquemos así a través de los comandos. 

## Comandos utilizados y ejemplos.

*Los comandos tienen la siguiente estructura: comando / opciones / argumentos*

  - `ls [ruta del directorio]` → listar un directorio (ver qué archivos y carpetas hay en la ruta en la que estamos). Si queremos ver el directorio actual, no hace falta especificar la ruta. 
  - `cd [ruta al directorio]` → acceder a un directorio en específico. Si escribimos solo `cd`, vamos al directorio raíz. `cd ..`, nos sube un directorio. Con `cd -` nos lleva al último sitio en el que estábamos.
  - `pwd` → nos indica en qué ruta estamos actualmente.
  - `mkdir [nombre carpeta]` → crear una carpeta nueva especificando su nombre.
  - `&&` → sirve para ejecutar dos comandos en una misma línea o de una vez. Por ejemplo, si queremos crear una carpeta y luego situarnos dentro, escribimos: `mkdir micarpeta && cd micarpeta`.
  - `|` (Alt Gr + 1) → para pasar de una salida a una entrada. Por ejemplo, si queremos hacer un `cat` para leer un archivo pero visualizarlo con `less`, escribimos `cat README.md | less`.
  - `man` → este comando es el de “manual”, el que nos dice qué hace un comando y nos muestra todas las opciones posibles. Por ejemplo, si queremos saber qué hace `ls` y qué opciones podemos usar (como que nos especifique quién es el propietario de un archivo o carpeta), tenemos que usar `man ls`. Por defecto, utiliza el visor `| more`, que para avanzar por el documento tenemos que ir clickando en la barra espaciadora, y para salir pulsar la tecla `q`. También está disponible `| less` (`man ls | less`)
  - `cat` → sirve para previsualizar  el archivo en la propia terminal. Por ejemplo, `cat README.md`. 
  - `mv [origen] [destino]` → sirve para mover (cortar) las carpetas o archivos de sitio, pero también para renombrarlos. Si queremos mover la carpeta de periodismo de datos (`/mnt/c/Users/usuaria/Documentos/periodismo-de-datos`) a otro lado, escribimos: `mv /mnt/c/Users/usuaria/Documentos/periodismo-de-datos /mnt/c/Users/usuaria/Documentos/Apuntes/` . Como vemos, después de `mv` escribimos la ruta de origen y lo siguiente es el directorio de destino. Si queremos renombrar, escribimos `mv periodismo-de-datos nuevo-nombre`.
  - `cp [origen] [destino]` → sirve para copiar y pegar carpetas o archivos. La sintaxis es igual que `mv`. 
  - `nano [archivo]` → el editor de texto. Para editar con `nano`, tenemos que escribir `nano` seguido del nombre del archivo. Si estamos en la carpeta de la asignatura, por ejemplo, escribimos `nano README.md`. Para guardar usamos CTRL + O, y para salir del editor CTRL + X.
  - `echo` → sirve para que la terminal nos devuelva un texto. Si queremos que la terminal nos diga Hola, escribimos `echo Hola`. Si queremos que nos diga cuál es nuestra home, escribimos `echo $HOME` (variable de entorno)
  - `env` → este comando sirve para visualizar en pantalla todas las variables de entorno. Si lo usamos con `| less`, es un visor más ameno porque son demasiadas variables y no caben en la pantalla: `env | less`. 
  - `touch [nombrearchivo]` → es el comando para crear un archivo nuevo. Por ejemplo, si queremos crear un README.md en nuestra carpeta, escribimos `touch README.md` y ya está creado.
  - `tree` → es como `ls` pero con más opciones. Con `tree -L 1` le decimos cuántos niveles queremos ver. También podemos poner `tree -L 2` o `tree -L 3`, según el nivel de detalle (a más alto el número, más detalles).
  - `rm [archivo/carpeta]` → es el comando para eliminar archivos o directorios, pero de forma irrecuperable, sin pasar por una Papelera de reciclaje o similar.
  - `wget [enlace]` → para descargarnos un archivo/contenido de una web. Tenemos que copiar el enlace de lo que nos queramos descargar. 
  - `curl [enlace]` → es igual que wget pero con más opciones.