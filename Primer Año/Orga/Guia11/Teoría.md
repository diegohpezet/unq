# Conceptos

**Mem.Cache**: Memoria de rapido acceso que almacena un _bloque_ de la memoria

**Bloque**: Conjunto de lineas consecutivas que se almacenan en una misma linea de cache

**Tag**: Referencia un bloque, son los bits mas significativos en cache

**Linea**: Conjunto de bloques en una linea del cache

**Indice**: Referencia a elemento individual dentro de una linea

- Ejemplo: A0F9

Correspondencia Asociativa

| Tag | Indice |
| :-- | -----: |
| A0F |      9 |

Correspondencia Directa

| Tag | Linea | Indice |
| :-- | :---: | -----: |
| A   |  0F   |      9 |

//Busca la linea 0F del tag A que tenga indice 9

# Orden de correspondencia

Orden establecido para definir como almacenar en cache

# Correspondencia Asociativa

Busca la instruccion de manera conjunta en todas las lineas de cache

Fórmula: $\dfrac{cantCeldas}{"cantCeldasPorLinea"} = cantBloques$

Ejemplo: $\dfrac{64}{4}$ = $\dfrac{2^6}{2^2}$ = $2^4$ = 16

Dada la formula sabemos que:

- Se usan 2 bits para el indice ($2^2$)
- Se usan 4 bits para el tag($2^4$)
- Hay 16 bloques

# Correspondencia Directa

Mediante el tag y el indice se define en donde esta el dato buscado

Puede ocurrir un acierto si el dato solicitado esta en cache o un fallo si no. Cuando se produce un fallo la cache almacena el dato solicitado

## Comparacion

| -           | Asociativa             | Directa |
| ----------- | ---------------------- | ------- |
| Ventajas    | Mayor tasa de aciertos |         |
| Desventajas |                        |         |

**Tasa**: Relacion entre aciertos y fallos ($\dfrac{aciertos}{fallos}$)

### Ejemplo de direccion

El CPU pide _C132_

Considerando el siguiente esquema de memoria:

C130 |0000|
C131 |1111|
C132 |2222|
.... |....|
C13F |FFFF|

| Dir | Linea | Indice |
| --- | ----- | ------ |
| C   | 13    | 2      |

## Politicas de reemplazo

**Cabe destacar que esto solamente aplica en C.Asociativa**

- FIFO (First In First Out): El primer registro en entrar es tambien el primero en salir
- LRU (Last REcently Used): Lo usado mas recientemente se conserva. La cache se va actualizando en base al uso.
- LFU (Least Used): Sale el registro menos usado

## Politicas de escritura

- Write Through: Escribe en mem principal a la vez que se reemplaza un valor en cache
- Write Back: Escribe primero el valor en cache y lo copia a ppal cuando desaloja el dato de cache

# Principios de localidad

- Localidad espacial: Puede ser que se use una celda consecutiva a la llamada recientemente
- Localidad temporal: Puede ser que vuelva a usar una celda llamada recientemente

## Performance de la caché

$$
\begin{align*}
WriteBack: \\
TiempoTotal = CantFallos * (TiempoCache + TiempoPpal) + CantAciertos * TiempoCache\\
\\
WriteThrough: \\
TiempoTotal = (CantFallosLectura + CantEscrituras) * (TiempoCache + TiempoPpal) + (CantAciertos * TiempoCache)
\end{align*}
$$
