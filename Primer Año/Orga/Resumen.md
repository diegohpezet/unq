# U7 - Q4: Flags, saltos y alternativa condicional

Para dirijir el flujo de la ejecución de programa a veces se establecen condiciones en el funcionamiento del mismo

```js
comparar: CMP R0, 0x0001
          JE esIgual
          MOV R5, 0x0000
          JMP salir

esIgual:  MOV R5, 0x0001
          JMP salir

salir:    RET
```

## Ensamblado

- **CMP**: Es una instrucción de dos operandos, como se venía trabajando anteriormente. Su CodOp es 0110
  - CMP R0, 0xFEDC = 0110 100000 000000 1111 1110 1101 1100

- **JMP**: Es un salto absoluto, el valor del operando origen debe ser la dirección de memoria donde se desea saltar. Suponer que "salir" está ubicado en 0x9000
  - JMP salir = 1010 000000 000000 1001 0000 0000 0000

- **Saltos condicionales**: Son saltos relativos. No reemplazan el valor de PC con una dirección de memoria sino que le suman o le restan el valor del desplazamiento expresado en CA2(8)
- JE salir 1111(Prefijo) 0001(JE) [desplazamiento(8)]

## Cómo se implementa una comparación (Flags)

Se reformula la evaluación del CMP en términos de una resta

Hay 4 flags:
- Z(zero): Toma el valor 1 si el resultado de la resta es 0
- N(negative): Toma el valor 1 si el resultado de la resta es negativo
- C(carry): Toma el valor 1 cuando la resta o la suma tuvieron acarreo
- V(overflow): Toma el valor 1 cuando el resultado no tiene el signo esperado

# U8 - Q5: Repeticiones y máscaras

La **estructura de repetición** permite repetir bloques de código. Su estructura es la siguiente:

```js
//Inicialización de variables
MOV R0, 0x0000       //Contador

repetir: CMP R0, 0x0005
         JE salir
         ADD R0, 0x0001
         JMP repetir

salir:   RET
```

Este programa solo se repite 5 veces, incrementando un contador

Las **máscaras** por su parte permiten modificar los valores de ciertas posiciones de una cadena de bits. Puede ser necesario para conocer el valor de determinado bit, por ejemplo para determinar si un valor es par o impar.

Las máscaras son
- AND
- OR
- XOR
- NOT

Ejemplo de uso:

```js
esPar: MOV R4, 0xFFF1 
       AND R4, 0x0001       
       // 1111 1111 1111 0001 ^ 0000 0000 0000 0001 = 1
       CMP R4, 0x0001
       JNE siEs
       MOV R5, 0x0000
       JMP fin

siEs:  MOV R5, 0x0001
fin:   RET
```

# U9 - Arreglos

**Arreglo**: Conj. de valores en el mismo sistema numerico almacenados en un bloque.

Mediante repeticion se pueden recorrer. Ejemplo:

```js
recorrido: MOV R1, 0x0000  // Inicia el contador

ciclo: CMP R1, 0x0004
       JG fin
       ADD R1, 0x0001
       JMP ciclo

fin: RET
```

## Método de direccionamiento indirecto

Sirve para indicar que se apunta al dato que indica el dato del registro indicado. Suponer:

[R0], donde R0 tiene almacenado el valor 2000. En este caso, se buscaría el valor dentro de la celda 0x2000

# U10 - Sistemas en punto fijo y punto flotante

Son sistemas binarios que permiten representar números con valores decimales.

Surge nuevos concepto, **resolución**, que es la distancia mínima entre dos valores y **error**, que es la diferencia entre el valor buscado y el valor obtenido

## Punto Fijo

Se dedican los primeros bits a la parte entera, el resto a la parte fraccionaria.

<center>

**Suponer un sistema BSS(8,3) y una cadena 10011101**

| Sistema  | Cadena   | Interpretación | Rango       | Resolución |
| -------- | -------- | -------------- | ----------- | ---------- |
| BSS(8,3) | 10011101 | 19,625         | [0; 31,825] | 0,125      |

