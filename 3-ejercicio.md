### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:11.21-alpine3.17

```
docker run -d --name mi_postgres -e POSTGRES_PASSWORD=mi_contraseña --network none postgres:11.21-alpine3.17
```


### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4

Primero vamos a crear una red para luego conectarla a postgreSQL

```
docker network create mi_red_privada
```

```
docker network connect mi_red_privada mi_postgres
```


La figura presenta el esquema creado en donde los puertos son:
- a: (completar con el valor)
- b: (completar con el valor)
- c: (completar con el valor)

![Imagen](imagenes/esquema-ejercicio3.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.

COMPLETAR CON UNA CAPTURA DEL LOGIN

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/27201bf8-2c6d-485a-81b9-8b29c4fdd130)

### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.

## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info

Para esto primero nos conectaremos a postgres

```
docker exec -it mi_postgres psql -U postgres
```

Dentro de nuestra DB, vamos a crear una nueva base, llamada info

```
CREATE DATABASE info;
```

Dentro de esta, vamos a crear una tabla y a crear datos dentro de ella

```
CREATE TABLE personas (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

INSERT INTO personas (nombre) VALUES ('Donoban');
INSERT INTO personas (nombre) VALUES ('Milena');
```

### Realizar un select *from personas

Ponemos la siguiente linea de codigo para hacer la consulta

```
SELECT * FROM personas;
```

![image](https://github.com/DonobanR/2024A-ISWD633-Practica2/assets/135273301/3c60d80c-aca2-426e-beb7-3884b1294ce0)
