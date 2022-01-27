Creamos el docker compose para crear 3 maquinas , 1 cliente con el enviroment de vnc, 1 servidor apache y 1 servidor dns.

Una vez levantados los 3 contenedores es necesario configurar los cname del dns  para poder acceder a la web escribiendo diferentes direcciones en el navegador, y que la máquina resuelva el nombre.

Necsario tambien configurar el servidor web con la dirección del cliente para que responda a las peticiones web

La configuracion dns es la siguiente

;
; BIND data file for local loopback interface
;
$TTL	604800
@	IN	SOA	practica.com. root.practica.com. (
			      2		; Serial
			 604800		; Refresh
			  86400		; Retry
			2419200		; Expire
			 604800 )	; Negative Cache TTL
;
@	      IN   NS	ns.practica.com.
@         IN   A   10.0.0.250
@	      IN  AAAA ::1
ns        IN   A   10.0.0.250
hola  IN   A   10.0.0.100
adios       IN CNAME hola.practica.com.

Para acceder al cliente kasm, en el navegador web local, escribimos https://127.0.0.1:6901/  y la contraseña es "password" que pusimos en el docker compose. Y accedemos al entorno del kasm.

Para abrir el index.html del virutal host escribimos en este caso hola.practica.com para acceder con el virtual host. Y se abre el index.html


CERTIFICADO SSL

-Para generar el .key y .crt lo hacemos con el comando sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /home/asir2a/Escritorio/apache-selfsigned.key -out /home/asir2a/Escritorio/apache-selfsigned.crt

-Para mover los archivos generados a la ruta de configuracion de apache utilizamos docker cp.

-Descomentar las lineas del vhosts en el httpd conf.

-Importante SSL Engine ON

-En SSL Certificate hay que cambiar el nombre de los .crt y .key a los nombres de nuestros archivos 

-Para comprobar logueamos con https://hola.practica.com y vemos que existe el certificado aunque no esté validado.



