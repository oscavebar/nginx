# Casos prácticos

## Versión instalada
Para saber que versión de nginx tenemos instalada solo tenemos que escribir el comando: **nginx -v**

![version](/imagenes/version.PNG)

## Ficheros de configuración
Los ficheros de configuraicón de nginx se encuentran en la ruta "/etc/nginx/"

![directorio](/imagenes/directorio.PNG)

Hay muchos directorios y archivos aquí pero lo que voy a tomar en cuenta es:

- **nginx.conf** que es el fichero donde se encuentra la configuración general de nginx.
- **sites-available** que es el directorio donde se almacenan los sitios virtuales y donde por defecto ya tenemos uno creado.
- **sites-enabled** que el directorio donde se almacenan los sitios que tenemos activos actualmente y donde por defecto ya tenemos uno.

## Página web por defecto

Al instalar nginx se nos crea una página web por defecto en /var/www/html y sirve para ver si funciona y se ha instalado correctamente.

![paginadefecto](/imagenes/paginadefecto.PNG)

Ahora voy a modificar la página.

![pagina1](/imagenes/pagina1.PNG)

Cuando lo guardemos, ya se habrán aplicado los cambios a la página web.

![resultado1](/imagenes/resultado1.PNG)

## Virtual Hosting

Una definición sencilla de lo que es el balanceo de carga sería la siguiente:
El balanceo de carga es la manera en que las peticiones de Internet son distribuídas sobre una fila de servidores.

### Preparación

Para realizar un ejemplo usaré el servidor que he creado para el ejemplo anterios tal como lo he dejado, otro servidor nginx configurado muy parecido al otro pero cambiando el contenido de la página para diferenciarlo y por último otro servidor que se encargará del balanceo de carga y configuraremos adelante.


Está es la página de mi segundo servidor:
![resultado2](/imagenes/resultado2.PNG)

### Configuración del servidor de balanceo de carga

Para la configuración del servidor de balanceo de carga instalamos nginx.
Una vez hecho esto borraremos el sitio activado por defecto  y crearemos un archivo con la ruta y el nombre indicado en la siguiente imagen.

![balanceo1](/imagenes/balanceo1.PNG)

Dentro del archivo nuevo creado tenemos que introducir lo siguiente teniendo en cuenta los siguiente puntos:
- upstream backend nos deja introducir los servidores de las páginas web a través de las ips perteneciente a la red interna. Tenemos que indicar el modo de balance que vas a utilizar, he escogido 'ip_hash' que permite persistir en la sesión.
-En el apartado de server tienes que especificar las ips de los servidores.

![balanceo1](/imagenes/loadbalancing.PNG)

### Comprobación

Para comprobar que los fichero no tienen errores de sintaxis o fallos en la configuración escribimos el comando **nginx -t**

![comprobacion](/imagenes/comprobacion.PNG)

Si aquí no hay problemas, reiniciamos el servicio de nginx con **systemctl restart nginx.servide**

Finalmente nos vamos al buscador e introducimos la ip del servidor de balanceo y nos llevará a nuestra primera página, si esperamos un poco y volvemos a cargar podremos ver que nos abre la segunda página.

![server1](/imagenes/server1.PNG)

![server2](/imagenes/server2.PNG)
