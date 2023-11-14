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

## Performance de la caché

```
Ttotal = Tcache + (1-Tasa de aciertos) * Tprincipal
```

