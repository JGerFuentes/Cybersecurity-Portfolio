## Checkpoint - Week 1
- ¿Qué diferencia hay entre `apt` y `dpkg`? ¿Cuándo conviene usar uno u otro?

La diferencia entre `apt` y `dpkg` radica en que el primero es un sistema de gestión de paquetes de Linux que se conecta a Internet y trabaja con repositorios remotos, lo que permite utilizarlo para actualizar, descargar, instalar, buscar y desinstalar paquetes del sistema. **Además, permite resolver dependencias automáticamente**. Mientras que el segundo, se trata de una herramienta de gestión de archivos `.deb`, que no se encuentra conectado a Internet, por lo tanto no descarga nada, y que maneja los paquetes ya instalados de manera local (instalación, borrado y listado **del repositorio local**). El sistema de gestión `apt` utiliza la herramienta de gestión `dpkg` por debajo. 

- ¿Qué hace el comando dpkg -L cowsay?

Este comando permite listar todos los archivos que ~~componen~~ **fueron instalados por** el paquete *cowsay*, ~~una vez instalado en el sistema~~.

- ¿Cuál es el propósito de `apt update` y `apt upgrade`?

El propósito de `apt update` es actualizar la lista de fuentes de repositorios remotos del sistema. Permite saber si los paquetes instalados en el sisema se encuentran actualizados o precisan de una actualización. **No modifica los paquetes en sí mismo sino que actualiza la base de datos local de versiones.** Por su parte, el comando `apt upgrade` es el responsable de actualizar todos aquellos paquetes desactualizados.

- ¿Qué significa `which cowsay` y por qué puede ser útil?

Este comando imprime en pantalla ~~el directorio en el que se encuentra ubicado el paquete *cowsay*~~ **la ruta al ejecutable principal que se encuentra en la variable $PATH**. Esto puede ser de utilidad para confirmar el directorio en el cual se encuentra instalado ~~el paquete para acceder a todos sus archivos `.deb`~~ **el comando `cowsay`**.

- ¿Qué aprendiste sobre el directorio /etc y /var/log? ¿Qué tipo de archivos suelen encontrarse ahí?

En el directorio `/etc` se pueden encontrar todos los archivos de configuración más importantes del sistema. Mientras que en el directorio `/var/log` se encuentra el historial de registros de todo lo que sucede en el sistema. **Algunos ejemplos de este último son: `syslog`, `auth.log` y `dpkg.log`, los cuales permiten auditar eventos del sistema**.