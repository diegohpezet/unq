# Memoria y Caché

1. La biblioteca de la escuela de magia Howards está en una habitación secreta donde acceden la profesora Hooch solo cuando alguna persona necesita estudiar alg´un hechizo. Adem´as de que acceder a esa habitacion le lleva mucha energıa maagica, estos libros son tan especiales que no pueden retirarse de esa habitacion. Entonces Hooch hace una copia de las paginas que le han pedido antes de salir de ahi.

   a. Suponer que Hermione va el lunes a buscar el primer hechizo del libro monstruoso de los monstruos, y el martes vuelve en busqueda del segundo hechizo del mismo libro, ¿cuantas veces la profesora Hooch entra a la habitacion secreta?

   - La profesora Hooch entra 2 veces a la habitación secreta

   b. Suponer que el mi´ercoles Harry pide el hechizos de la pagina 3 del mismo libro, ¿como puede Hooch ahorrar su energıa magica?

   - Puede hacerlo dejando el libro a mano

   c. La profesora McGonnagal la autoriza a Hooch a hacer copias de los libros completos que les han pedido para tenerlos en su escritorio y que puedan leerlos allı. Si ella lo hiciera, ¿qu´e libros tendrıa en su oficina?

   - Tendría el libro monstruoso de los monstruos

2. Dada la documentacion de la rutina cantElementos implementada en la guia 9:

```
Requiere: Un arreglo de valores almacenados en BSS(16) a partir de la celda indicada en R0 y que finaliza con el primer elemento cuyo valor es 0x0000

Modifica: ??

Retorna: En R6 la cantidad de elementos del arreglo
```

```js
cantElementos: MOV R6, 0x0000   0001 100100 000000 0000 0000 0000 0000

repetir: CMP [[R0]], 0x0000     0110 110000 000000 0000 0000 0000 0000
         JE fin                 0001 fin
         ADD R0, 0x0001         0010 100000 000000 0000 0000 0000 0001
         ADD R6, 0x0001         0010 100100 000000 0000 0000 0000 0001
         JMP repetir            1010 repetir

fin: RET                        1100
```

a. Ensamblar la rutina y cargarla a partir de la celda A003

```
A003 |1900| cantElementos
A004 |0000|
A005 |6C00| repetir
A006 |0000|
A007 |1000|
A008 |A00F|
A009 |2800|
A00A |0001|
A00B |2900|
A00C |0001|
A00D |A---|
A00E |A005|
A00F |C000| fin
```

b. Hacer un listado de accesos a memoria que se producen en

| Etapa                         | Bus de Ctrl | Bus de dir | Bus de datos |
| ----------------------------- | ----------- | ---------- | ------------ |
| Busq de instruccion           | R/W=1       | A003       | 1900         |
| Busq de operandos             | R/W=1       | A004       | 0000         |
| Alm. de resultados            | R/W=0       | R6         | 0000         |
| Busq de instruccion (repetir) | R/W=1       | A005       | 6C00         |
| Busq de operandos             | R/W=1       | B000       | F102         |
| Busq de operandos             | R/W=1       | A006       | 0000         |
| Busq de instruccion           | R/W=1       | A009       | 2800         |
| Busq de operandos             | R/W=1       | A00A       | 0001         |
| Alm de resultados             | R/W=0       | R0         | 0001         |
| Busq de instruccion           | R/W=1       | A00B       | 2900         |
| Busq de operandos             | R/W=1       | A00C       | 0001         |
| Alm de resultados             | R/W=0       | R6         | 0001         |
| Busq de instruccion           | R/W=1       | A00D       | A000         |
| Busq de operandos             | R/W=1       | A00E       | A005         |
| Busq de instruccion(repetir)  | R/W=1       | A005       | 6C00         |
| Busq de operandos             | R/W=1       | B001       | A000         |
| Busq de operandos             | R/W=1       | A006       | 0000         |
| Busq de instruccion           | R/W=1       | A009       | 2800         |
| Busq de operandos             | R/W=1       | A00A       | 0001         |
| Alm de resultados             | R/W=0       | R0         | 0001         |
| Busq de instruccion           | R/W=1       | A00B       | 2900         |
| Busq de operandos             | R/W=1       | A00C       | 0001         |
| Alm de resultados             | R/W=0       | R6         | 0001         |
| Busq de instruccion           | R/W=1       | A00D       | A000         |
| Busq de operandos             | R/W=1       | A00E       | A005         |
|                               |             |            |              |
|                               |             |            |              |
|                               |             |            |              |
|                               |             |            |              |
|                               |             |            |              |
|                               |             |            |              |

