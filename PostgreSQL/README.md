# Curso de PostgreSQL

<p align="center">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postgresql/postgresql-original.svg" width="230px">
</p>

## Módulo 1: Introducción a PostgreSQL

### Instalación de MySQL

`sudo apt install postgresql postgresql-contrib`

### Introducción

PostgreSQL utiliza un rol de usuario para gestionar las conexiones. Por defecto, el nombre del rol es el mismo que el nombre de usuario de tu sistema. Para acceder a la consola de PostgreSQL, sigue estos pasos:

**Cambiar usuario:** 

`sudo -i -u postgres`

**Abrir la consola de PostgreSQL:** 

`psql`

**Para salir de la consola:** 

`p\q`

**Crear un nuevo rol (usuario):**

```sql
CREATE USER nombre_usuario WITH PASSWORD 'contraseña';
```

**Crear una nueva base de datos:**

```sql
CREATE DATABASE nombre_base_datos;
```

**Conceder permisos al usuario para esa base de datos::**

```sql
GRANT ALL PRIVILEGES ON DATABASE nombre_base_datos TO nombre_usuario;
```

## Módulo 2: Creación de Bases de Datos y Tablas

**Crear una base de datos:**

```sql
CREATE DATABASE nombre_base_datos;
```

**Crear una tabla:**

```sql
CREATE TABLE nombre_tabla (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT
);
```
