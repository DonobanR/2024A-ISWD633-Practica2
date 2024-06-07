# Variables de Entorno
### ¿Qué son las variables de entorno
Las variables de entorno en Docker son pares clave-valor usados para configurar aplicaciones dentro de contenedores. Se pueden definir en el Dockerfile usando ENV o al ejecutar un contenedor con -e. Permiten ajustar configuraciones como credenciales, modos de operación y parámetros específicos del entorno.

### Para crear un contenedor con variables de entorno

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

Para que se complete la ejecucion, poner al final el nombre de la imagen *nginx:alpine*

```
docker run -d --name nginx -e username=User1 -e role=admin nginx:alpine
```

# CAPTURA DE COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/62552000-da8f-4d8f-b4b2-d16ea18ff60b)


### Crear un contenedor con mysql:8 , mapear todos los puertos

Sabiendo que el puerto por defecto de MySQL es el puerto 3306, procederemos a escribir la siguinte linea de comando

````
docker run -d --name mysql-container -p 3306:3306 -p 33060:33060 -p 33061-33100:33061-33100 mysql:8
````

### ¿El contenedor se está ejecutando?
No, no se esta ejecutando, por ports que no son validos

### Identificar el problema

docker: Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:3306 -> 0.0.0.0:0: listen tcp 0.0.0.0:3306: bind: Only one usage of each socket address (protocol/network address/port) is normally permitted.


### Eliminar el contenedor creado con mysql:8 

````
docker rm mysql-container
````


### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

Previo a esto es necesario crear el archivo y colocar las variables en un archivo, **.env** se ha convertido en una convención estándar, pero también es posible usar cualquier extensión como **.txt**.
```
docker run -d --name <nombre contenedor> --env-file=<nombreArchivo>.<extensión> <nombre imagen>
```
**Considerar**
Es necesario especificar la ruta absoluta del archivo si este se encuentra en una ubicación diferente a la que estás ejecutando el comando docker run.

### Crear un contenedor con mysql:8 , mapear todos los puertos y configurar las variables de entorno mediante un archivo

Crear previamente el archivo *.txt* o *.env* en la ruta que tu desees, en mi caso, utilizare el desktop para crear mi archibo *.txt*

````
cd OneDrive\Escritorio
````

````
docker run -d --name mysql-container -p 3308:3306 -p 33061:33060 --env-file=VariablesEntorno.txt mysql:8
````

# CAPTURA DE COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/28e449b3-5a99-45bc-8965-8a0f13288d2a)


### ¿Qué bases de datos existen en el contenedor creado?

Para ver las bases de datos que existen en el contendor, primero debemos ingresar a ella, para eso procederemos a escribir la siguiente liena de comando:

````
docker exec -it mysql-container mysql -uroot -p
````

Despues segun la estructura de tu archivo *.txt* o *.env* creado anteriormente entraras a tu BD, despues de ingresar, escribe

````
SHOW DATABASES;
````

En mi caso estas bases de datos exisen en el contenedor creado

mysql> SHOW DATABASES;

| Database           |
|--------------------|
| information_schema |
| mydatabase         |
| mysql              |
| performance_schema |
| sys                |

5 rows in set (0.01 sec)
