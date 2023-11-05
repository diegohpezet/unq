# Punto Fijo

1. Interpretar las siguientes cadenas en un sistema de punto fijo BSS(4,1) (es decir, con 4 bits en total, de los cuales 1 es fraccionario)
    - 0001
    - 1011

    _**Usando el método escalado:** <br> 0001 = 2<sup>0</sup> = 1. <br> Al escalar = 1 * 2<sup>-1</sup> = 1/2<sup>1</sup> = 1/2 = **0,5**_

    _1011 = 2<sup>3</sup> + 2<sup>1</sup> +2<sup>0</sup> = 8 + 2 + 1 = 9<br> Al escalar: 9 * 2<sup>-1</sup> = 9/2<sup>1</sup> = 9/2 = **4,5**_

2. ¿Cuál es el rango del sistema BSS(4,1)?

    _El rango del sistema BSS(4,1) es (0, 5.5)_

3. Interpretar las siguientes cadenas en un sistema de punto fijo BSS(7,3):
    - 0010110
        - **Usando el método escalado** <br> _IBss<sub>(7,3)</sub>(0010110) = 2<sup>4</sup> + 2<sup>2</sup> + 2<sup>1</sup> = 16 + 4 + 2 = 22 <br> Al escalar: 2 * 2<sup>-3</sup> = 22/2<sup>3</sup> = 22/8 = 2,75_
    - 1000000
        - **Usando el método por partes** <br> _IBss<sub>(7,3)</sub>(1000000) = 2<sup>3</sup> = 8_
    - 1000001
        - **Usando el método por partes** <br> _IBss<sub>(7,3)</sub>(1000001) = 2<sup>3</sup> + 2<sup>-3</sup> = 8 + 0,125 = 8,125_

4. ¿Cual es el rango del sistema BSS(7,3)?

    _El rango del sistema BSS (7,3) es (0, 15,875)_

5. Completar la tabla 1 interpretando cada cadena de 3 bits en los tres sistemas propuestos

6. Suponer un sistema BSS(10,4)
    * ¿Cuantos numeros se pueden representar?
        - 2<sup>10</sup> = 1024
    * ¿Cual es la resolucion del sistema?
        - La resolución es 2<sup>-4</sup>, que equivale a 0,0625
    * ¿Cuales son el maximo y el minimo numero representables?
        - Mínimo = 0 <br> 
        Máximo: I<sub>BSS(10,4)(1111111111)</sub> = 2<sup>5</sup> + 2<sup>4</sup> + 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> + 2<sup>-1</sup> + 2<sup>-2</sup> + 2<sup>-3</sup> + 2<sup>-4</sup> = 32 + 16 + 8 + 4 + 2 + 1 + 0.5 + 0.25 + 0.125 + 0,0625 = 63,9375</sub> <br> 
        Rango BSS(10,4) = (0, 63.9375)
    * ¿Cuales son el maximo y el minimo numero representable en el intervalo (0,1)? (es decir, en el intervalo desde el 0 hasta el 1, **ambos excluidos**)
        - Estos son 0,9375 (0000001111) y 0,0625 (0000000001)

7. Resonder las preguntas del ejercicio anterior para un sistema SM (10,4)
    * 2<sup>10</sup>-1 = 1023
    * Mínimo: I<sub>SM(10,4)</sub>(1111111111) = -1*(2<sup>4</sup> + 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> + 2<sup>-1</sup> + 2<sup>-2</sup> + 2<sup>-3</sup> + 2<sup>-4</sup>) = -1*(16 + 8 + 4 + 2 + 1 + 0,5 + 0,25 + 0,125 + 0,0625) = -1*(31,9375) = -31,9375<br>
    Máximo: I<sub>SM(10,4)</sub>(0111111111) = 1*(2<sup>4</sup> + 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> + 2<sup>-1</sup> + 2<sup>-2</sup> + 2<sup>-3</sup> + 2<sup>-4</sup>) = 1*(16 + 8 + 4 + 2 + 1 + 0,5 + 0,25 + 0,125 + 0,0625) = 1*(31,9375) = 31,9375<br><br>
    Rango SM<sub>(10,4)</sub>: (-31,9375, 31,975)
    * La resolucion es 2<sup>-4</sup>, que equivale a 0,0625
    * Estos son 0,9375 (0000001111) y 0,0625 (0000000001)

