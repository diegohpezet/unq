# Practica 11 | Listas

```js
// --- Ejercicio 1 --- //
function singularCon_(elemento) {
/*
    PROPOSITO: Describe una lista que solo tiene el elemento dado
    PARAMETROS:
        * elemento: Elemento - Elemento a guardar en la lista
    PRECONDICION: Ninguna
    TIPO: Lista de elementos
*/
    return ([elemento])
}

// --- Ejercicio 2 --- //
function segundoDe_(lista) {
/*
    PROPOSITO: Describe el segundo elemento de una lista
    PARAMETROS:
        - lista: Lista de elementos - Listado de elementos a procesar
    PRECONDICION:
        - **lista** debe tener al menos dos elementos
    TIPO: Elemento
*/
    return(primero(resto(lista)))
}

// --- Ejercicio 3 --- //
function esSingular_(lista) {
/*
    PROPOSITO: Indica si la lista dada es singular
    PARAMETROS:
        * lista: Lista de elementos - Listado de elementos a evaluar
    PRECONDICION: Ninguna
    TIPO: Booleano
*/
    return (not esVacía(lista) && esVacía(resto(lista)))
}

// --- Ejercicio 4 --- //
function primeraCartaDeLaMano_(manoDeCartas) {
/*
    PROPOSITO: Describe la primer carta de la mano de cartas dada
    PARAMETROS:
        - manoDeCartas: Lista de cartas - Mano de cartas recibida
    TIPO: Carta
    PRECONDICION: Ninguna
*/
    return (primero(manoDeCartas))
}

function segundaCartaDeLaMano_(manoDeCartas) {
/*
    PROPOSITO: Describe la segunda carta de la mano de cartas dada
    PARAMETROS:
        - manoDeCartas: Lista de cartas - Mano de cartas recibida
    TIPO: Carta
    PRECONDICION: Ninguna
*/
    return (siguiente(primero(manoDeCartas)))
}

function ultimaCartaDeLaMano_(manoDeCartas) {
/*
    PROPOSITO: Describe la ultima carta de la mano de cartas dada
    PARAMETROS:
        - manoDeCartas: Lista de cartas - Mano de cartas recibida
    TIPO: Carta
    PRECONDICION: Ninguna
*/    
    return (primero(resto(resto(manoDeCartas))))
}

function laMano_LuegoDeRobarUnaCartaDe_(mano, mazo) {
/*
    PROPOSITO: Describe la mano dada luego de robar una carta del mazo
    PARAMETROS:
        - mano: Lista - Mano de cartas
        - mazo: Lista - Mazo de cartas
    PRECONDICION: Ninguna
    Tipo: Lista de cartas
*/
    return (mano ++ primero(mazo))
}

function laMano_LuegoDeJugarUnaCarta(manoDeCartas) {
/*
    PROPOSITO: Describe la mano de cartas dada luego de jugar una carta
    PARAMETROS:
        - manoDeCartas: Lista de cartas
    TIPO: Lista de cartas
    PRECONDICION: Ninguna
*/
    return (resto(manoDeCartas))
}

function laMano_LuegoDeJugarLaSegundaCarta(manoDeCartas) {
/*
    PROPOSITO: Describe la mano de cartas dada luego de haberse jugado la segunda carta
    PARAMETROS:
        - manoDeCartas: Lista de cartas
    TIPO: Lista de cartas
    PRECONDICION: Ninguna
*/
    primerCarta := primero(manoDeCartas)
    manoSinDosPrimerasCartas := resto(resto(manoDeCartas))
    
    return (primerCarta ++ manoSinDosPrimerasCartas)
}
```