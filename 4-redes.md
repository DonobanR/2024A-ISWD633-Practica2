# Redes
Las redes son un componente fundamental que permite la comunicación entre contenedores, así como la comunicación de los contenedores con el mundo exterior. 
![Imagen](imagenes/redes.PNG)
- Bridge: Esta es la red por defecto en Docker. Permite la comunicación entre contenedores en el mismo host. Cada contenedor conectado a la red bridge tiene una IP propia en la subred de la red bridge.
    -  Brige por default: Cuando se ejecuta un contenedor, Docker crea automáticamente una red de tipo bridge por default. Esta red se utiliza para permitir la comunicación entre contenedores en el mismo host. Cada contenedor conectado a esta red obtiene su propia dirección IP en la subred de la red bridge.
    - Bridge creada por nosotros: Un usuario también puede crear sus propias redes de tipo bridge en Docker. Esto puede ser útil para organizar y segmentar los contenedores de una aplicación de manera más controlada. Al crear una red bridge personalizada, se puede especificar un rango de direcciones IP y otras configuraciones de red específicas. Los contenedores conectados a esta red utilizarán las direcciones IP de la subred definida por el usuario.
- Host: Con esta red, los contenedores comparten la red del host en lugar de tener su propia interfaz de red. Esto puede mejorar el rendimiento de red, pero los contenedores pueden entrar en conflicto con los puertos del host si intentan utilizar los mismos puertos.
- None: Con esta red, se deshabilita la configuración de red. Los contenedores que usan esta red tienen su propia red de bucle invertido y no pueden comunicarse con otros contenedores a menos que se conecten explícitamente a una red.

### Crear una red de tipo bridge

```
docker network create <nombre red> -d bridge
```

### Crear un contenedor vinculado a una red

```
docker run -d --name <nombre contenedor> --network <nombre red> <nombre imagen>
```

### Para saber a qué red está conectado un contenedor

```
docker inspect <nombre contenedor>
```
ó
```
docker network inspect <nombre red> 
```

### Vincular contenedor a una red
```
docker network connect <nombre red> <nombre contenedor>
```

### Para desvincular un contenedor de una red
```
docker network disconnect <nombre red> <nombre contenedor>
```

### Para listar las redes existentes
```
docker network ls
```

### Crear los contenedores y las redes que se presentan en el esquema. Usar para todos los contenedores la imagen de nginx:alpine

![Imagen](imagenes/esquema-ejercicio-redes.PNG)

CAPTURA DE LAS REDES EXISTENTES CREADAS

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/265a798a-c13b-47ba-b2a9-3cfe5af8ce75)


CAPTURAS(S) DE LOS CONTENEDORES CREADOS EN DONDE SE EVIDENCIE A QUÉ RED ESTÁN VINCULADOS

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/7d39ec3e-d6b8-4884-a23c-a9514abeb637)

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/562bb7b6-7b5e-4081-9e46-86f46cfbae51)

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/511d95f7-6454-4397-b959-e0077a96f27d)

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/2cfac602-070c-411e-a7d0-dbdfed09553b)

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/eff8a4d6-2c99-43b2-ba3a-4c0e3b4bdf81)



### Para eliminar las redes creadas
```
docker network rm <nombre de la red>
```

