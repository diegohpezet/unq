# Ejercicio de conexion

Rehacer ejercicio 3 con politica de reemplazo LRU

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

```js
cantElementos: MOV R6, 0x0000   0001 100100 000000 0000 0000 0000 0000

repetir: CMP [R0], 0x0000       0110 110000 000000 0000 0000 0000 0000
         JE fin                 0001 fin
         ADD R0, 0x0001         0010 100000 000000 0000 0000 0000 0001
         ADD R6, 0x0001         0010 100100 000000 0000 0000 0000 0001
         JMP repetir            1010 repetir

fin: RET                        1100
```

<center>

| dir(hexa) | dir(binario)        | tag | linea | indice | F/A |
| --------- | ------------------- | --- | ----- | ------ | --- |
| A003      | 1010 0000 0000 0011 | A00 | 00    | 11     | F   |
| A004      | 1010 0000 0000 0100 | A00 | 01    | 00     | F   |
| A005      | 1010 0000 0000 0101 | A00 | 01    | 01     | A   |
| A006      | 1010 0000 0000 0110 | A00 | 01    | 10     | A   |
| B000      | 1011 0000 0000 0000 | B00 | 00    | 00     | F   |
| A008      | 1010 0000 0000 1000 | A00 | 10    | 00     | F   |
| A009      | 1010 0000 0000 1001 | A00 | 10    | 01     | A   |
| A00A      | 1010 0000 0000 1010 | A00 | 10    | 10     | A   |
| A00B      | 1010 0000 0000 1011 | A00 | 10    | 11     | A   |
| A00C      | 1010 0000 0000 1100 | A00 | 11    | 00     | F   |
| A00D      | 1010 0000 0000 1101 | A00 | 11    | 01     | A   |
| A005      | 1010 0000 0000 0101 | A00 | 01    | 01     | A   |
| A006      | 1010 0000 0000 0110 | A00 | 01    | 10     | A   |
| B001      | 1011 0000 0000 0001 | B00 | 00    | 01     | A   |
| A008      | 1010 0000 0000 1000 | A00 | 10    | 00     | A   |
| A009      | 1010 0000 0000 1001 | A00 | 10    | 01     | A   |
| A00A      | 1010 0000 0000 1010 | A00 | 10    | 10     | A   |
| A00B      | 1010 0000 0000 1011 | A00 | 10    | 11     | A   |
| A00C      | 1010 0000 0000 1100 | A00 | 11    | 00     | A   |
| A00D      | 1010 0000 0000 1101 | A00 | 11    | 01     | A   |
| A005      | 1010 0000 0000 0101 | A00 | 01    | 01     | A   |
| A006      | 1010 0000 0000 0110 | A00 | 01    | 10     | A   |
| B002      | 1011 0000 0000 0010 | B00 | 00    | 10     | A   |

</center>

## Performance

Se tiene:

- Mem principal con tiempo de acceso 3s
- Mem cache con
  - Tiempo de acceso de 0,3s
  - Tasa de aciertos 90%
  - Politica de escritura _Write Through_

¿Cuanto tiempo lleva ejecutar una rutina que ocasiona 2000 lecturas y 300 escrituras?

$$
\begin{align*}
CantAciertos = 2000 * 0.9 1800 \\
CantFallosLectura = 2000 * 0.1 = 200 \\
\\
TiempoTotal = (200 + 300) * (0,3 + 3) + (1800*0,3) \\
TiempoTotal = 500 * 3,3 + 540 \\
TiempoTotal = 1650 + 540 \\
TiempoTotal = 2190 \\
\end{align*}
$$
