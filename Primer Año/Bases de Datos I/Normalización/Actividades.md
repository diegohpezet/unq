# Ejercicio 1: Proceso de Normalización

Sea el siguiente esquema de BD que modela los museos y sus galerías con exposiciones

```
EXPOSICION<museo, ciudadMuseo, nombreGaleria, nombreObra, añoCreacion, precioEntrada>
```

con las restricciones:

1. Cada museo se encuentra en una ciudad (ciudadMuseo), pero en una ciudad puede haber muchos museos.
2. En cada museo, hay muchas galerías donde se exponen obras.
3. El nombre de las galerías (nombreGaleria) pueden repetirse en diferentes museos, no se repiten en un mismo museo.
4. Cada obra tiene un solo año de creación, pero en un año pueden haberse creado varias obras.
5. Una obra se encuentra en una galería.
6. El nombre para cada obra es único por obra.
7. Cada museo cobra un precio distinto (precioEntrada) por cada galería visitada.



**Resolución:**

*Claves*:
- MUSEOS: ciudadMuseo, museo
- GALERIAS: nombreGaleria, precioEntrada
- OBRAS: nombreObra, añoCreacion

*DFs*:
- ciudadMuseo, museo -> nombreGaleria
- nombreGaleria -> nombreObra
- nombreObra -> añoCreacion

1FN:
- **EXPOSICIÓN_MUSEOS**<<u>museo</u>, <u>ciudadMuseo</u>, <u>nombreGaleria</u>, <u>nombreObra</u>, añoCreación>
- **EXPOSICION_PRECIOS**<<u>museo</u>, <u>nombreGaleria</u>, precioEntrada>

2FN:
- **MUSEOS**<<u>museo</u>, <u>ciudadMuseo</u>>
- **GALERIAS**<<u>nombreGaleria</u>, precioEntrada, museo (FK)>
- **OBRAS**<<u>nombreObra</u>, añoCreación, nombreGaleria (FK)>
- 
3FN:
- **MUSEOS**<<u>museo</u>, <u>ciudadMuseo</u>>
- **GALERIAS**<<u>nombreGaleria</u>, precioEntrada>
- **OBRAS**<<u>nombreObra</u>, añoCreación, nombreGaleria (FK)>
- **EXPOSICIÓN**<<u>museo</u>, <u>nombreGaleria</u>, <u>nombreObra</u>>