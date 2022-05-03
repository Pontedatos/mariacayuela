# Metodología del proceso de compilación de los trabajos de la asignatura y su posterior visualización mediante GitHub Pages

***María Cayuela***

En este apartado, explicaré cómo he creado este repositorio, cómo he incluido todos los materiales de la asignatura y, finalmente, cómo he activado GitHub Pages para mostrarlo como una web.

## 1. Nuevo repositorio y compilación de los trabajos

Lo primero es crear el repositorio que usaremos para agrupar todas las prácticas de la materia, y que será la fuente desde donde GitHub Pages muestre la página web. Para ello, creamos un repositorio nuevo en GitHub, y especificamos que el propietario sea la organización Pontedatos en vez de nuestro usuario personal. En el nombre del repositorio, ponemos nuestro nombre de usuario, por lo que el repositorio quedará `Pontedatos/mariacayuela`.

Luego, conectamos dicho repositorio a nuestra carpeta local para que queden conectadas. Para ello, en el siguiente paso a crear el repositorio son las instrucciones para hacer el proceso. En nuestra carpeta local ya creada, metemos los trabajos y las prácticas que hemos hecho, que podemos copiarlas desde la terminal mediante el comando `cp`, indicando las rutas de origen y las de destino. Luego, situados en esa carpeta y con los archivos ya copiados, indicamos que esa carpeta va a ser un directorio Git con `git init`. Luego, seguimos el proceso que hemos venido haciendo durante todo el curso: añadimos los archivos con `git add` y creamos el commit y su mensaje con `git commit -m "mensaje"`. 

Una vez hecho esto, seleccionamos la rama principal, con `git branch -M main`, añadimos el origen remoto (nuestro repositorio en GitHub) con `git remote add origin https://github.com/Pontedatos/mariacayuela` y, finalmente, hacemos *push* para subir los archivos a GiHub: `git push -u origin main`.

## 2. Crear la estructura para la web

Para crear la web, tenemos que tener una estructura óptima para mostrar correctamente todos los archivos. GitHub Pages coge la estructura del repositorio y, por ello, en el repositorio no existirán carpetas, sino que todos los archivos estarán al mismo nivel, para facilitar los enlaces y la visualización. 

Una vez estructurado el repositorio y tras asegurarnos de que están todos los documentos necesarios organizados (y sin carpetas), activamos Pages. Para ello, vamos a los Ajustes (*Settings*) del repositorio, y en el apartado Código y automatización (*Code and automation*) seleccionamos Pages. Antes de activarla, tenemos que hacer dos ajustes. El primero, elegir como fuente la rama `main` del repositorio como `/root` y guardamos. Luego, si queremos elegir un diseño para que no sea un HTML plano, lo hacemos en el apartado de *Theme Chooser*. 

Una vez hecho esto, GitHub Pages crea nuestra web, cogiendo como base [pontedatos.github.io/](pontedatos.github.io) a lo que añade el nombre de nuestro repositorio, por lo que quedaría como [pontedatos.github.io/mariacayuela](pontedatos.github.io/mariacayuela). Como vemos al visitar la web, GitHub ha transformado el archivo `README.md` en la página de inicio, que al ser HTML es `index.html`. De igual forma, el resto de documentos escritos en Markdown GitHub los convierte a HTML para que sean interpretados y renderizados de forma correcta por los navegadores. 