## Correspondencia Asociativa

3.  Usando una memoria cache de 4 lineas y 4 celdas por bloque, calcular los aciertos y fallos provocados por la ejecucion de la rutina del ejercicio 2 (considerar la lista de accesos).

| dir(hexa) | dir(binario) | tag | linea | F/A |
| --------- | ------------ | --- | ----- | --- |
|           |              |     |       |     |

4.  Suponer una memoria principal de 32 celdas de un byte y una memoria caché con 4 lineas y capacidad de almacenar un bloque de 4 celdas en cada linea.

    (a) ¿Cuantos bloques tiene la memoria principal?

    - 32 bloques en memoria principal.Se pueden almacenar 4 celdas en cada linea. Hay 4 lineas. Entonces: $\dfrac{32}{4}$ = $\dfrac{2^5}{2^2}$ = $2^3$ = 8

    (b) ¿Que tamaño tiene el tag?

    - Se usan 3 bits para el tag

    (c) ¿Que capacidad total de datos debe tener la caché?

    - Cada dato se conforma de 5 bits, 3 para el tag y 2 para el indice. Sabiendo esto, la cache debe tener $(5*4)*4 = 80$ bits

5.  Suponer una memoria principal con direcciones de 16 bits y una memoria cache con 256 lineas y capacidad de almacenar un bloque de 4 celdas en cada linea. Si la CPU pide la lectura de la celda FA32, ¿Que tag se debe buscar en la cache?

    - **Forma intuitiva**: Sabiendo que hay 4 celdas por bloque y que para referenciar 4 celdas solo se requieren 2 bit, el tag son los 14 restantes
    - **Fórmula**: $\dfrac{2^16}{2^2}$ = $2^14$

6.  Suponer una memoria caché que tiene el siguiente contenido:
 <table>
      <tr>
         <td>345</td>
         <td>00112233445566778899AABBCCDDEEFF</td>
      </tr>
      <tr>
         <td>345</td>
         <td>FFEEDDCCBBAA99887766554433221100</td>
      </tr>
      <tr>
         <td>345</td>
         <td>00112233445566778899AABBCCDDEEFF</td>
      </tr>
      <tr>
         <td>345</td>
         <td>FFEEDDCCBBAA99887766554433221100</td>
      </tr>
<table>

a. Si las direcciones de memoria tienen 16 bits y el tag es de 12 bits entonces hay 4 bits que se usan para distinguir la palabra/índice. ¿Cuántas celdas entran en un bloque?

   4 celdas de índice pueden referenciar 16 celdas (2<sup>4</sup>)

b. ¿Está cacheada la celda 3451?

   Sí, está cacheado

c. ¿Qué valor retorna la caché para esa celda?

   Retorna: 44556677

7.  El chip 80286 (fabricado entre 1982 y 1993) tenıa un bus de datos de 16 bits, pero un bus de direcciones de 24 bits, lo que lo hacıa la primera arquitectura de Intel capaz de soportar 16Mb de RAM. Suponer la siguiente memoria cache, adaptada a dicha arquitectura:

(a) 32 celdas por bloque

(b) 256 lineas

(c) correspondencia asociativa

**Determinar**:

a. ¿Como se divide una direccion de memorıa en tag y palabra?

- $\dfrac{2^{24}}{2^{8}}$ = $2^{16}$. La dirección de 24 bits se divide usando 16 para el tag y 8 para el indice

b. ¿Como se decide si la direccion FAFAFA esta en cache?

- ???

c. ¿Cuantas celdas contiene dicha memoria cache?

- cantCeldasPorBloque _ cantLineas = $32 _ 256 = 8192$ celdas

## Correspondencia Directa

Para los ejercicios de esta seccion se asume que las memorias cache tienen correspondencia directa

8. Suponiendo una memoria cache de 4 lineas y 4 celdas por bloque, calcular aciertos y fallos en el escenario del ejercicio 2.

