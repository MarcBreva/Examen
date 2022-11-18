# Examen 1a Evaluacion

## Indice

1. Introduccion
2. Cuerpo
3. Bibliografia
4. Conclusión

## Introduccion

En este documento MarkDown recogeremos la información y resumen de los ejercicios del examen, Ejercicio 1 es un test, Ejercicio 2 es un ejercicio de SSH, Ejercicio 3 Command line, Ejercicio 4 VirtualHost.

## Cuerpo

### Ejercicio 2 (SSH)

Primer paso nos conectamos a el sistema remoto mediante SSH, mediante este comando:

> $ ssh remote_username@remote_host

remote_host será la direccion IP o nombre de dominio al que tratamos de conectarnos.

Posteriormente salimos a la carpeta raiz utilizando el comando:

> $ cd ..

Y una vez en la carpeta raiz usamos el comando:

> $ cd /var/www

para acceder a la carpeta y en ella crearemos una carpeta con nuestro nombre propio con el comando:

> $ sudo mkdir tunombre

usaremos sudo porque necesitaremos permisos para poder crear una carpeta.

Realizado todo esto nos queda el paso final, para ello entraremos en nuestra nueva carpeta usando el comando anteriormente menciona "cd", y una vez dentro de la carpeta crearemos un archivo txt con este comando:

> $ touch ejercicio2.txt

## Ejercicio 3 (Command Line)

Para este ejercicio en el que queremos descargar una imagen en la carpeta del ejercicio anterior utilizaremos wget, una de las herramientas que mas se utliza para la descarga de archivos.

Su utlizacion es bien sencilla, partimos de la base de instalarlo con el comando:

> $ sudo apt install wget

Aqui tenemos varias opciones para instalarlo, en este caso utilizaremos un comando para guardar el fichero con el nombre que nosotros queramos:

> $ sudo wget -O nombre-fichero URL-del-archivo-a-descargar

Para finalizar podemos hacer usar el comando "ls" en nuestra carpeta y ver si tenemos el archivo deseado.

## Ejercicio 4 (Virtual Host)

Para este ejercicio será necesario tener instalado Apache, si aún no lo has hecho puedes instalar Apache mediante el paquete apt:

> $ sudo apt update
> $ sudo apt install apache2

**Primer paso, crear la estructura de directorios:**

Por ejemplo, para nuestros sitios crearemos nuestros directorios como se muestra a continuación. Si usa dominios reales o valores alternativos, cambie el texto resaltado por estos:

> $ sudo mkdir -p /var/www/example.com/public_html
> $ sudo mkdir -p /var/www/test.com/public_html

**Paso dos, conceder permisos:**

Ahora tenemos la estructura de directorio para nuestros archivos, pero son propiedad de nuestro usuario root. Si queremos que nuestro usuario regular pueda modificar archivos en nuestros directorios web, podemos cambiar la propiedad haciendo esto:

> $ sudo chown -R $USER:$USER /var/www/example.com/public_html
> $ sudo chown -R $USER:$USER /var/www/test.com/public_html

La variable $USER llevará el valor del usuario con el que se inició sesión.

Modificaremos permisos para garantizar que se permita el acceso de lectura al directorio web general:

> $ sudo chmod -R 755 /var/www

**Paso tres, Crear la página de demostración para el host virtual**

Con esto, tendremos lista nuestra estructura de directorios. Crearemos contenido para presentarlo.

Con fines demostrativos, haremos una página index.html para cada sitio.

Comencemos con example.com. Podemos abrir un archivo index.html en un editor de texto. En este caso usaremos nano:

> $ nano /var/www/example.com/public_html/index.html

**Paso 4, Crear nuevos archivos de host virtual**

comenzamos copiando el archivo para el primer dominio:

> $ sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/example.com.conf

Abra el nuevo archivo en su editor con privilegios root:

> $ sudo nano /etc/apache2/sites-available/example.com.conf

Se abrira un archivo y primero, debemos cambiar la directiva ServerAdmin de modo que se incluya un correo electrónico en el cual el administrador del sitio pueda recibir correos.

> ServerAdmin admin@example.com

Tras esto, debemos añadir dos directivas. La primera, llamada ServerName, establece el dominio base que debería coincidir con la definición de este host virtual. Este será probablemente su dominio. El segundo, llamado ServerAlias, define nombres adicionales que deberían coincidir como si fuesen el nombre base. Esto es útil para hacer coincidir los hosts que definió, como www:

> ServerName example.com
> ServerAlias www.example.com

Cambiamos la ubicación del root del documento para este dominio:

> DocumentRoot /var/www/example.com/public_html

**Paso cinco, Habilitar los nuevos archivos de host virtual:**

Ahora que creamos nuestros archivos de host virtual, debemos habilitarlos. Apache incluye algunas herramientas que nos permiten hacer esto.

Usaremos la herramienta a2ensite para habilitar cada uno de nuestros sitios.

> $ sudo a2ensite example.com.conf
> $ sudo a2ensite test.com.conf

Deshabilite el sitio predeterminado definido en 000-default.conf:

> $ sudo a2dissite 000-default.conf

Cuando termine, deberá reiniciar Apache para que estos cambios surtan efecto y usar systemctl status para verificar que el reinicio se haya realizado correctamente.

> sudo systemctl restart apache2
> sudo systemctl status apache2

**Paso seis: Configurar el archivo de hosts locales**

Si no ha usado nombres de dominios reales que sean de su propiedad para probar este procedimiento y ha usado algunos dominios de ejemplo, puede al menos probar la funcionalidad de este proceso modificando temporalmente el archivo hosts en su equipo local.

> $ sudo nano /etc/hosts

Usando los dominios que se utilizan en esta guía, y sustituyendo el IP de su servidor por el texto your_server_IP, su archivo deberá tener este aspecto:

> 127.0.0.1   localhost
> 127.0.1.1   guest-desktop
> your_server_IP example.com
> your_server_IP test.com

**Paso siete: Probar sus resultados**

Toca probarlo dirigiéndose a los dominios que establecimos en el navegador web:

> http://ejemplo.com

## Bibliografia

[VirtualHost](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-18-04-es)
[Descargar Archivos](https://www.ochobitshacenunbyte.com/2020/11/06/descarga-de-archivos-en-linux-desde-la-linea-de-comandos/)
[SSH](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server-es)

## Conclusión

Un examen completo donde hemos visto todo lo que hemos ido dando a lo largo del trimestre, bastante completo y separado en varios ejercicios diferentes donde se han puesto a prueba los conocimientos aprendidos.













