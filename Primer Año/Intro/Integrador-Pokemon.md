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
type Entrenador is record{
/* PROPÓSITO: Modelar un entrenador de Pókemon.
INV.REP.: identificador es un número > 0 */
    field lista // [Pokemon]
    field identificador // Número
    field esTactico // Booleano
}


function entrenador__(id, tactico) {
/*
    PROPOSITO: Describe un entrenador con los datos dados sin ningún pokemon en su lista
    PARAMETROS:
        id: Numero - identificador del entrenador
        tactico: Booleano - indica si el entrenador es táctico o no
    TIPO: Entrenador
    PRECONDICION: **id** debe ser mayor a 0
*/
    return (
        Entrenador(
            lista <- [], 
            identificador <- id,
            esTactico <- tactico
        )
    )
}

function entrenador_ConPokemon_Agregado(entrenador, pokemon) {
/*
    PROPOSITO: Describe al entrenador resultante de agregar el pokemon dado a la lista de pokemon del entrenador dado
    PARAMETROS:
        * entrenador: Entrenador
        * pokemon: Pokemon
    TIPO: Entrenador
    PRECONDICION: Ninguna
*/
    return (
        Entrenador(
            entrenador | 
            lista <- lista(entrenador) ++ [pokemon]
        )
    )
}

function cantidadDePokemonDe_(entrenador) {
/*
    PROPOSITO: Describe la cantidad de pokemon que tiene un entrenador
    PARAMETROS: 
        * entrenador: Entrenador
    TIPO: Numero
    PRECONDICION: Ninguna
*/
    return (cantidadDeElementosEn_(lista(entrenador)))
}

function cantidadTotalDePokemonEn_(listaDeEntrenadores) {
/*
    PROPOSITO: Describe la cantidad de pokemon que tienen los entrenadores del listado dado
    PARAMETROS:
        * listaDeEntrenadores: [Entrenador]
    TIPO: Numero
    PRECONDICION: Ninguna
    OBSERVACIÓN: Es un recorrido de acumulacion por pokemon en un listado de entrenadores
*/
    cantidadDePokemonActual := 0
    foreach entrenador in listaDeEntrenadores {
        cantidadDePokemonActual := cantidadDePokemonActual + cantidadDePokemonDe_(entrenador)
    }

    return(cantidadDePokemonActual)
}

function entrenadorMasAntiguoEntre_Y_(entrenador1, entrenador2) {
/*
    PROPOSITO: Describe al entrenador mas antiguo entre los entrenadores dados
    PARAMETROS:
        * entrenador1: Entrenador
        * entrenador2: Entrenador
    TIPO: Entrenador
    PRECONDICION: Los entrenadores dados no deben tener la misma id
    OBSERVACION: El entrenador mas antiguo es aquel que tenga menor id
*/
    return (
        choose entrenador1 when (identificador(entrenador1) < identificador(entrenador2)) entrenador2 otherwise
    )
}

function elMasAntiguoEn_(listaDeEntrenadores) {
/*
    PROPOSITO: Describe al entrenador mas antiguo del listado de entrenadores dado
    PARAMETROS:
        * listaDeEntrenadores: [Entrenador]
    TIPO: Entrenador
    PRECONDICION: El listado dado no debe estar vacio y no debe haber dos entrenadores con la misma id
    OBSERVACION: Es un recorrido de mínimos sobre un listado de entrenadores donde se busca el entrenador con menor id
*/
    entrenadorMasAntiguoHastaAhora := primero(listaDeEntrenadores)
    foreach entrenador in resto(listaDeEntrenadores) {
        entrenadorMasAntiguoHastaAhora := entrenadorMasAntiguoEntre_Y_(entrenadorMasAntiguoHastaAhora, entrenador)
    }
    
    return(entrenadorMasAntiguoHastaAhora)
}

function menorCantidadDePokemonEntre_Y_(pokemonEntrenador1, pokemonEntrenador2) {
/*
    PROPOSITO: Describe la menor cantidad de pokemon que presenta alguno de los equipos dados, en caso de tener la misma longitud devuelve cualquiera
    PARAMETROS:
        * pokemonEntrenador1: [Pokemon]
        * pokemonEntrenador2: [Pokemon]
    TIPO: Numero
    PRECONDICION: Ninguna
*/
    return (
        minimoEntre_Y_(cantidadDeElementosEn_(pokemonEntrenador1), cantidadDeElementosEn_(pokemonEntrenador2))
    )
}

function cantidadDeVictoriasDeEntrenador_Contra_(entrenador1, entrenador2) {
/*
    PROPOSITO: Describe la cantidad de victorias que tendría el equipo de un entrenador contra el equipo de otro
    PARAMETROS:
        * entrenador1: Entrenador
        * entrenador2: Entrenador
    TIPO: Numero
    PRECONDICION: Ninguna
    OBSERVACION: 
        * En cada pelea entre dos Pókemon siempre gana el más fuerte, y si tienen igual fuerza, la pelea no cuenta para ninguno de los dos
        * Es un recorrido de acumulacion por pokemon en un equipo
*/
    pokemonEntrenador1 := lista(entrenador1)
    pokemonEntrenador2 := lista(entrenador2)
    
    victoriasEntrenador := 0
    
    repeat(menorCantidadDePokemonEntre_Y_(pokemonEntrenador1, pokemonEntrenador2)) {
        victoriasEntrenador := victoriasEntrenador + unoSi_CeroSiNo(es_MasFuerteQue_(primero(pokemonEntrenador1), primero(pokemonEntrenador2)))
        
        pokemonEntrenador1 := resto(pokemonEntrenador1)
        pokemonEntrenador2 := resto(pokemonEntrenador2)
    }
    
    return (victoriasEntrenador)
}

