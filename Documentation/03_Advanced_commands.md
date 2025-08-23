![Logo Bash desde cero con Warp](./bash_warp.png)

# 5 - COMANDOS AVANZADOS

## Lectura de archivos

* `cat` Muestra todo el contenido del archivo en pantalla (útil para archivos pequeños).
* `less` Permite ver archivos largos, paginando su contenido (sales pulsando `q`).
* `more` Similar a less, pero como menos funcionalidades (por ejemplo, no puedes desplazarte hacia atrás).
* `head` Muestra las primeras 10 líneas de un archivo por defecto.
	* `head -n 20` Para especificar el número de líneas.
* `tail` Muestra las últimas 10 líneas de un archivo por defecto.
	* `tail -n 20` Para especificar el número de líneas.
	* `tail -f file.log` Muy útil para ver logs en tiempo real mientras crecen.

> [!TIP]
>
> Para desplazarte por la paginación es habitual usar flechas, barra espaciadora, scroll o PgUp/PgDown.

## Búsqueda y recuento

Búsqueda: `grep` busca patrones dentro de archivos o de la salida de otros comandos.

* `grep "texto a buscar" nombre_archivo` Busca un texto en un archivo (retorna las filas en las que aparece el texto).
	* `grep -i "texto a buscar" nombre_archivo` Busca el texto ignorando mayúsculas/minúsculas.
	* `grep -r "texto a buscar" dir` Busca el texto recursivamente en directorios

Recuento: `wc` cuenta líneas, palabras y bytes/caracteres.

* `wc nombre_archivo` Muestra el recuento de líneas, palabras y bytes/caracteres.
	* `wc -l nombre_archivo` Muestra el recuento de líneas.
	* `wc -w nombre_archivo` Muestra el recuento de palabras.
	* `wc -c nombre_archivo` Muestra el recuento de bytes/caracteres.

Como siempre, las opciones se pueden combinar: `wc -lw nombre_archivo`.

## Redirecciones y pipes

### Redirecciones

* `>` Redirige la salida y sobrescribe el archivo.
* `>>` Redirige la salida y añade al final del archivo.
* `<` Toma la entrada desde un archivo.

Ejemplos:

* `echo "texto" > archivo.txt` Sobrescribe el contenido del archivo con la salida del comando (en este caso, imprimir un texto).
* `echo "texto" >> archivo.txt` Añade al contenido del archivo la salida del comando (en este caso, imprimir un texto).
* `sort < archivo.txt` Usa el archivo como entrada y ejecuta el comando con su contenido (en este caso, ordenar).

### Pipes

* `|` Encadena comandos.

Ejemplo:

* `cat nombre_archivo | grep "texto a buscar" | wc -w` Muestra el contenido de un archivo, busca un texto en ese contenido y realiza el recuento de palabras resultantes de la búsqueda.

## Variables de entorno

Puedes definir variables temporalmente (locales) o que existan en todo momento (globales).

### Variable local

Las variables locales solo viven en la sesión actual.

* `nombre_variable="valor asociado a la variable"` Almacena el valor de un texto en una variable.
* `echo $nombre_variable ` Muestra el valor de la variable.

### Variable global

Las variables globales más allá de la sesión (en todos los programas lanzados desde esa terminal de la sesión).

**Algunas variables globales ya existentes:**

* `echo $HOME` Muestra la ruta del directorio home del usuario.
* `echo $PATH` Muestra una lista de rutas separadas conocidas por el sistema por defecto.

**Creación de una variable global:**

* `export NOMBRE_VARIABLE="valor asociado a la variable"`

**Creación de una variable global permanente:**

Para ello debes agregar la línea de la exportación a tu archivo de configuración de la shell. Los archivos de configuración más habituales creados en tu directorio de usuario son:

* `~/.bash_profile`
* `~/.bash_login`
* `~/.profile`
* `~/.bashrc`
