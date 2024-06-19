## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio5.PNG)

### Crear la red
```
docker network create net-wp
```

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
```
docker run --name mysql-container --network net-wp -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppassword -d mysql:8
```

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
```
docker run --name wordpress-container --network net-wp -e WORDPRESS_DB_HOST=mysql-container:3306 -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppassword -e WORDPRESS_DB_NAME=wordpress -p 9300:80 -d wordpress
```

De acuerdo con el trabajo realizado, en la el esquema de ejercicio el puerto a es **(completar con el valor)**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/4125f694-fecc-49e2-b457-372b58cfb8cf)

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/396051c5-917f-4574-9913-a896077db01e)



Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

CAPTURA DEL SITO EN DONDE SEA VISIBLE LA PUBLICACIÓN.

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/4eb2ca4a-96b8-40c4-9677-ab663ca74c1e)


### Eliminar el contenedor wordpress
```
docker rm -f wordpress-container
```

### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

### ¿Qué ha sucedido, qué puede observar?
Al eliminar y recrear el contenedor de WordPress sin persistir los datos, se pierde toda la configuración y las publicaciones. Para evitar esto, se deben utilizar volúmenes para persistir los datos de la base de datos MySQL y WordPress. Esto asegura que las configuraciones y publicaciones se mantengan intactas tras la recreación del contenedor.