</center>

### Interpretación

**Método por partes**: Se interpreta la cadena de la siguiente manera:
- $I_{BSS(8,3)}(10011101) = 1*2^{4} + 0*2^{3} + 0*2^{2} + 1*2^{1} + 1*2^{0} + 1*2^{-1} + 0*2^{-2} + 1*2^{-3} = 0.125 + 0.5 + 1 + 2 + 16 = 19,625$

**Método escalado**: Primero se interpreta la cadena como en BSS y luego se la divide por $2^{n}$, donde n es la cant de decimales
- $I_{BSS(8)}(10011101) = 2^{7} + 2^{4} + 2^{3} + 2^{2} + 2^{0} = 128 + 16 + 8 + 4 + 1 = 157$ <br /> <br /> $\dfrac{157}{2^3} = \dfrac{157}{8} = 19,625$

### Representación y error

Para representar empleando el método escalado se redondea el resultado de $x*2^n$, donde n representa la cantidad de bits correspondientes a la parte fraccionaria. Luego simplemente se representa esa cadena en BSS

Ejemplo = $19,625 * 2^3 = 19,625 * 8 = 157$
$R_{BSS(8)}(157) = 2^{7} + 2^{4} + 2^{3} + 2^{2} + 2^{0}$ = 10011101

### Rango

- **Mínimo** = $I_{BSS(8,3)}(00000000) = 0$
- **Máximo** = $I_{BSS(8,3)}(11111111) = 31,825$
- **Rango** = [0; 31,825]

### Resolución

$2^{-m}$, donde m es la cantidad de bits que representan el valor decimal

Entonces: $2^{-3} = 0.125$

## Punto Flotante

Expresa el valor entero y luego lo desplaza para representar valores decimales

<center>

**Suponer un sistema de punto flotante con mantisa en BSS(5) y exponente en SM(3) y una cadena 10011101**

| Sistema                           | Cadena   | Interpretación | Rango       | Resolución |
| --------------------------------- | -------- | -------------- | ----------- | ---------- |
| mantisa: BSS(5), exponente: SM(3) | 10011101 | 9,5            | [0; 31,825] | 0,125      |

</center>

### Interpretación

Se interpreta por un lado la mantisa y por otro el exponente. Luego se reemplazan los valores en la formula: **$m * 2^e$**

- m = $I_{BSS(5)}(10011) = 2^4 + 2^1 + 2^0 = 19 $
- e = $I_{SM(3)}(101) = -1*(2^0) = -1$

<center>

$19 * 2^{-1} = 19 * 0.5 = 9,5$

</center>

### Representación

### Rango

Se calculan la mantisa máxima y mínima, el exponente máximo y mínimo y luego se reemplazan en la fórmula: $[Mmin * 2^{Emax}, Mmax * 2^{Emax}]$

- Mmin = $I_{BSS(5)}(00000) = 0$
- Mmax = $I_{BSS(5)}(11111) = 31$
- Emin = $I_{SM(4)}(111) = -3$
- Emax = $I_{SM(4)}(011) = 3$

<center>

$[0 * 2^{3}; 31 * 2{3}]$

</center>

### Resolución

Corresponde a la distancia que puede mínima que puede haber entre 2 valores consecutivos. Al hablarse de exponentes este valor puede ser fijo o exponencial, es decir ir aumentando, por lo que puede haber una resolución fija o una resolución máxima y una mínima.

Se obtiene haciendo la **interpretación de la mantisa que represente el valor 1** y multiplicandolo a $2^{Emin}$ (para la R.minima) o $2^{Emax}$ (para la R.maxima)

- $Rmin = I_{BSS(5)}(00001) * 2^{-3} = 0.125$
- $Rmax = I_{BSS(5)}(00001) * 2^{3} = 8$

# U11 - Caché

La memoria caché es una memoria de acceso rápido para la CPU, almacena información que supone que se requiere tener "a mano" para reducir tiempos de lectura

