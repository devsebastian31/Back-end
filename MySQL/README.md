# Curso de MySQL

<p align="center">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original.svg" width="230px">
</p>

## Módulo 1: Introducción a MySQL

### Instalación de MySQL

`sudo apt install mysql-server`

### Introducción a SQL

**Configurar MySQL:** Después de la instalación, ejecuta el siguiente comando para asegurar tu instalación de MySQL:

`sudo mysql_secure_installation`

Durante este proceso, se te pedirá que configures una contraseña para el usuario root y otras configuraciones de seguridad.


Para acceder a la consola de MySQL como el usuario root, puedes usar:

`sudo mysql -u root -p`

Se te pedirá que ingreses la contraseña que configuraste durante el proceso de instalación.

## Módulo 2: Fundamentos de SQL

### Sintaxis básica:

**Creación de Bases de Datos y Tablas:**

* Crear una base de datos:

```sql
CREATE DATABASE nombre_base_datos;
```

* Crear una tabla:

```sql
CREATE TABLE nombre_tabla (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT
);
```

## Módulo 3: Operaciones CRUD

**Insertar Datos:**

```sql
INSERT INTO nombre_tabla (nombre, edad) VALUES ('Juan', 25);
```

**Leer datos:** 

```sql
SELECT * FROM nombre_tabla;
```

**Actualizar Datos:**

```sql
UPDATE nombre_tabla SET edad = 26 WHERE nombre = 'Juan';
```

**Eliminar Datos:**

```sql
DELETE FROM nombre_tabla WHERE nombre = 'Juan';
```

### Modificación de la Estructura de Tablas.

**Agregar una Columna:**

```sql
ALTER TABLE nombre_tabla ADD columna_nueva VARCHAR(100);
```

**Modificar una Columna:**
```sql
ALTER TABLE nombre_tabla MODIFY columna_existente INT NOT NULL;
```

**Eliminar una Columna:**
```sql
ALTER TABLE nombre_tabla DROP COLUMN columna_a_eliminar;
```

**Renombrar una Columna:**
```sql
ALTER TABLE nombre_tabla CHANGE columna_antigua nuevo_nombre VARCHAR(100);
```

**Renombrar la Tabla:**
```sql
ALTER TABLE nombre_tabla RENAME TO nuevo_nombre_tabla;
```

**Agregar una Clave Primaria:**
```sql
ALTER TABLE nombre_tabla ADD PRIMARY KEY (columna_id);
```

**Eliminar una Clave Primaria:**
```sql
ALTER TABLE nombre_tabla DROP PRIMARY KEY;
```

**Agregar un Índice:**
```sql
ALTER TABLE nombre_tabla ADD INDEX idx_columna (columna);
```

**Eliminar un Índice:**
```sql
ALTER TABLE nombre_tabla DROP INDEX idx_columna;
```

## Módulo 4: Consultas Avanzadas

**Filtrado de Datos:**

```sql
SELECT * FROM nombre_tabla WHERE edad > 20;
```

**Ordenar Resultados:**

```sql
SELECT * FROM nombre_tabla ORDER BY edad DESC;
```

**Funciones de Agregación:**

```sql
SELECT COUNT(*) FROM nombre_tabla;
```

**Agrupar Resultados:**

```sql
SELECT edad, COUNT(*) FROM nombre_tabla GROUP BY edad;
```

## Módulo 5: Joins y Relaciones

**Ejemplo de Joins:**

```sql
SELECT a.nombre, b.nombre_asignatura
FROM alumnos a
JOIN asignaturas b ON a.id = b.alumno_id;
```

**Creación de Índices:**

```sql
CREATE INDEX idx_nombre ON nombre_tabla(nombre);
```

**Creación de Vistas:**

```sql
CREATE VIEW vista_alumnos AS
SELECT nombre, edad FROM nombre_tabla WHERE edad > 18;
```

**Gestión de Usuarios:**

```sql
CREATE USER 'nuevo_usuario'@'localhost' IDENTIFIED BY 'contraseña';
GRANT ALL PRIVILEGES ON nombre_base_datos.* TO 'nuevo_usuario'@'localhost';
```


## Módulo 6: Copias de Seguridad y Restauración

**Hacer Copias de Seguridad:**

```bash
mysqldump -u usuario -p nombre_base_datos > copia.sql
```

**Restaurar desde una Copia de Seguridad:**

```bash
mysql -u usuario -p nombre_base_datos < copia.sql
```


## Módulo 7: Optimización y Rendimiento

**Análisis de Consultas:**

```bash
mysqldump -u usuario -p nombre_base_datos > copia.sql
```

**Restaurar desde una Copia de Seguridad:**

```sql
EXPLAIN SELECT * FROM nombre_tabla WHERE edad > 20;
```