```js
A003  cantElementos: MOV R6, 0x0000   0001 100100 000000 0000 0000 0000 0000

repetir: CMP [R0], 0x0000     0110 110000 000000 0000 0000 0000 0000
         JE fin                 0001 fin
         ADD R0, 0x0001         0010 100000 000000 0000 0000 0000 0001
         ADD R6, 0x0001         0010 100100 000000 0000 0000 0000 0001
         JMP repetir            1010 repetir

fin: RET                        1100
```

```
A003 |1900| cantElementos
A004 |0000|
A005 |6C00| repetir
A006 |0000|
A007 |1000|
A008 |A00F|
A009 |2800|
A00A |0001|
A00B |2900|
A00C |0001|
A00D |A000|
A00E |A005|
A00F |C000| fin
```

| dir(hexa) | dir(binario)        | tag | linea | indice | Contenido | F/A | R/W |
| --------- | ------------------- | --- | ----- | ------ | --------- | --- | --- |
| A003      | 1010 0000 0000 0011 | A00 | 00    | 11     | 1900      | F   | 1   |
| A004      | 1010 0000 0000 0100 | A00 | 01    | 00     | 0000      | F   | 1   |
| A005      | 1010 0000 0000 0101 | A00 | 01    | 01     | 6C00      | A   | 1   |
|           |                     |     |       |        |           |     |     |
| A006      | 1010 0000 0000 0110 | A00 | 01    | 10     | 0000      | A   | 1   |
| B000      | 1011 0000 0000 0000 | B00 | 00    | 00     | F102      | F   | 1   |
| A009      | 1010 0000 0000 1001 | A00 | 10    | 01     | 2800      | F   | 1   |
| A00A      | 1010 0000 0000 1010 | A00 | 10    | 10     | 0001      | A   | 1   |
| A00B      | 1010 0000 0000 1011 | A00 | 10    | 11     | 2900      | A   | 1   |
| A00C      | 1010 0000 0000 1100 | A00 | 11    | 00     | 0001      | F   | 1   |
| A00D      | 1010 0000 0000 1101 | A00 | 11    | 01     | A000      | A   | 1   |
| A00E      | 1010 0000 0000 1110 | A00 | 11    | 10     | A005      | A   | 1   |
| A005      | 1010 0000 0000 0101 | A00 | 01    | 01     | 6C00      | A   | 1   |
| A006      | 1010 0000 0000 0110 | A00 | 01    | 10     | 0000      | A   | 1   |
| B001      | 1011 0000 0000 0001 | B00 | 00    | 01     | A000      | A   | 1   |
| A009      | 1010 0000 0000 1001 | A00 | 10    | 01     | 2800      | A   | 1   |
| A00A      | 1010 0000 0000 1010 | A00 | 10    | 10     | 0001      | A   | 1   |
| A00B      | 1010 0000 0000 1011 | A00 | 10    | 11     | 2900      | A   | 1   |
| A00C      | 1010 0000 0000 1100 | A00 | 11    | 00     | 0001      | A   | 1   |
| A00D      | 1010 0000 0000 1101 | A00 | 11    | 01     | A000      | A   | 1   |
| A005      | 1010 0000 0000 0101 | A00 | 01    | 01     | 6C00      | A   | 1   |
| A006      | 1010 0000 0000 0110 | A00 | 01    | 10     | 0000      | A   | 1   |
| B002      | 1011 0000 0000 0010 | B00 | 00    | 10     | A893      | A   | 1   |
| A009      | 1010 0000 0000 1001 | A00 | 10    | 01     | 2800      | A   | 1   |
| A00A      | 1010 0000 0000 1010 | A00 | 10    | 10     | 0001      | A   | 1   |
| A00B      | 1010 0000 0000 1011 | A00 | 10    | 11     | 2900      | A   | 1   |
| A00C      | 1010 0000 0000 1100 | A00 | 11    | 00     | 0001      | A   | 1   |
| A00D      | 1010 0000 0000 1101 | A00 | 11    | 01     | A000      | A   | 1   |
| A00E      | 1010 0000 0000 1110 | A00 | 11    | 10     | A005      | A   | 1   |
| A005      | 1010 0000 0000 0101 | A00 | 01    | 01     | 6C00      | A   | 1   |
| A006      | 1010 0000 0000 0110 | A00 | 01    | 10     | 0000      | A   | 1   |
| B003      | 1011 0000 0000 0011 | B00 | 00    | 11     | 0000      | A   | 1   |
| A007      | 1010 0000 0000 0111 | A00 | 01    | 11     | 1000      | A   | 1   |
| A008      | 1010 0000 0000 1000 | A00 | 10    | 00     | A00F      | A   | 1   |
| A00F      | 1010 0000 0000 1111 | A00 | 11    | 11     | C000      | A   | 1   |

