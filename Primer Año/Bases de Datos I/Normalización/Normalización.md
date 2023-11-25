# Normalización

Refiere al proceso de simplificación (**sin perder información**) de los datos. Busca:

- Tener almacenado con el menor espacio posible
- Eliminar datos repetidos
- Eliminar errores
- Datos ordenados

## Dependencias

"B no tendría razón de ser sin A". Ej: Un usuario no tiene sentido sin su id

- Dependencia funcional: Atributos que dependen funcionalmente de otro
  - A <- B <-C
- Dependencia Transitiva: B depende de A, y C no depende de A pero depende de B
  - A <- B ^ B <- C

## Formas normales

Base de datos no normalizada:
(Existe repetición de datos)

| <u>Matricula</u> | Nombre | Dirección |  Teléfono  | Materia | <u>NumMateria</u> | Carrera  |
| :--------------: | :----: | :-------: | :--------: | :-----: | :---------------: | :------: |
|        1         | Sergio | Puebla 22 | 5656565656 |   BD    |        123        | Sistemas |
|        1         | Sergio | Puebla 22 | 5656565656 |  Prog   |        234        | Sistemas |
|        2         |  Ana   | Reforma 1 | 2323232323 |   BD    |        123        | Sistemas |

- **1 Forma Normal**: Trata de identificar grupos de repetición.
<center>

| <u>Matricula</u> | Nombre | Dirección |  Teléfono  | Carrera  |
| :--------------: | :----: | :-------: | :--------: | :------: |
|        1         | Sergio | Puebla 22 | 5656565656 | Sistemas |
|        2         |  Ana   | Reforma 1 | 2323232323 | Sistemas |

| <u>Matricula</u> | Materia | <u>NumMateria</u> |
| :--------------: | :-----: | :---------------: |
|        1         |   BD    |        123        |
|        1         |  Prog   |        234        |
|        2         |   BD    |        123        |

</center>
<hr>

- **2 Forma Normal**: Identifica Dependencias funcionales, separando entonces los "elementos" que conforman en otras tablas

<center>

| <u>Matricula</u> | Nombre | Dirección |  Teléfono  | Carrera  |
| :--------------: | :----: | :-------: | :--------: | :------: |
|        1         | Sergio | Puebla 22 | 5656565656 | Sistemas |
|        2         |  Ana   | Reforma 1 | 2323232323 | Sistemas |

| Materia | <u>NumMateria</u> |
| :-----: | :---------------: |
|   BD    |        123        |
|  Prog   |        234        |
|   BD    |        123        |

| <u>Matricula</u> | <u>NumMateria</u> |
| :--------------: | :---------------: |
|        1         |        123        |
|        1         |        234        |
|        2         |        123        |

</center>
<hr />

- **3 Forma Normal**: Identifica dependencias transitivas. En este caso Carrera depende de nombre, y nombre depnde de matrícula.

<center>

| <u>Matricula</u> | Nombre | Dirección |  Teléfono  | NroCarrera (FK) |
| :--------------: | :----: | :-------: | :--------: | :-------------: |
|        1         | Sergio | Puebla 22 | 5656565656 |      1234       |
|        2         |  Ana   | Reforma 1 | 2323232323 |      1234       |

| <u>NroCarrera</u> | Carrera  |
| :---------------: | :------: |
|       1234        | Sistemas |
|       5678        | Medicina |

| Materia | <u>NumMateria</u> |
| :-----: | :---------------: |
|   BD    |        123        |
|  Prog   |        234        |
|   BD    |        123        |

| <u>Matricula</u> | <u>NumMateria</u> |
| :--------------: | :---------------: |
|        1         |        123        |
|        1         |        234        |
|        2         |        123        |

</center>
<hr />

- **4 Forma Normal**: Identifica dependencias multivaluadas
```
"Sea R un esquema de relacion formado por los atributos A,B,C, la dependencia multivaluada A->->B existe *si y solo si* el conjunto de valores de B que se obtiene para un par de valores (A,C) depende sólo del valor de A y es independiente de los valores para C
```

Nota: Si se hace un NATURAL JOIN de las relaciones resultantes se devuelve a la relación original


### Notas respecto al parcial

Van a ser 3 ejercicios

- A partir de tablas pasar a 1FN
- Simil a practica 6, dado un contexto obtener DFs para obtener 2da y 3er forma normal
- A partir de tablas en 3FN, pasar a 4FN de ser necesario

Claves candidatas = antecedentes - consecuentes + independientes
