Creamos el docker compose para crear 3 maquinas , 1 cliente con el enviroment de vnc, 1 servidor apache y 1 servidor dns.

Una vez levantados los 3 contenedores es necesario configurar los cname del dns  para poder acceder a la web escribiendo diferentes direcciones en el navegador, y que la máquina resuelva el nombre.

Necsario tambien configurar el servidor web con la dirección del cliente para que responda a las peticiones web