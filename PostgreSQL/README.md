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

**Insertar Datos:**

```sql
INSERT INTO productos (nombre, precio, stock) VALUES 
('Laptop', 1200.99, 15),
('Teclado', 20.00, 100);
```

**Consultas Básicas:**

```sql
SELECT * FROM productos;
SELECT nombre, precio FROM productos WHERE stock > 10;
```

## Módulo 3: Consultas y Manipulación de Datos

### Filtrado de Datos con WHERE, AND, OR

**Uso de WHERE:** El operador WHERE se utiliza para filtrar registros que cumplen con una condición específica. Veamos un ejemplo simple:

```sql
SELECT * FROM productos
WHERE precio > 100;
```

En este caso, la consulta selecciona todos los productos cuyo precio es mayor a 100.


**Uso de AND:** El operador AND permite combinar múltiples condiciones que deben cumplirse simultáneamente. Solo se seleccionarán los registros que cumplan con ambas condiciones.

```sql
SELECT * FROM productos
WHERE precio > 100 AND stock > 10;
```

Esta consulta selecciona productos cuyo precio es mayor a 100 y que tienen un stock mayor a 10.


**Uso de OR:** El operador OR permite combinar condiciones alternativas. Los registros se seleccionarán si cumplen con al menos una de las condiciones especificadas.

```sql
SELECT * FROM productos
WHERE precio > 100 OR stock > 10;
```

Esta consulta selecciona productos cuyo precio es mayor a 100 o cuyo stock es mayor a 10. Si un producto cumple al menos una de estas condiciones, se incluirá en el resultado.


**Combinación de AND y OR:** Puedes combinar AND y OR para hacer filtros más complejos. Es importante utilizar paréntesis para agrupar condiciones y definir el orden en el que deben evaluarse.

```sql
SELECT * FROM productos
WHERE (precio > 100 OR stock > 10) AND categoria_id = 2;;
```

Esta consulta selecciona productos cuyo precio es mayor a 100 o cuyo stock es mayor a 10. Si un producto cumple al menos una de estas condiciones, se incluirá en el resultado.

En esta consulta, seleccionamos productos que:

* Tienen un precio mayor a 100 o un stock mayor a 10, y además
* Pertenecen a la categoría con categoria_id igual a 2.

**Ejemplo con mas condiciones:**

Supongamos que tenemos la siguiente tabla productos

| id | Nombre | precio | stock | categoria_id|
|----|--------|--------|-------|-------------|
| 1  | Laptop | 1200   | 5     | 2           |
| 2  | Teclado| 20     | 50    | 1           |
| 3  | Mouse  | 10     | 150   | 1           |
| 4  | Monitor| 300    | 20    | 2           |

Con esta tabla, podemos hacer una consulta avanzada:

```sql
SELECT * FROM productos
WHERE (precio > 50 AND stock < 50) OR (categoria_id = 1 AND stock > 100);
```

Esta consulta selecciona productos que:

* Tienen un precio mayor a 50 y un stock menor a 50, o
* Pertenecen a la categoría 1 y tienen un stock mayor a 100.


| id | Nombre | precio | stock | categoria_id|
|----|--------|--------|-------|-------------|
| 1  | Laptop | 1200   | 5     | 2           |
| 3  | Mouse  | 10     | 150   | 1           |

### Ordenamiento y Paginación de Resultados

**Ordenamiento con ORDER BY:** El operador ORDER BY permite ordenar los resultados de una consulta en orden ascendente (ASC) o descendente (DESC).

```sql
SELECT * FROM productos
ORDER BY precio ASC; -- Ordena por precio en orden ascendente
```

**Ejemplo:**

```sql
SELECT * FROM productos
ORDER BY precio DESC, nombre ASC;
```

En este ejemplo, los productos se ordenan primero por precio en orden descendente. Si dos productos tienen el mismo precio, se ordenan por nombre en orden ascendente.

**Paginación con LIMIT y OFFSET:** La paginación permite dividir los resultados en “páginas” para visualizar un número limitado de registros por cada consulta. Esto se hace con las cláusulas LIMIT y OFFSET.

* **LIMIT** define la cantidad de registros a mostrar.
* **OFFSET** indica el punto de inicio, es decir, el número de registros a omitir antes de comenzar a mostrar los resultados.

**Ejemplo:** Supongamos que queremos mostrar los productos en bloques de 5 registros cada uno.

**Página 1 (registros del 1 al 5):**

```sql
SELECT * FROM productos
ORDER BY precio ASC
LIMIT 5 OFFSET 0;
```

**Página 2 (registros del 6 al 10):**

```sql
SELECT * FROM productos
ORDER BY precio ASC
LIMIT 5 OFFSET 5;
```

**Página 3 (registros del 11 al 15)::**

```sql
SELECT * FROM productos
ORDER BY precio ASC
LIMIT 5 OFFSET 5;
```

### Ejemplo Completo de Ordenamiento y Paginación

Supongamos que tenemos la siguiente tabla productos

| id | Nombre   | precio | stock | categoria_id|
|----|----------|--------|-------|-------------|
|1	 | Laptop   | 1200   |	5	 | 2
|2	 | Teclado  | 20	 | 50	 | 1
|3	 | Mouse    | 10	 | 150	 | 1
|4	 | Monitor  | 300	 | 20	 | 2
|5	 | Impresora| 150	 | 30	 | 2
|6	 | Tablet	| 200	 | 15	 | 1

Si queremos ver los productos ordenados por precio de forma descendente y mostrar solo los primeros 3:

```sql
SELECT * FROM productos
ORDER BY precio DESC
LIMIT 3;
```

| id | Nombre   | precio | stock | categoria_id|
|----|----------|--------|-------|-------------|
|1	 | Laptop   | 1200   | 5	 | 2
|4	 | Monitor  | 300	 | 20	 | 2
|6	 | Tablet	|200	 | 15	 | 1

Si queremos mostrar la “segunda página” con 3 registros por página, debemos utilizar OFFSET para omitir los primeros 3:

```sql
SELECT * FROM productos
ORDER BY precio DESC
LIMIT 3 OFFSET 3;
```

| id | Nombre   | precio | stock | categoria_id|
|----|----------|--------|-------|-------------|
|5	 | Impresora| 150	 | 30	 | 2
|2	 | Teclado  | 20	 | 50	 | 1
|3	 | Mouse    | 10	 | 150	 | 1

### Actualización y Eliminación de Registros

```sql
UPDATE productos SET precio = 1100.00 WHERE nombre = 'Laptop';
DELETE FROM productos WHERE nombre = 'Teclado';
```

### Actualización y Eliminación de Registros

**Uso de Funciones de Agregación (COUNT, SUM, AVG, etc.):**

```sql
SELECT COUNT(*) AS total_productos FROM productos;
SELECT AVG(precio) AS precio_promedio FROM productos;
```

### Agrupación de Datos con GROUP BY y HAVING