9.  Considerar una computadora con una memoria de 64 celdas de un byte y una memoria cache con 4 lineas y bloques de 8 celdas por linea.

$\dfrac{celdas}{celdasPorBloque} = \dfrac{64}{8} = 4$ bloques por línea

(a) Que tamaño tienen las direcciones de esta memoria?

- Siendo que hay 64 celdas se requieren 6 bits para representar las direcciones ($2^6$)

(b) ¿Cuantos bits de una direccion se destinan a: tag, linea y palabra?

- Se le asignan 1 bit de tag, 3 de linea y 2 de palabra.

(c) Explicar lo anterior usando una direccion como ejemplo.

- Suponer que se pide la dirección 0110001. El tag es 0, la linea es 110 y se busca el elemento en la posición 01 del bloque
    
10. Considerando el escenario del ejercicio 9, mencionar el tag y la linea de la cache a la que corresponde cada dirección:

| dir    | tag | nroLinea |
| ------ | --- | -------- |
| 111000 | 1   | 110      |
| 011001 | 0   | 110      |
| 111111 | 1   | 111      |
| 101000 | 1   | 010      |
| 101001 | 1   | 010      |

11.  Considerando el escenario del ejercicio 9, listar todas las direcciones en la misma línea que la direccion 111000.

- Las direcciones son 111000, 111001, 111010, 111011, 111100, 111101, 111110, 111111

12. Suponer que la cache descripta en el ejercicio 9 esta vacia, y que se realizan lecturas de direcciones en el siguiente orden. Determinar para cada lectura si esta produjo un fallo o un acierto.

13. ¿Como se divide una direccion de memoria de 16 bits en tag, linea y palabra si la memoria cache contiene 4 celdas por bloque y 256 lineas? ¿Como se decide si la direccion FA32 esta en cache?

## Correspondencia asociativa por conjuntos

Esta correspondencia combina aspectos de las dos anteriores. Las lineas se agrupan en conjuntos para corresponder de manera directa cada bloque de memoria principal con un conjunto dentro de la cache, y dentro de cada conjunto los bloques se almacenan con un criterio asociativo. Dicho de otra forma, las celdas de memoria tendran un unico conjunto en el que pueden almacenarse y dentro de ese conjunto, pueden ir a cualquier lınea.

14. Cuantos bits de una direccion se destinan a: tag, conjunto y palabra en el siguiente esquema:

- Una memoria principal de 32 celdas de un byte
- Una memoria cache con:
  - Bloques de 4 celdas
  - 4 lineas
  - Correspondencia asociativa por conjuntos de 2 lineas

| Dir | Dato                                |
| --- | ----------------------------------- |
| 00  | 01010101 01010101 01010101 01010101 |
| 01  | 01010101 01010101 01010101 01010101 |
| 10  | 01010101 01010101 01010101 01010101 |
| 11  | 01010101 01010101 01010101 01010101 |

## Performance de la caché

15. Se tiene un sistema con una memoria principal con
un tiempo de acceso de 3s, y una memoria cache
cuyo tiempo de acceso es de 0,3s y cuya tasa de
aciertos es del 90%. ¿Cuanto tiempo se tarda en
leer 2000 celdas?

T<sub>total</sub> = T<sub>cache</sub> + (1-Tasa de aciertos) * T<sub>principal</sub>

$T = 0,3s + (1 - 0.9) * 3s$ <br> $T = 0.6s$

16.  Suponer los fallos y aciertos de programa que se
analizo en el ejercicio 3, y considerando que la
cache tiene tiempo de acceso es de 0,2s, la memoria
principal tiene un tiempo de acceso de 2s y que es
despreciable el tiempo de CPU, ¿cuanto tarda en
ejecutarse el programa?

17.  Suponer los fallos y aciertos de programa que se
analizo en el ejercicio 8, y considerando que la
cache tiene tiempo de acceso es de 0,2s, la memoria
principal tiene un tiempo de acceso de 2s y que es
despreciable el tiempo de CPU, ¿cu´anto tarda en
ejecutarse el programa?

