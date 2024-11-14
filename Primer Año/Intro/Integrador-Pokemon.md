```js
type TipoDePokemon is variant{
/* PROPÓSITO: Modelar los tipos de Pókemon posibles */
    case Tierra {}
    case Agua {}
    case Fuego {}
}

type Pokemon is record {
/* 
    PROPÓSITO: Modelar un Pókemon
    INV.REP.: 
        * La fuerza y el nivel son mayores o iguales a 0
        * Si está debilitado (estáSaludable es falso), su fuerza es cero 
*/
    field tipo // TipoDePókemon
    field fuerza // Número
    field estáSaludable // Booleano.
    field nivel // Número
}

// --- Ejercicios con registros y variantes --- //

function es_MasFuerteQue_(pokemon1, pokemon2) {
/*
    PROPOSITO: Indica si el primer pokemon tiene mas fuerza que el segundo.
    PARAMETROS:
        * pokemon1: Pokemon
        * pokemon2: Pokemon
    TIPO: Booleano
    PRECONDICION: Ninguna
*/
    return (fuerza(pokemon1) > fuerza(pokemon2))
}

function esDeMayorNivel_Que_(pokemon1, pokemon2) {
/*
    PROPOSITO: Indica si el primer pokemon tiene mas nivel que el segundo.
    PARAMETROS:
        * pokemon1: Pokemon
        * pokemon2: Pokemon
    TIPO: Booleano
    PRECONDICION: Ninguna
*/
    return (nivel(pokemon1) > nivel(pokemon2))
}

function pokemon_PotenciadoEn_(pokemon, potenciador) {
/*
    PROPOSITO: Describe al pokemon dado potenciado en fuerza y nivel por el potenciador dado
    PARAMETROS:
        * pokemon: Pokemon
        * potenciador: Numero
    TIPO: Pokemon
    PRECONDICION: Ninguna
*/
    return (Pokemon(
            pokemon | 
            nivel <- nivel(pokemon) * potenciador, 
            fuerza <- fuerza(pokemon) * potenciador
        ))
}

function pokemon_ConValoresDuplicados(pokemon) {
/*
    PROPOSITO: Describe al pokemon dado potenciado en fuerza y nivel por dos
    PARAMETROS:
        * pokemon: Pokemon
    TIPO: Pokemon
    PRECONDICION: Ninguna
*/
    return(pokemon_PotenciadoEn_(pokemon, 2))
}

function pokemon_PotenciadoEn_SiEsDeTipo_(pokemon, factor, tipo) {
/*
    PROPOSITO: Describe al pokemon dado potenciado segun el factor dado si el mismo corresponde al tipo dado. Caso contrario devuelve el pokemon original
    PARAMETROS:
        * pokemon: Pokemon
        * factor: Numero
        * tipo: TipoDePokemon
    TIPO: Pokemon
    PRECONDICION: Ninguna
*/
    return (
        choose pokemon_PotenciadoEn_(pokemon, factor) when (tipo(pokemon) == tipo)
        pokemon otherwise
    )
}

function pokemon_Derrotado(pokemon) {
/*
    PROPOSITO: Describe al pokemon dado derrotado
    PARAMETROS:
        * pokemon: Pokemon
    TIPO: Pokemon
    PRECONDICION: El pokemon dado no debe estar debilitado
    OBSERVACION: Un pokemon está derrotado cuando su fuerza es 0 y su campo estáSaludable es falso
*/
    return (
        Pokemon(
            pokemon |
            fuerza <- 0,
            estáSaludable <- False
        )
    )
}

// --- Ejercicios con Listas de Registros --- //


```