8. ¿Cuál es la resolucion de un sistema BSS(N,M)?
    - La resolucion de un sistema BSS(N,M) es igual al valor del bit menos significativo

9. Suponer un sistema BSS(8,4). Represente los siguientes numeros y calcule el error absoluto y relativo en cada caso: 
    - 10,2
        - R<sub>BSS(8,4)</sub>(10,2) = R<sub>BSS(8,4)</sub>(2<sup>3</sup> + 2<sup>1</sup> 2<sup>-2</sup>) = 10100011
            - I<sub>BSS(8,4)</sub>(10100011) = 10,1875 <br>
            Entonces el error absoluto es |10,2 - 10,1875| = |0,0125| <br>
            El error relativo es (EA<sub>(10,2)</sub> / 10,2) = 0,0125 / 10,2 = 0,0012254901960784
    - 0,125
        - R<sub>BSS(8,4)</sub>(0,125) = R<sub>BSS(8,4)</sub>(2<sup>-3</sup>) = 00000010
            - I<sub>BSS(8,4)</sub>(00000010) = 0,125 <br>
            Entonces el error absoluto es |0,125 - 0,125| = |0| <br>
            El error relativo es 0/0,125 = 0

10. Suponer un sistema BSS(4,1). Al representar el valor 1,1 se obtiene un error absoluto de 0,1 pues se aproxima con el **valor 1** (cadena 0010). Si se quiere representar el valor **1,2** se obtiene un error absoluto de 0,2
    - ¿Qué error se obtiene a representar el **1,3**?
        - Se obtiene 0,2, puesto que la resolucion es 0,5 y el error absoluto no puede superar la mitad de la misma
    - ¿Cuál es el **máximo error absoluto** que puede ocurrir al representar un valor? Ojo: dentro del rango representable
        - Resolucion/2 = 2.5
    - ¿Cual es el rango del sistema?
        - Rango BSS(4,1): (0, 7,5)

11. ¿Cuál es el **máximo error absoluto** que puede ocurrir al representar un valor en cada uno de los siguientes sistemas?
    - BSS(4,2): 0.25/2 = 0.125
    - BSS(4,3): 0.125/2 = 0.0625

12. Supongamos que se desea utilizar un sistema de punto fijo SM(X,Y) para representar números entre -10 y 10. Se pretende ademas que el error absoluto sea menor a 0.2. ¿Cuales son los mínimos X,Y que satisfacen estos requerimientos?

13. Se necesita un sistema de punto fijo que permita las siguientes cosas: 
    - Representar el número -17
    - Representar el número 42
    - Que el error absoluto máximo sea menor a 0.05
    
    Diseñe el sistema con la minima cantidad de bits

14. Construya un circuito que dada una cadena de 5 bits, devuelva un 1 si la cadena representa un numero en SM(5, 2) con parte fraccionaria distinta a cero, y un 0 en caso contrario.

15. Utilizando circuitos que conozca, construya un circuito que dadas dos cadenas en BSS(3,3), devuelva el resultado de sumarlas, es decir, devuelva una cadena BSS(4,3).

16. Suponga que se desea agregar a Q3 capacidades de computo para numeros en punto fijo:
    - ¿Que sistema recomendarıa, con cuantos bits para la parte fraccionaria y cuantos para la parte entera?
    - ¿Que instrucciones agregarıa a Q3? Especifique los nuevos codigos de operacion y el comportamiento de dichas instrucciones._Se puede utilizar un codigo de operacion extensible (mediante un prefijo) tal como se hace con los saltos condicionales._
    - ¿Como modificarıa la ALU para que soporte dichas instrucciones? No se requiere construir los circuitos, solo explicar cuales serıan los circuitos necesarios.

# Punto Flotante

17. Completar la tabla 2 con la interpretacion de las cadenas en cada sistema indicado
    
