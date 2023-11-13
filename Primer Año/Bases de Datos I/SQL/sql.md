# Bases de datos

Es cualquier cosa que agrupe información con algún sentido.

En términos de informática nos sirve para acceder a información desde nuestra computadora o desde un programa.

Para poder acceder a una base de datos se debe usar un software gestor de base de datos (SGBD). El objetivo de este tipo de programas es el de encargarse de realizar operaciones sobre una BD, asegurando la fiabilidad de los datos y consistencia en las operaciones.

# SQL

La información suele ser almacenada en forma de tablas

| id  | email               | contraseña |
| --- | ------------------- | ---------- |
| 1   | juanperez@gmail.com | 1234       |
| 2   | pedro@gmail.com     | 1111       |

Una base de datos puede tener varias tablas, que generalmente contienen registros de un tipo. *Ej: "USUARIOS","PRODUCTOS","CIUDADES",etc*

## DDL

Por sus siglas, Database Definition Language, es el conjunto de instrucciones que nos permiten crear y definir tablas dentro de una base de datos.

```sql
CREATE DATABASE db_unq;

CREATE TABLE universidades(
    tag VARCHAR(10)
    nombre VARCHAR(255),
    localidad VARCHAR(255),
    fecha_creacion DATE,
    PRIMARY KEY (tag)
);

CREATE TABLE alumnos (
    dni int, 
    nombre VARCHAR(255),
    apellido VARCHAR(255),
    email VARCHAR(255),
    universidad VARCHAR(255),
    PRIMARY KEY (dni),
    FOREIGN KEY (universidad) REFERENCES universidades(tag)
);
```

## DML

Por sus siglas, Database Manipulation Language, permite alterar los datos dentro de la base de datos, empleando operaciones de CRUD

```sql
INSERT INTO universidades VALUES 
    ("UNQ", "Universidad Nacional de Quilmes", "Bernal", 2022-7-13),
    ("UNLP", "Universidad Nacional de La Plata", "La Plata", 1800-3-20);

INSERT INTO alumnos VALUES 
    (12345678, "Federico", "Gomez", "myemail@gmail.com", "UNQ"), 
    (87654321, "Juan", "Gonzalez", "juang@gmail.com", "UNLP");

UPDATE universidades SET fecha_creacion = 1975-5-10 WHERE tag="UNQ";
```

```sql
SELECT * FROM universidades;
```

| Universidades |                                  |             |                  |
| ------------- | -------------------------------- | ----------- | ---------------- |
| *tag*         | *nombre*                         | *localidad* | *fecha_creacion* |
| UNQ           | Universidad Nacional de Quilmes  | Bernal      | 1975-5-10        |
| UNLP          | Universidad Nacional de La Plata | La Plata    | 1800-3-20        |

```sql
SELECT * FROM alumnos;
```

| Alumnos  |          |            |                   |             |
| -------- | -------- | ---------- | ----------------- | ----------- |
| *dni*    | *nombre* | *apellido* | *email*           | universidad |
| 12345678 | Federico | Gomez      | myemail@gmail.com | UNQ         |
| 87654321 | Juan     | Gonzalez   | juang@gmail.com   | UNLP        |

## Condiciones

Dada una cláusula WHERE podemos establecer condiciones a nuras queries de selección de datos. Su estructura es "... WHERE (condición)"

Estas condiciones se pueden agrupar para lograr una query más específica. Un ejemplo sería

```sql
SELECT nombre FROM Alumnos WHERE universidad = "UNQ" AND email LIKE "%@gmail.com";
```

## Joins

Permiten ejecutar queries relacionando datos de más de una tabla. Existen varios tipos de uniones:

- LEFT JOIN: Busca todos los registros de la tabla de la izquierda que se relacionen con los de la tabla de la derecha. TRAE TODOS LOS REGISTROS DE LA TABLA DE LA IZQ

```sql
SELECT us.nombre, un.tag FROM usuarios AS us 
LEFT JOIN universidades AS un ON us.universidad = un.tag
-- Selecciona todos los nombres independientemente si la universidad tiene un tag o no
```

- RIGHT JOIN: Busca todos los registros de la tabla de la derecha que se relacionen con los de la tabla de la izq. TRAE TODOS LOS REGISTROS DE LA TABLA DE LA DER

```sql
SELECT us.nombre, un.tag FROM usuarios AS us 
RIGHT JOIN universidades AS un ON us.universidad = un.tag
-- Selecciona todos los tags independientemente que tengan usuario o no
```

- INNER JOIN: Trae la intersección entre las tablas, es decir todos los registros de la tabla A que se relacionen con los de la B

- CROSS JOIN o Producto cartesiano: Trae todas las combinaciones posibles entre las tablas. Hay que tener en cuenta que devuelve MUCHOS registros como resultado

### Instrucciones adicionales

- GROUP BY: Agrupa elementos en base a un campo

```sql
SELECT count(dni), universidad FROM Alumnos GROUP BY universidad 
-- Devuelve la cantidad de registros con dni por universidad
-- (1,UNQ);(1,UNLP)
```

- HAVING: devuelve las tuplas que tengan 


# Actividades de ejemplo

**Centro de Lavado y Planchado**

Dados los siguientes esquemas:

```
EMPLEADO(apodo PK, edad, telefono)

LAVARROPAS(codLavarropas PK, marca, origen, val_defecto, capacidad, id_sucursal FK)

PLANCHA(cod_plancha PK, fabricante, id_sucursal FK)

TURNO(fecha PK, plancha_id PK FK, apodo PK FK, horas)

SUCURSAL(id_sucursal PK, barrio)
```

(a) Obtener todos los (cod_plancha, fabricante) de las planchas instaladas en sucursales que no tengan lavarropas ESPañoles.

```sql
SELECT p.cod_plancha, p.fabricante FROM Plancha AS p
JOIN Lavarropas AS l ON p.id_sucursal = l.id_sucursal
WHERE l.origen != 'ESP' 
```

(b) Obtener todos los (cod_lavarropas, marca) de los lavarropas fabricados en BRA o que en la sucursal donde está instalado trabaje el empleado “johnny”

```sql
SELECT l.cod_lavarropas, l.marca FROM Lavarropas AS l
JOIN Sucursal AS s ON s.id_sucursal = l.id_sucursal,
JOIN Turno AS t ON t.
WHERE l.origen = 'BRA' OR t.apodo = 'Jhonny'
```

(c) Obtener la (id_sucursal, cantidad) de lavarropas por sucursal.

```sql

```

(d) Obtener el promedio de horas trabajadas por empleado, de aquellos empleados que trabajan en sucursales que tienen lavarropas con capacidad de más de 20 kg y cuyo promedio de horas trabajadas sea mayor a 5.

```sql

```

(e) Obtener los empleados que trabajaron solamente con planchas del fabricante “Atma”.

```sql

```

