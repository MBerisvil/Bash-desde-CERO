![Logo Bash desde cero con Warp](./bash_warp.png)

# 11 - PROCESOS Y ALIAS


## Monitorización

* `ps` muestra los procesos asociados a la terminal actual
* `ps aux` muestra la lista de todos los procesos en ejecución del sistema.
	* `a` procesos de todos los usuarios.
	* `u` muestra el nombre de usuario y detalles.
	* `x` muestra procesos no asociados a la terminal.
* `top` monitor de procesos interactivo en tiempo real.
* `htop` versión mejorada de `top` (requiere instalación del CLI).
* `free -h` muestra información sobre la memoria (sólo disponible en Linux).
* `df -h` uso de disco (disk free).
* `du -sh *` tamaño de todos los archivos y directorios actuales (disk usage).

> [!IMPORTANT]  
> 
> La opción `-h` suele estar asociada a mostrar la información en formato "*human-readable*", para facilitar su lectura.

> [!TIP]
> 
> El **PID** hace referencia al identificador único del proceso para acceder a su manipulación.
> 
> Para salir del monitor utiliza `Ctrl/Cmd + C`.

## Trabajos (jobs)

* `jobs` muestra los procesos actuales de la sesión.
* `Ctrl/Cmd + Z` para suspender un proceso.
* bg %[número_job] reanuda el proceso en segundo plano (background).
* fg %[número_job] trae el proceso al frente (foreground).


> [!TIP]
> 
> Utiliza `sleep [segundos]` para simular un job que "duerme" el sistema.

## Matar procesos

* `kill PID` elimina el proceso asociado a su PID.
* `kill -9 PID` elimina con forzado el proceso asociado a su PID.

## Historial

* `history` muestra el historia de comandos.
* `!!` repite el último comando.
* `!` expansión de comandos:
	* `!10` ejecuta el comando número *10*.
	* `!ls` ejecuta el último comando que empezó con `ls`.

> [!WARNING] 
>  
> Cuidado al escribir `!` en una cadena de texto, ya que puede intentar realizar un referencia al historial y producir un error. Para evitarlo, puedes escapar el signo utilizando la barra invertida `\` antes de `!`. También puedes usar comillas simples `'` en vez de dobles `"` para crear la cadena de texto.

## Alias

Un alias crea atajos para comandos.

* `alias atajo=comando`
* `alias ll='ls -l'` crea el comando `ll` que lanzará `ls -l`.
* `unalias ll` elimina el alias.

> [!CAUTION]
> 
> El alias también es temporal. Puedes agregarlo a un script de configuración para hacerlo permanente.

