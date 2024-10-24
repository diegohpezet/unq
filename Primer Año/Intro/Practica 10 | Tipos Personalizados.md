# Practica 10 - Tipos Personalizados

```js
/* ------ Expo en clase ------ */
type TipoDePokemon is variant {   // Variante
/*
    PROPOSITO: Modelar los tipos de pokemon
*/
    case Fuego {}
    case Agua {}
    case Planta {}
    case Electrico {}
}

type Pokemon is record {    // Registro
/*
    INV.REP:
        - **nombre** no puede ser un string vacio
        - **tipo** debe ser un Tipo de pokemon valido
*/
    field nombre    // String
    field tipo      // TipoDePokemon
}

pikachu := Pokemon(nombre <- "Pikachu", tipo <- Electrico)     // Constructor

function esPokemonTipoAgua(pokemon) {
/*
    PROPOSITO: Indica si el pokemon actual es de tipo Agua
    PARAMETROS:
        - pokemon: Pokemon - Pokemon a evaluar su tipo
    PRECONDICION: Ninguna
    TIPO: Booleano
*/
    return (tipo(pokemon) == Agua)
}

esPokemonTipoAgua(pikachu) // False

pikachuTipoAgua := Pokemon(pikachu | nombre <- "Pikachu de alola", tipo <- Agua)  // Cambiar valor
esPokemonTipoAgua(pikachuTipoAgua)  // True

// --- Ejercicio 1 --- //
/*
Declarar un tipo variante llamado DíaDeLaSemana, que sirva para identificar los días de la semana. Luego implementar las siguientes funciones (sin olvidar sus contratos):
*/
type DiaDeLaSemana is variant {
/*
    PROPOSITO: Modela un dia de la semana
    INV.REP: **dia** debe ser un dia de la semana
*/
    case Lunes {}
    case Martes {}
    case Miercoles {}
    case Jueves {}
    case Viernes {}
    case Sabado {}
    case Domingo {}
}

// --- a --- //
function diaSiguiente_(diaDeLaSemana) {
/*
    PROPOSITO: Describe el día siguiente de **diaDeLaSemana**
    PARAMETROS:
        - diaDeLaSemana: DiaDeLaSemana
    PRECONDICION:
        - **diaDeLaSemana** debe ser un dia válido
*/
    return (
        choose Martes when (diaDeLaSemana == Lunes)
               Miercoles when (diaDeLaSemana == Martes)
               Jueves when (diaDeLaSemana == Miercoles)
               Viernes when (diaDeLaSemana == Jueves)
               Sabado when (diaDeLaSemana == Viernes)
               Domingo when (diaDeLaSemana == Sabado)
               Lunes otherwise
    )
}

// --- b --- //
function diaPrevio_(diaDeLaSemana) {
/*
    PROPOSITO: Describe el día previo de **diaDeLaSemana**
    PARAMETROS:
        - diaDeLaSemana: DiaDeLaSemana
    PRECONDICION:
        - **diaDeLaSemana** debe ser un dia válido
*/
    return (
        choose Domingo when (diaDeLaSemana == Lunes)
               Lunes when (diaDeLaSemana == Martes)
               Martes when (diaDeLaSemana == Miercoles)
               Miercoles when (diaDeLaSemana == Jueves)
               Jueves when (diaDeLaSemana == Viernes)
               Viernes when (diaDeLaSemana == Sabado)
               Sabado otherwise
    )
}

// --- c --- //
function esDiaDeFinDeSemana(diaDeLaSemana) {
    /*
        PROPOSITO: Indica si el **diaDeLaSemana** es un dia de fin de semana
        PARAMETROS:
            - diaDeLaSemana: DiaDeLaSemana
        PRECONDICION:
            - **diaDeLaSemana** debe ser un dia válido
    */ 
    return (
        choose True when (
            diaDeLaSemana == Viernes || diaDeLaSemana == Sabado || diaDeLaSemana == Domingo
        ) False otherwise
    )
}

program {
    if (esDiaDeFinDeSemana(diaPrevio_(Lunes))) {
        Poner(Azul)
    }
}

// --- Ejercicio 2 --- //
type PartidoPolitico is variant {
/*
    PROPOSITO: Modela los distintos partidos políticos
*/
    case DemocraciaPorLaVerdad {}
    case UnidosPorLaRepública {}
    case LiberalesPorLaLibertad {}
    case IzquierdaDeLosObreros {}
}

type Partido is record {
    field nombre    // PartidoPolitico
    field votos     // Numero
}

function cantidadDeVotosDe_(unPartido) {
/*
    PROPÓSITO: Indica la cantidad de votos que recibió un partido.
    PARÁMETROS
    * unPartido: Partido - El partido político del cual saber
    su cantidad de votos.
    TIPO: Número
    PRECONDICIÓN: Ninguna
*/
    return (votos(unPartido))
}

function tieneMasVotantes_Que_(partidoPolitico1, partidoPolitico2) {
/*
    PROPOSITO: Indica si **partidoPolitico1** tiene mas votantes que **partidoPolitico2**
    PARAMETROS:
        partidoPolitico1: PartidoPolitico - Partido político a comparar
        partidoPolitico2: PartidoPolitico - Partido político a comparar
    PRECONDICION: La cantidad de votantes no puede ser igual entre los dos partidos politicos
    TIPO: Booleano
*/
    return (cantidadDeVotosDe_(partidoPolitico1) > cantidadDeVotosDe_(partidoPolitico2))
}

function elQueTieneMásVotos() {
/*
    PROPOSITO: Describe el partido con mas votantes
    PRECONDICION: No debe haber dos o mas partidos con la misma cantidad de votos
    TIPO: PartidoPolitico
*/
}

function habraBallotage() {
/*
    PROPOSITO: Indica si habrá ballotage en estas elecciones
    PRECONDICION: Ninguna
    TIPO: Booleano
    OBSERVACION: Existe ballotage cuando el partido con más votos no acumula más del 50% de los votos totales y no hay una diferencia de más del 10% entre el primero y el segundo candidato
*/
}

/* --- Ejercicio 3 --- */
type Palo is variant {
/*
    PROPOSITO: Modelar los palos de las cartas del truco
*/
    case Oro {}
    case Espada {}
    case Copa {}
    case Basto {}
}

type Carta is record {
/*
    PROPOSITO: Modelar las cartas del truco
    INV.REP: 
        - **valor** debe ser un numero del 1 al 12
*/
    field valor     // Numero
    field palo      // Palo
}

function anchoDeEspadas() {
    return (Carta(valor <- 1, palo <- Espada))
}

function anchoDeBastos() {
    return (Carta(valor <- 1, palo <- Basto))
}

function laCarta_De_(valorCarta, paloCarta) {
    return (Carta(valor <- valorCarta, palo <- paloCarta))
}

function esUnAncho_(carta) {
    return (valor(cata) == 1)
}

function esFigura_(carta) {
    return (
        choose True when (valor(carta) == 10 || valor(carta) == 11 || valor(carta) == 12) 
               False otherwise
        )
}

function esDeOro_(carta) {
    return (palo(carta) == Oro)
}

function tieneUnNumeroMasGrande_Que_(carta1, carta2) {
    return (valor(carta1) > valor(carta2))
}

function valorParaEnvidoDe_(carta) {
    return (
        choose 0 when (esFigura_(carta))
               valor(carta) otherwise
        )
}

function mayorValorEntre_Y_(carta1, carta2) {
    return (choose valor(carta1) when(
                valorParaElEnvidoDe_(carta1) > valorParaElEnvidoDe_(carta2)
            )
                   valor(carta2) otherwise
    )
}

function sumaParaElEnvidoCon_Y_(carta1, carta2) {
    return (valorParaElEnvidoDe_(carta1) + valorParaElEnvidoDe_(carta2))
}

function sonMejores_Y_Que_Y_(carta1, carta2, carta3, carta4) {
    return (sumaParaElEnvidoCon_Y_(carta1, carta2) > sumaParaElEnvidoCon_Y_(carta3, carta4))
}

/* --- Ejercicio 4 --- */
type Celda is record {
/*
PROPÓSITO: Modelar una celda del tablero
INV.REP.: Los números son todos >=0
*/
    field cantidadDeAzules // tipo: Número
    field cantidadDeNegras // tipo: Número
    field cantidadDeRojas // tipo: Número
    field cantidadDeVerdes // tipo: Número
}

function celdaActual() {
    return (
        Celda(
            cantidadDeAzules <- nroBolitas(Azul), 
            cantidadDeNegras <- nroBolitas(Negro), 
            cantidadDeRojas <- nroBolitas(Rojo),
            cantidadDeVerdes <- nroBolitas(Verde)
        )
    )
}

procedure EscribirEnCelda_(celdaAEscribir) {
/*
    PROPOSITO: Escribe la celda **celdaAEscribir** en la celda actual
    PARAMETROS: celdaAEscribir: Celda
    PRECONDICION: La celda actual debe estar vacía
*/
    Poner_De_(cantidadDeAzules(celdaAEscribir), Azul)
    Poner_De_(cantidadDeRojas(celdaAEscribir), Rojo)
    Poner_De_(cantidadDeNegras(celdaAEscribir), Negro)
    Poner_De_(cantidadDeVerdes(celdaAEscribir), Verde)
}

function tienenMismaCantidadDeRojas_Y_(celda1, celda2) {
/*
    PROPOSITO: Indica se la las celdas dadas tienen la misma cantidad de bolitas rojas
    PARAMETROS:
        - celda1: Celda - Celda a comparar
        - celda2: Celda - Celda a comparar
    PRECONDICION: Ninguna
    TIPO: Booleano
*/
    return (cantidadDeRojas(celda1) == cantidadDeRojas(celda2))
}

// --- Ejercicio 5 --- //
type Persona is record {
/*
    PROPOSITO: Modelar una persona
    INV.REP: 
        - **dni** no es vacio y tiene 8 caracteres de longitud
        - **domicilio** no es vacio
*/
    field dni           // String
    field domicilio     // String
    field esDonante     // Booleano
}

function sonConvivientes(persona1, persona2) {
/*
    PROPOSITO: Indica si ambas personas comparten domicilio
    PARAMETROS: 
        - persona1: Persona
        - persona2: Persona
    PRECONDICION: Ninguna
    TIPO: Booleano
*/
    return (domicilio(persona1) == domicilio(persona2))
}

function personaNacidaDe_(madre) {
/*
    PROPOSITO: Describe a una nueva persona nacida de **madre**
    PARAMETROS:
        - madre: Persona - Madre de la nueva persona nacida
    PRECONDICION: **madre** debe tener un domicilio valido asignado
    TIPO: Persona
*/
    return (
        Persona(
            dni <- ""
            domicilio <- domicilio(madre)
            esDonante <- False
        )
    )
}

function persona_RegistradaCon_(personaIndocumentada, dniAAsignar) {
/*
    PROPOSITO: Asigna el un DNI a la persona dada
    PARAMETROS:
        - personaIndocumentada: Persona - Persona a la que se le va a asignar DNI
        - dniAAsignar: String - DNI a asignar a la persona
    PRECONDICION: 
        - **personaIndocumentada** no debe tener DNI asignado
        - **dniAAsignar** debe ser un DNI valido. Un dni valido es aquel que tiene 8 digitos numericos
    TIPO: Persona
*/
    return (Persona(personaIndocumentada | dni <- dniAAsignar))
}

function persona_ConDomicilioNuevoEn_(personaACambiar, domicilioAAsignar) {
/*
    PROPOSITO: Asigna el domicilio dado a la persona indicada
    PARAMETROS: 
        - personaACambiar: Persona - Es la persona a modificarle el domicilio
        - domicilioAAsignar: String - Es el domicilio a asignarle a la persona
    PRECONDICION:
        - **domicilioAAsignar** debe ser un domicilio válido. Un domicilio válido es aquel que no es vacio
*/
    return (Persona(personaACambiar | domicilio <- domicilioAAsignar))
}
```