function entrenadorGanadorDeDesafioEntre_Y_(entrenador1, entrenador2) {
/*
    PROPOSITO: Describe al entrenador ganador de un desafío entre los entrenadores dados
    PARAMETROS:
        * entrenador1: Entrenador
        * entrenador2: Entrenador
    TIPO: Entrenador
    PRECONDICION: 
    OBSERVACION:
        * El desafío consiste en que compitan un Pókemon de cada entrenador hasta que se acaben los Pókemon de uno de ellos, resultando en batallas del primero con el primero, el segundo con el segundo, etc
        * Gana el desafío el entrenador que consiga ganar más batallas, o de haber empate en la cantidad de peleas ganadas, el de mayor antigüedad
*/
    return(
        choose entrenador1 when (cantidadDeVictoriasDeEntrenador_Contra_(entrenador1, entrenador2) > cantidadDeVictoriasDeEntrenador_Contra_(entrenador2, entrenador1))
               entrenador2 when (cantidadDeVictoriasDeEntrenador_Contra_(entrenador2, entrenador1) > cantidadDeVictoriasDeEntrenador_Contra_(entrenador1, entrenador2))
               entrenadorMasAntiguoEntre_Y_(entrenador1, entrenador2) otherwise
    )
}

function entrenadorGanadorDeDesafioEn_(listaDeEntrenadores) {
/*
    PROPOSITO: Describe al entrenador ganador de desafios en el listado de entrenadores dado
    PARAMETROS:
        * listaDeEntrenadores: [Entrenador]
    TIPO: Entrenador
    PRECONDICION: No deberían haber dos entrenadores con el mismo id
    OBSERVACION: Es un recorrido de máximos por entrenadores en un listado de entrenadores, que devuelve el entrenador que haya ganado a todos los entrenadores próximos en la lista
*/

    ganadorActual := primero(listaDeEntrenadores)
    foreach entrenador in resto(listaDeEntrenadores) {
        ganadorActual := entrenadorGanadorDeDesafioEntre_Y_(ganadorActual, entrenador)
    }
    
    return (ganadorActual)
}

function fuerzaTotalDe_(entrenador) {
/*
    PROPOSITO: Describe la fuerza total de los pokemon de un entrenador
    PARAMETROS:
        * entrenador: Entrenador
    TIPO: Numero
    PRECONDICION: Ninguna
*/
    fuerzaActual := 0
    foreach pokemon in lista(entrenador) {
        fuerzaActual := fuerzaActual + fuerza(pokemon)
    }
    
    return (fuerzaActual)
}

function fuerzaTotalEnBatallaEn_(listaDeEntrenadores) {
/*
    PROPOSITO: Describe la fuerza total de todos los pokemon de los entrenadores en la lista
    PARAMETROS:
        * listaDeEntrenadores: [Entrenador]
    TIPO: Numero
    PRECONDICION: Ninguna
    OBSERVACION: Es un recorrido de acumulacion por pokemon en un listado de entrenadores que se incrementa por la fuerza de cada pokemon de los mismos
*/

    fuerzaActual := 0
    foreach entrenador in listaDeEntrenadores {
        fuerzaActual := fuerzaActual + fuerzaTotalDe_(entrenador)
    }
    
    return (fuerzaActual)
}


program {
    // Repo de pokemones
    charmander := Pokemon(tipo <- Fuego, fuerza <- 20, nivel <- 5, estáSaludable <- True)
    squirtle := Pokemon(tipo <- Agua, fuerza <- 15, nivel <- 5, estáSaludable <- True)
    
    // Repo de entrenadores
    entrenador1 := entrenador__(1, True)
    entrenador2 := entrenador__(2, False)
    entrenador3 := Entrenador(
                    identificador <- 3, 
                    lista <- [
                        squirtle,
                        charmander,
                        charmander,
                        squirtle
                    ], 
                    esTactico <- False
                )
    entrenador4 := Entrenador(
                    identificador <- 4, 
                    lista <- [
                        charmander,
                        squirtle,
                        squirtle,
                        charmander
                    ], 
                    esTactico <- False
                )

    return (
        entrenadorGanadorDeDesafioEntre_Y_(entrenador3, entrenador4)
    )
}




/* --- Biblioteca --- */
function cantidadDeElementosEn_(lista) {
/*
    PROPOSITO: Describe la cantidad de elementos en la lista dada
    PARAMETROS: 
        * lista: Lista de elementos - Lista de elementos a buscar su cantidad de elementos
    TIPO: Numero
    PRECONDICION: Ninguna
    OBSERVACION: Es un recorrido de acumulacion por elementos de la lista dada
*/
    listaRestante := lista
    cantidadContada := 0
    while (not esVacía(listaRestante)) {
        cantidadContada := cantidadContada + 1
        listaRestante := resto(listaRestante)
    }
    return (cantidadContada)
}

function minimoEntre_Y_(valor1, valor2) {
	/*
		PROPOSITO: Describe el valor mas pequeño entre **valor1** y **valor2**
		PRECONDICION: **valor1** y **valor2** deben ser del	mismo tipo
		PARAMETROS: 
			* valor1: Expresion - Valor a comparar
			* valor2: Expresion - Valor a comparar
		TIPO: Expresion
	*/
	
	minimo := valor1
	if (valor1 > valor2) {
		minimo := valor2
	}
	
	return (minimo)
}

function unoSi_CeroSiNo(condicion) {
/*
	PROPOSITO: Describe 1 en caso de que se cumpla la condicion **condicion** o bien
	0 en caso de que no se cumpla
	PRECONDICION: Ninguna
	PARAMETROS:
		* condicion: Booleano - Condición que determina que valor se describe
	TIPO: Numero
*/
	return (choose 1 when (condicion) 0 otherwise)
}
```