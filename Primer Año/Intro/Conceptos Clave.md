# Cheatsheet

| Comandos |  |
| --- | --- |
| Comandos primitivos | Poner(Color); Sacar(Color); Mover(Dirección); IrAlBorde(); |
| Repetición simple | repeat (condicion) { … } |
| Alternativa condicional | if (condicion) { … } elseif (condicion) { … } else { … } |
| Repetición condicional | while (condicion) { … } |
| Alternativa en expresiones | choose ... when (condicion) ... otherwise |

| Definiciones |  |
| --- | --- |
| Punto de entrada | program { … } |
| Procedimientos | procedure Nombre (…params) { … } |
| Parámetros | (param1, param2, …) |
| Funciones | function nombre (…params) { … } |

|  | Color | Dirección | Número | Booleano |
| --- | --- | --- | --- | --- |
| Valores literales | Azul, Negro, Rojo, Verde | Norte, Este, Sur, Oeste | 0,1,2, …; -1,-2, … | true, false |
| Operadores de enumeración | minColor(), maxColor(), siguiente(Color), previo(Color) | minDir(), maxDir(), siguiente(Dirección), previo(Dirección) | siguiente(Número), previo(Número), opuesto(Número) | minBool(), maxBool(), previo(Número), opuesto(Número) |
| Sensores |  |  | numBolitas(Color) | hayBolitas(Color), puedeMover(Dir) |

| Tipos personalizados | |
| --- | --- |
| Definicion | type NombreDeMiTipo is ... {} |`

```js
type TipoDePokemon is variant {
    case Fuego {}
    case Agua {}
    case Planta {}
    // ...
}

type Pokemon is register {
    field nroPokedex,   // Numero
    field nombre,       // String
    field tipo          // TipoDePokemon
}

Pokemon(nroPokedex <- 1, nombre <- "Bulbasaur", tipo <- Planta)
```

| Operaciones con listas | |
| --- | --- |
| Obtener elementos | primero(lista), siguiente(elemento), esVacia(lista) |
| Append | lista ++ otraLista |

| Comentarios |  |
| --- | --- |
| Linea | // … |
| Bloque | /* … */ |

| Contratos |  |
| --- | --- |
| Propósito | ¿Qué? |
| Precondición | ¿Cuándo? |
