![Logo Bash desde cero con Warp](./bash_warp.png)


# 9 - ADMINISTRACIÓN DEL SISTEMA

> [!NOTE]  
> 
> En Unix/Linux, cada archivo o directorio tiene permisos para controlar quién puede **leer**, **escribir** o **ejecutarlo**.

## Tipos de permiso

### Modo simbólico:

* `r` lectura
* `w` escritura
* `x` ejecución

### Modo octal:

* `4` (`r`) lectura
* `2` (`w`) escritura
* `1` (`x`) ejecución

## Tipos de usuario

* `u` usuario propietario
* `g` grupo de usuarios
* `o` otros
* `a` todos

## Ver permisos

* En archivos: `ls -l nombre_archivo`
* En carpetas: `ls -ld nombre_directorio`

## Anatomía de los permisos

### Modo simbólico:

`-rwxrwxrwx`

Está formado por cuatro bloques: `[-][rwx][rwx][rwx]`

De izquierda a derecha:

* `-` tipo de archivo
* `rwx` permisos de usuario
* `rwx` permisos de grupo
* `rwx` permisos para otros usuarios

`rwx` está indicando que ese bloque tiene permisos de lectura (`r`), escritura (`w`) y ejecución (`x`).

> [!WARNING]  
> 
> La ausencia de un permiso (permimso no otorgado) se representa con `-`.
> 
> Ejemplos: `r--` indicaría que sólo tiene permisos de lectura, en cambio, `r-x` indicaría que tiene permisos de lectura y ejecución. Siempre se conserva el orden `rwx`.

### Modo octal:

`777`

* Está formado por 3 dígitos, representando de izquierda a derecha los bloques de `[usuario][grupo][otros]`.
* Cada número es el resultado de sumar el valor asociado al tipo de permiso:
	* `7` = 4 + 2 + 1 (lectura + escritura + ejecución) [`rwx`]
	* `6` = 4 + 2 (lectura + escritura) [`rw-`]
	* `5` = 4 + 1 (lectura + ejecución) [`r-x`]
	* `4` (lectura) [`r--`]
	* `3` = 2 + 1 (escritura + ejecución) [`-wx`]
	* `2` (escritura) [`-w-`]
	* `1` (ejecución) [`--x`]

Por lo tanto, `777` quiere decir que todos los usuarios tienen permisos de lectura, escritura y ejecución.

`764` significaría que el *propietario* tiene todos los permisos (4 + 2 + 1 = 7), el *grupo* tendría de lectura y escritura (4 + 2 = 6), y *otros* únicamente de lectura (4).

### Tipos de archivos más habituales

* `-` archivo
* `d` directorio
* `l` enlace simbólico
* `d` dispositivo de bloque
* `c` dispositivo de carácter
* `s` socket
* `p` pipe

## Modificación de permisos

* Se utiliza el comando `chmod`.

### Modo simbólico:

* `chmod [tipo_usuario][+/-][permiso] nombre_archivo/directorio`
* `+` para otorgar un permiso.
* `-` para eliminar un permiso.
* Ejemplos:
	* `chmod u+x nombre_archivo/directorio`: Otorga permisos de ejecución al usuario propietario.
	* `chmod u-x nombre_archivo/directorio`: Elimina permisos de ejecución para el usuario propietario.

### Modo octal:

* `chmod [permisos_octal] nombre_archivo/directorio`
* Ejemplos:
	* `chmod 753 nombre_archivo/directorio`: u=`rwx`, g=`r-x`, o=`-wx`
	* `chmod 642 nombre_archivo/directorio`: u=`rw-`, g=`r--`, o=`-w-`

## Cambiar propietario y grupo

* `chown [usuario] nombre_archivo/directorio` para cambiar el propietario.
* `chown [usuario]:[grupo] nombre_archivo/directorio` para cambiar el propietario y el grupo.

## Máscara de permisos

La máscara hace referencia a los permisos por defecto que se le otorgarán a nuevos directorios o archivos.

* `umask` muestra la máscara de permisos por defecto.
* `umask [permisos_octal]` establece los permisos por defecto.
	* Ejemplo: `umask 022`

> [!CAUTION]
> 
> La modificación de la máscara es temporal, y sólo afecta a la sesión de la shell actual. Para hacerlo permanente, puedes agregarlo al script de configuración de Bash (como en el caso de variables globales explicado en una lección anterior).

### Cálculo de permisos con máscara

La máscara hace referencia a los valores que deben restarse a los permisos máximos razonables de un directorio o archivo.

* Permisos máximos razonables para un directorio: `777`
* Permisos máximos razonables para un archivo: `666` (Sin ejecución, ya que dar esos permisos por defecto a todos los archivos sería peligroso)

Si la máscara de permisos es `0022`, quiere decir lo siguiente:

* Si la máscara tiene 4 dígitos, el primer cero de la izquierda únicamente indica que la representación de los 3 siguientes está en sistema octal.
* 0 al usuario no le quito ningún permiso
* 2 a los grupos le quito el permiso de escritura (2)
* 2 a otros le quito el permiso de escritura (2)

Cálculo de permisos:

* Para directorios: `777` - `022` (bloque a bloque) = `755` [`rwxr-xr-x`]
* Para archivos: `666` - `022` (bloque a bloque) = `644` [`rw-r--r--`]

Esos son los permisos por defecto que se le otorgarían a nuevas carpetas y archivos.

## El superusuario

> [!CAUTION]
> 
> Algunas acciones requieren privilegios de administrador (**root**).
> 
> `sudo [comando]` (solicita la contraseña del superusuario).
> 
> Ejemplo: `sudo rm -rf [directorio_protegido]`

---