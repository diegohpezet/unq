# Práctica Integradora 2do parcial

1. Dada una cadena que describe 4 pedidos con el formato ANNN ANNN ANNN ANNN, donde cada cuarteto de bits representa un pedido. El bit A indica el estado del pedido (si fue atendido o no), y N su nuemero de orden en BSS(3). Se necesita programar la rutina *conseguirEstadosDePedidos*, que cumple con la siguiente documentación

<table>
    <thead>
        <tr>
            <td>conseguirEstadosDePedidos</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Requiere</td>
            <td>Una cadena de 4 pedidos en el formato ANNN ANNN ANNN ANNN en la celda 11AC</td>
        </tr>
        <tr>
            <td>Modifica</td>
            <td></td>
        </tr>
        <tr>
            <td>Retorna</td>
            <td>En la celda 60B0 una cadena con los estados de los pedidos de la cadena recibida, respetando su formato y completando con 0 los números de orden</td>
        </tr>
    </tbody>
</table>

- Mediante una cadena de ejemplo, mostrar qué resultado se espera de la rutina anterior
  - Dada la cadena 1010 0110 1001 0011 se espera la cadena 1000 0000 1000 0000

- Escribir la rutina *conseguirEstadosDePedidos*, respetando la documentación (Utilizando máscaras)
  ```js
  conseguirEstadosDePedidos: AND [0x11AC], 0x8888
                             MOV [0x60B0], [0x11AC]
                             RET
  ```
- Justificar la máscara utilizada
  - Se empleó la máscara AND de conjunción ya que su funcionamiento permite conservar solo los valores "1" de las posiciones que dictamine el operando origen. Por ejemplo en este caso se optó por el operando 0x8888 (1000 1000 1000 1000), entonces solo se copiaran los valores "1" ubicados en la primera posición de cada cuarteto de bits.

2. Se cuenta con la siguiente rutina *incrementarSegunPrefijo*, la cual no debe ser implementada, y cumple la siguiente documentación

| incrementarSegunPrefijo |     |
| ----------------------- | --- |
| Requiere  | En R6 una cadena a analizar y en R5 un prefijo de 4 bits con el formato PPPP 0000 0000 0000 (tiene un rellendo de 12 ceros) |
| Modifica | R4 |
| Retorna  | R3 incrementado en 1 si solo si la cadena recibida en R6 comienza con el prefijo recibido en R5 |

- Explicar el funcionamiento del programa con un ejemplo
  - Suponiendo una cadena 0101 0000 0000 0000 en R5, y una cadena 0101 1100 0111 1111 en R6, se espera que el valor se incremente en 1

- Escribir la rutina *jugadorasConNivelMáximo*, de manera que cumpla con la siguiente documentación:

| jugadorasConNivelMáximo |     |
| ----------------------- | --- |
| Requiere | Un arreglo de perfiles de personas jugadoras de un videojuego con el formato NNNN IIII EEEE EEEE, donde NNNN representa el nivel, IIII es su identificador y EEEE EEEE su experiencia. El arreglo inicia en la celda 0x0F77, que finaliza con el primer elemento de valor 0000 |
| Modifica | **R1, R2** |
| Retorna | En R3 la cantidad de personas del arreglo que poseen el nivel máximo |

- Definir la rutina *jugadorasConNivelMáximo*, aclarando índice, acumulador o contador en caso de usarlos
  ```js
  jugadorasConNivelMaximo: MOV R2, 0x0F77 //Celda inicial
                           MOV R3, 0x0000 //Cant de personas con nivel máximo
                  repetir: CMP [R2], 0x0000
                           JE fin
                           MOV [R2], R1 //R1 es una celda auxiliar, para no pisar valores en memoria
                           CALL compararNivel
                           ADD R2, 0x0001
                           JMP repetir
                      fin: RET
  [assembly 0x0123]
  compararNivel: AND R1, 0x00FF
                 CMP R1, 0x00FF
                 JE sumarUno
                 RET
       sumarUno: ADD R3, 0x0001
                 RET
  ```