Almacena información en **bloques**, que son conjuntos de celdas consecutivas en memoria. A cada bloque almacenado se le asigna una **línea** en caché. Para ubicar un elemento en caché se usa un **índice**, que dice que elemento de la linea es el solicitado

## Principios de localidad

- Localidad espacial: Se entiende que las posiciones cercanas a una celda accedida recientemente son más probables de volverse a usar
- Localidad temporal: Supone que cuando un programa hace referencia a una celda es probable que lo vuelva a hacer a la brevedad

## Funciones de correspondencia

**Correspondencia asociativa**: El contenido de cada celda leída se asocia a una etiqueta (*tag*)¨que identifica su dirección en memoria principal.

Busca de forma consecutiva en todas las lineas

*Ejemplo*: Suponer una memoria principal con direcciones de 16 bits y una memoria caché de 4 lineas, que almacenan bloques de 4 celdas cada una

```
Mem.Ppal: 
0x0000 | DA70 |
0x0001 | DA71 |
0x0002 | DA72 |
0x.... | DA73 |
0xFFFF | 9999 |

Mem.Caché:
Tag |Bloque             |
00  |DA70 DA71 DA72 DA73|
01  |DA74 DA75 DA76 DA77|
10  |.... .... .... ....|
11  |.... .... .... ....|
```

*Fórmula*: $\dfrac{cantCeldasMemPpal}{"cantCeldasPorLinea"} = cantBloques$

Ejemplo (con otros valores): $\dfrac{64}{4}$ = $\dfrac{2^6}{2^2}$ = $2^4$ = 16

Dada la formula sabemos que:

- Se usan 2 bits para el indice ($2^2$)
- Se usan 4 bits para el tag($2^4$)
- Hay 16 bloques

A la hora de realizar una **lectura** se determina primero si la celda está cacheada, aplicando el siguiente formato de dirección:

| Dirección: (16b) |             |
| ---------------- | ----------- |
| Nro.Bloque (12b) | Indice (4b) |

El algoritmo que se ejecuta es el siguiente:
```
Sea X la direccion de la celda pedida
Sea B el numero de bloque de la celda X
Sea I el indice correspondiente a la celda X
Si B no esta en etiquetando ninguna linea entonces :
       Leer bloque B
       Sea L la linea elegida ( segun algoritmo de reemplazo )
       Almacenar el bloque B en L
sino :
       Sea L la linea etiquetada por B
       Proyectar el dato D a pa
```

**Correspondencia Directa**: A parte del tag y el índice surge el concepto de **linea**. A la hora de validar si una celda está cacheada, la memoria caché debe buscar el bloque que la contiene, *únicamente en la linea que le corresponde a ese bloque*, usando el tag que lo identifica

```
Sea X la direccion de la celda pedida
Sea I el indice correspondiente a la celda X
Sea B el numero de bloque de la celda X
Sea L la linea que le corresponde al bloque B
Sea T el tag que corresponde al bloque B
Si L no tiene el tag T entonces :
       Leer bloque B
       Almacenar el bloque B en L
       Proyectar el dato D a partir de la linea L y el indice I
       Enviar dato D a la CPU
```

## Algoritmos de correspondencia

**LRU (Last Recently Used)**: Es el más común. Se reemplaza aquel bloque cuya última referencia se ha producido en el pasado más lejano

**FIFO (First In-First Out)**: El primer bloque en entrar es aquel bloque en salir

**LFU (Least Frequently Used)**: Reemplaza el bloque que se acceda con menos frecuencia

## Políticas de escritura

**Write-through**: Cada vez que un dato se modifica en memoria caché, se realiza el cambio en memoria principal. Manteniendo los bloques de caché y de principal iguales

**Write-back**: El dato se modifica primero en caché y, al desalojarse el bloque, se actualizan recién los cambios en mem.principal. Se identifica el bloque alterado mediante un *dirty bit*

## Performance de la caché

T<sub>total</sub> = T<sub>cache</sub> + (1-Tasa de aciertos) \* T<sub>principal</sub>