|  Cod  | BSS(3) | BSS(3,1) | SM(3,1) |
| :---: | :----: | :------: | :-----: |
| 0000  |   0    |   0,0    |   0,0   |
| 0001  |   1    |   0,5    |   0,5   |
| 0010  |   2    |   1,0    |   1,0   |
| 0011  |   3    |   1,5    |   1,5   |
| 0100  |   4    |   2,0    |   2,0   |
| 0101  |   5    |   2,5    |   2,5   |
| 0110  |   6    |   3,5    |   3,0   |
| 0111  |   7    |   4,0    |   3,5   |
| 1000  |   8    |   4,5    |   -0    |
| 1001  |   9    |   5,0    |  -0,5   |
| 1010  |   10   |   5,5    |  -1,0   |
| 1011  |   11   |   6,0    |  -1,5   |
| 1100  |   12   |   6,5    |  -2,0   |
| 1101  |   13   |   7,0    |  -2,5   |
| 1110  |   14   |   7,5    |  -3,0   |
| 1111  |   15   |   8,0    |  -3,5   |

18.  Comparar los sistemas de la tabla 2 a partir de una cadena a eleccion

|  Cod  | BSS(3) | BSS(3,1) | SM(3,1) |
| :---: | :----: | :------: | :-----: |
| 1011  |   11   |   6,0    |  -1,5   |

19.  Para cada sistema de la tabla 2 calcular rango, resolucion maxima y resolucion mınima.

| Sistema  |    Rango    | Resolución maxima | Resolucion minima |
| :------: | :---------: | :---------------: | :---------------: |
|  BSS(3)  |   [0; 7]    |                   |                   |
| BSS(3,1) |   [0; 8]    |                   |                   |
| SM(3,1)  | [-3,5; 3,5] |                   |                   |

20.  Calcular rango, resolucion mınima y resolucion maxima para un sistema con mantisa en BSS(5) y exponente en BSS(3).
- Mmin = I<sub>BSS(5)</sub>(00000) = 0
- Mmax = I<sub>BSS(5)</sub>(11111) = 16 + 8 + 4 + 2 + 1 = 31
- Emax = I<sub>BSS(3)</sub>(111) = 4 + 2 + 1 = 7
- Rango = [0 x 2<sup>7</sup>; 31 x 2<sup>7</sup>] = [0; 3968]
  
|   Rango   | Resolución maxima | Resolucion minima |
| :-------: | :---------------: | :---------------: |
| [0; 3968] | Resolución maxima | Resolucion minima |

21.    Buscar un contraejemplo para refutar lo siguiente: _En punto flotante es posible representar todos los numeros reales contenidos en el rango._

- Imaginar un sistema de punto flotante con mantisa en BSS(2) y exponente en BSS(2). Si se intenta representar el valor 5 se puede notar que no hay cadena que lo represente a pesar de que el rango sea [0, 24]. *Fuente: pag 143*

22.   Completar la tabla 3 interpretando las cadenas en cada uno de los sistemas indicados.

|  Cod  | e: BSS(2) / m: BSS(2,2) | e: CA2(2) / m: BSS(2,2) |
| :---: | :---------------------: | :---------------------: |
| 0000  |            0            |            0            | e: 0 - 0 / m: 0  |
| 0001  |            0            |            0            | e: 1 - 1/ m: 0   |
| 0010  |            0            |            0            | e: 2 - 0/ m: 0   |
| 0011  |            0            |            0            | e: 3 - -1 / m: 0 |
| 0100  |          0,25           |          0,25           | e: 0 / m: 0,25   |
| 0101  |           0,5           |           0,5           | e: 1 / m: 0,25   |
| 0110  |            1            |          0,25           | e: 2 / m: 0,25   |
| 0111  |            2            |          0,125          | e: 3 / m: 0,25   |
| 1000  |           0,5           |           0,5           | e: 0 / m: 0,5    |
| 1001  |            1            |            1            | e: 1 / m: 0,5    |
| 1010  |            2            |           0,5           | e: 2 / m: 0,5    |
| 1011  |            4            |          0,25           | e: 3 / m: 0,5    |
| 1100  |          0,75           |          0,75           | e: 0 / m: 0,75   |
| 1101  |           1,5           |           1,5           | e: 1 / m: 0,75   |
| 1110  |            3            |          0,75           | e: 2 / m: 0,75   |
| 1111  |            6            |          0,375          | e: 3 / m: 0,75   |


23.   Para cada sistema de la tabla 3 calcular rango, resolucion maxima y resolucion mınima.

