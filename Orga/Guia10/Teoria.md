# Sistemas de numeración fraccionarios

Para representar numeros reales, es necesario tener una forma de codificar la "coma". La forma mas simple es determinando la posicion de la coma en un lugar fijo

## Sistemas de punto fijo

Se destinan una cierta cantidad de bits a la parte entera, y el resto a la parte fraccionaria

- BSS(n,m): sistema de punto fijo en BSS con n bits en total de los cuales m son fraccionarios
- SM(n,m): sistema de punto fijo en SM con n bits en total, de los cuales 1 es de signo y m de parte fraccionaria. Esto implica que _n-m-1_ corresponden a la parte entera.

Los bits fraccionarios tienen un peso, que esta asociado a una potencia de 2 negativa. Así, el primer bit fraccionario tiene un peso de 2<sup>-1</sup>, el segundo de 2<sup>-2</sup> y así sucesivamente.

Es por esto último que para **interpretar** una cadnea en punto fijo, se debe interpretar por un lado la parte entera en el sistema correspondiente y, por otro lado, la parte fraccionaria

### Interpretacion

Hay dos mecanismos

- Por partes: Requiere que se trabaje por un lado la parte entera y por otro lado la parte fraccionaria.
    
    Por ejemplo: Si se quiere interpretar BSS(8,3)(10011101), se toman los 5 bits de la parte entera y 3 para la parte fraccionaria
    - IBss(8,3)(10011101) = 2<sup>4</sup> + 2<sup>1</sup> + 2<sup>0</sup> + 2<sup>-1</sup> + 2<sup>-3</sup> = 16 + 2 + 1 + 0,5 + 0,125 = 19,625

- Escalado: Interpretar el numero como en BSS y dividir por 2<sup>m</sup>
    - IBss(8,3)(10011101) = 2<sup>7</sup> + 2<sup>4</sup> + 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>0</sup> = 157. Entonces se escala el valor entero: 157 * 2<sup>-3</sup> = 157/2<sup>-3</sup> = 157/8 = 19,625

### Representación y error

- Por partes: Requiere representar por un lado la parte entera y por el otro la parte fraccionaria 

    Por ejemplo: Se quiere representar el valor **3,8** en el sistema BSS(7,4)
    1. Representar el valor 3 usando los bits enteror (3 bits): **011**
    2. Construir la cadena fraccionaria que aproxime el valor 0,8 multiplicando por 2 tantas veces como bits fraccionarios se 
    
### Rango y resolucion



