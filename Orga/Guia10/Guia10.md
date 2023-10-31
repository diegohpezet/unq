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
        - Máximo num dividido la cantidad de saltos que se realizan: **63,9375 / 0,0625 = 1023**
    * ¿Cual es la resolucion del sistema?
        - La resolución es 2<sup>-4</sup>, que equivale a 0,0625
    * ¿Cuales son el maximo y el minimo numero representables?
        - Mínimo = 0 <br> 
        Máximo: I<sub>BSS(10,4)(1111111111)</sub> = 2<sup>5</sup> + 2<sup>4</sup> + 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> + 2<sup>-1</sup> + 2<sup>-2</sup> + 2<sup>-3</sup> + 2<sup>-4</sup> = 32 + 16 + 8 + 4 + 2 + 1 + 0.5 + 0.25 + 0.125 + 0,0625 = 63,9375</sub> <br> 
        Rango BSS(10,4) = (0, 63.9375)
    * ¿Cuales son el maximo y el minimo numero representable en el intervalo (0,1)? (es decir, en el intervalo desde el 0 hasta el 1, **ambos excluidos**)
        - Estos son 0,9375 (0000001111) y 0,0625 (0000000001)

7. Resonder las preguntas del ejercicio anterior para un sistema SM (10,4)
    * 31,9375 / 0,0625 = 511
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
        - 0,2
    - ¿Cual es el rango del sistema?
        - Rango BSS(4,1): (0, 7,5)

11. ¿Cuál es el **máximo error absoluto** que puede ocurrir al representar un valor en cada uno de los siguientes sistemas?
    - BSS(4,2)
    - BSS(4,3)

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

18. Comparar los sistemas de la tabla 2 a partir de una cadena a eleccion

19. Para cada sistema de la tabla 2 calcular rango, resolucion maxima y resolucion mınima.

20. Calcular rango, resolucion mınima y resolucion maxima para un sistema con mantisa en BSS(5) y exponente en BSS(3).

21. Buscar un contraejemplo para refutar lo siguiente: _En punto flotante es posible representar todos los numeros reales contenidos en el rango._

22. Completar la tabla 3 interpretando las cadenas en cada uno de los sistemas indicados.
23. Para cada sistema de la tabla 3 calcular rango, resolucion maxima y resolucion mınima.

24. Interpretar las siguientes cadenas aplicando el siguiente formato: [ mantisa: SM(9,7) ][ exponente: SM(7)]
    - 1110 1110 0101 1111
    - 0010 0001 1000 1100

25. Calcular rango, resolucion mınima y resolucion maxima para el sistema del ejercicio anterior