e: BSS(2) / m: BSS(2,2) 
- Mmin = I<sub>BSS(2,2)</sub>(00) = 0,0
- Mmax = I<sub>BSS(2,2)</sub>(11) = 0,75
- Emin = I<sub>BSS(2)</sub>(00) = 0
- Emax = I<sub>BSS(2)</sub>(11) = 3

- Rango = [0 x 2<sup>3</sup>; 0,75 x 2<sup>3</sup>] = [0; 6]
- Resolucion máxima = I<sub>BSS(2,2)</sub>(01) * 2<sup>3</sup> = 2<sup>-2</sup> * 2<sup>3</sup> = 0.25 * 8 = 2
- Resolucion mínima = I<sub>BSS(2,2)</sub>(01) * 2<sup>0</sup> = 2<sup>-2</sup> * 2<sup>0</sup> = 0.25 * 1 = 0.25

e: CA2(2) / m: BSS(2,2) 
- Mmin = I<sub>BSS(2,2)</sub>(00) = 0,0
- Mmax = I<sub>BSS(2,2)</sub>(11) = 0,75
- Emax = I<sub>CA(2)</sub>(11) = -1
- Rango = [0 x 2<sup>-1</sup>; 0,75 x 2<sup>-1</sup>] = [0; 0,375]

|         Sistema         |   Rango    | Resolución maxima | Resolucion minima |
| :---------------------: | :--------: | :---------------: | :---------------: |
| e: BSS(2) / m: BSS(2,2) |   [0; 6]   | Resolución maxima | Resolucion minima |
| e: CA2(2) / m: BSS(2,2) | [0; 0,375] | Resolución maxima | Resolucion minima |

1.    Interpretar las siguientes cadenas aplicando el siguiente formato: [ mantisa: SM(9,7) ][ exponente: SM(7)]

- 1110 1110 0101 1111
    - m = Ism(9,7)(111011100) = -1(Ibss(8,7)(11011100)) = -1*(2<sup>0</sup> + 2<sup>-1</sup> + 2<sup>-3</sup> + 2<sup>-4</sup> + 2<sup>-5</sup>) = -1*(1 + 0,5 + 0,125) + 0,0625 + 0,03125 = -1,71875
    - e = Ism(7)(1011111) = -1*(Ibss(6)(011111)) = -1*(2<sup>4</sup> + 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup>) = -1*(16 + 8 + 4 + 2 +1) = -31
    - m x 2<sup>e</sup> = -1,71875 * 2<sup>-31</sup> = -1,71875 * 2<sup>-31</sup>00000000008
- 0010 0001 1000 1100
    - m = I<sub>SM(9,7)</sub>(001000011) = 1*(I<sub>BSS(8,7)</sub>(01000011)) = 1*(2<sup>0</sup> + 2<sup>-6</sup> + 2<sup>-7</sup>) = 1*(1 + 0,015625 + 0,0078125) = 1,0234375
    - e = I<sub>SM(7)</sub>(000 1100) = 1*(I<sub>BSS(6)</sub>(001100)) = 1*(2<sup>3</sup> + 2<sup>2</sup>) = 1*(8+4) = 12
    - m x 2<sup>e</sup> = 1,0234375 x 2<sup>12</sup> = 4.192

25.   Calcular rango, resolucion mınima y resolucion maxima para el sistema del ejercicio anterior

|   Rango   | Resolución maxima | Resolucion minima |
| :-------: | :---------------: | :---------------: |
| [0; 3968] | Resolución maxima | Resolucion minima |

## Ejercicios integradores

1. ¿Qué problema representa el error relativo? ¿Es lo mismo un error cerca del 0 qué lejos de el? 
  - El error relativo representa la distancia de un número respecto a otro. Mientras más cerca del 0 este un valor, más importante es su error

2. ¿Como soluciona el punto flotante esto? ¿Como se expresa un valor en punto flotante? 
  - El punto flotante trabaja con enteros para luego, mediante una formula desplazar la coma sobre ese numero

3. ¿Como es la resolución en punto flotante? ¿Se comporta de la misma manera que la resolución en punto fijo? 
  - La resolución en punto flotante es variable, puesto que al tratarse de exponentes la distancia entre dos valores se va incrementando a medida que el exponente aumenta

4. ¿Qué se empobrece respecto a punto fijo? 
  - En escalas más grandes se pierden valores debido al aumento exponencial