- Ensamblar la rutina a partir de la celda F000
  |Celda | Dato | Bin |
  | ---- | ---- | --- |
  0xF000 | 1880 |  0001 100010 000000  -> (codOp, M.Destino, M.Origen) |
  0xF001 | 0F77 |  0000 1111 0111 0111 -> (0x0F77) |
  0xF002 | 18C0 |  0001 100011 000000 |
  0xF003 | 0000 |  0000 0000 0000 0000|
  0xF004 | 6C80 |  0110 110010 000000 |
  0XF005 | 0000 |  0000 0000 0000 0000|
  0xF006 | F108 |  1111 0001 00001000 |
  0xF007 | 1C51 |  0001 1100010 100001|
  0xF008 | B000 |  1011 000000 000000 |
  0xF009 | 0123 |  0000 0001 0010 0011|
  0xF00A | 2880 |  0010 100010 000000 |
  0xF00B | 0001 |  0000 0000 0000 0001|
  0xF00C | A000 |  1010 000000 000000 |
  0xF00D | F004 |  1111 0000 0000 0100|
  0xF00E | C000 |  1100 0000 0000 0000|

3. Se cuenta con una arquitectura Q con una memoria cache de correspondencia directa con 4 lineas y bloques de memoria de 16 celdas
  - Indicar el formato de las direcciones que aplica esta caché, mediante un ejemplo
    - $\dfrac{cantCeldas}{cantLineas} = \dfrac{16}{4} = \dfrac{2^4}{2^2}$. En base a esto sabemos que se usan 4 bits para la Linea, 2, para el indice y el resto para el tag. Entonces, suponiendo una dirección ABCD (1010 1011 1100 1101)
      - índice: 01
      - línea: 0011
      - tag: 1010 1011 11
  - Dado el siguiente mapa de memoria, y asumiendo que la caché está vacía, que R0=DAD0, y PC=A000, calcular los aciertos y fallos ocasionados por la ejecución de la rutina ensamblada, indicando la etapa del ciclo de ejecución correspondiente

  <center>

  | Celda | Dato |
  | ----- | ---- |
  | A000 | 1C00 |
  | A001 | 0100 |
  | A002 | C000 |
  | ... | ... |
  | DAD0 | 9000 |
  | ... | ... |
  | FFEF | 0000 |
  | ... | ... |

  </center>
  
  |etapa|dir|tag|linea|indice|F/A|R/W|
  | --- |---|---| --- | ---- |---|---|
  |B.instrucción|A000|A0<sub>00</sub>| 0000 | 00 | F | R |
  |B.instrucción|A001|A0<sub>01</sub>| 0000 | 01 | A | R |
  |Alm.Resultado|DAD0|DA<sub>11</sub>| 0100 | 00 | F | W |
  |B.Instrucción|A002|A0<sub>00</sub>| 0000 | 10 | A | R |
  |E.Operación  |FFEF|FF<sub>11</sub>| 1011 | 11 | F | R |

  - Explicar detalladamente a modo de ejemplo un acierto y un fallo, indicando como se relaciona la información de los items anteriores
    - Un **fallo** ocurre cuando realiza una búsqueda de instrucción sobre la celda A000. Dado que la celda no está en caché, se cachea el bloque donde ésta se encuentra. Una vez está cacheada, se envía al CPU el dato
    - Un **acierto** ocurre cuando se realiza la segunda búsqueda de instrucción. Cómo el bloque que contiene la celda A001 fué cacheado en la etapa anterior, se envía el dato a la CPU directamente desde caché

4. Se cuenta con la rutina *negativoPuntoFijo*, cuya documentación es la siguiente

| negativoPuntoFijo |   |
| ----------------- |---|
| Requiere | En R1 un valor en el sistema SM(16,14) |
| Modifica | Nada |
| Retorna | Un 1 en R0 si el valor de R1 es negativo, o un 0 si es positivo |

  - Definir un escenario de prueba para la rutina donde el valor de R1 sea positivo y otro negativo
    ```
    Escenario de prueba 1:
      Datos iniciales:
        R1 = 0,51
      Resultado esperado:
        R0 <= 0
    
    Escenario de prueba 2:
      Datos iniciales:
        R1 = -1,13
      Resultado esperado:
        R0 <= 1
    ```
  - Representar los valores elegidos en los escenarios en el sistema indicado y calcular el error absoluto obtenido en cada caso
    - **Usando el método escalado**
      - $
        0,51 * 2^{14} = 8.355,84 \\
        R_{SM(16,14)}(0,51) = R_{SM(16)}(8356) = 1*(2^{13} + 2^{7} + 2^{5}) = 0010000010100000 
        $
      - $
        -1,13 * 2^{14} = -18.513,96 \\
        R_{SM(16,14)}(-1,13) = R_{SM(16)}(-18,514) = -1*(2^{14} + 2^{11} + 2^{6} + 2^{4} + 2^{1}) = 10100100001010010
        $
