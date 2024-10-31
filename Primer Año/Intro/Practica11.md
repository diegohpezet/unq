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

// --- Ejercicio 5 --- //
function primerasTresCartasDeLaTira_(tiraDeCartas) {
/*
    PROPOSITO: Describe las primeras tres cartas de una tira de cartas
    PARAMETROS:
        * tiraDeCartas: Lista de Cartas
    TIPO: Lista de Cartas
    PRECONDICION: Debe haber al menos tres cartas en **tiraDeCartas**
*/
    aux := tiraDeCartas
    listaHastaAhora := []
    repeat (3) {
        listaHastaAhora := listaHastaAhora ++ [ primero(aux) ]
        aux := resto(aux)
    }

    return (listaHastaAhora)
}

// --- Ejercicio 6 --- //
type Direccion is variant {
    case Adelante {}
    case Derecha {}
    case Izquierda {}
}

type Pista is record {
    field tramos    // Lista de Direcciones
}

function sigueRectaEn_(pista) {
/*
    PROPOSITO: Indica si el siguiente tramo de una pista dada es recta
    PARAMETROS:   
        * pista: Pista - Pista a evaluar
    TIPO: Booleano
    PRECONDICION: Debe haber al menos dos tramos en la pista
*/
    return (primero(tramos(pista)) == primero(resto(tramos(pista))))
}

function sigueCurvaADerechaEn_(pista) {
/*

*/
    return (primero(resto(tramos(pista))) == Derecha)
}

function sigueCurvaAIzquierdaEn_(pista) {
/*

*/
    return (primero(resto(tramos(pista))) == Derecha)
}

function hayUnSiguienteTramoEn_(pista) {
/*

*/
    return (not esVacia(pista) && )
}


// --- Ejercicio 6 --- //
function listaCon_Repetido_Veces(elemento, cantidadDeVeces) {
/*
    PROPOSITO: Describe una lista que tienen tantos elementos como la cantidad de veces dada, en donde el elemento es el dado
    PARAMETROS: 
        * elemento: Elemento - Elemento que va a completar la lista
        * cantidadDeVeces: Numero - Cantidad de veces que se va a poner ese elemento
    TIPO: Lista de elementos
    PRECONDICION: Ninguna
*/    
    listaHastaAhora := []
    repeat (cantidadDeVeces) {
        listaHastaAhora := listaHastaAhora ++ [ elemento ]
    }

    return(listaHastaAhora)
}

// --- Ejercicio 7 --- //

function listaDesde_Hasta_(valorInicial, valorFinal) {
/*
	PROPOSITO: Describe una lista que va del **valorInicial** al **valorFinal**
	PARAMETROS:
		* valorInicial: Elemento - Primer valor de la lista
		* valorFinal: Elemento - Primer valor de la lista
	TIPO: Lista

*/
	return [valorInicial .. valorFinal]
}

// --- Ejercicio 8 --- //
function longitudDe_(lista) {
/*
	PROPOSITO: Describe la longitud de la lista dada
	PARAMETROS:
		* lista: Lista de Elementos - Lista de elementos a evaluar
	TIPO: Numero
	PRECONDICION: Ninguna
*/
	contador := 0
	foreach elemento in lista {
		contador := contador + 1
	}

	return (contador)
}

// --- Ejercicio 9 --- //
function sumatoriaDe_(listaNumerica) {
/*
	PROPOSITO: Describe la suma de todos los elementos de la lista
	PARAMETROS:
		* listaNumerica: Lista de Numeros - Lista a procesar
	TIPO: Numero
	PRECONDICION: La lista no debe estar vacía
*/
	sumatoria := 0
	foreach numero in listaNumerica {
		sumatoria := sumatoria + numero
	}

	return (sumatoria)
}

// --- Ejercicio 10 --- //
function productoriaDe_(listaNumerica) {
/*
	PROPOSITO: Describe el producto entre todos los elementos de la lista
	PARAMETROS:
		* listaNumerica: Lista de Numeros - Lista a procesar
	TIPO: Numero
	PRECONDICION: La lista no debe estar vacía
*/
    productoria := 1
    foreach numero in listaNumerica {
        productoria := productoria * numero
    }

    return (productoria)
}

// --- Ejercicio 13 --- //
function opuestasDe_(listaDeDirecciones) {
/*
    PROPOSITO: Describe una lista de direcciones opuestas a las del listado de direcciones dado
    PARAMETROS:
        * listaDeDirecciones: Lista de Direcciones
    TIPO: Lista de Direcciones
    PRECONDICION: La lista no debe estar vacia
*/
    listaNueva := []
    foreach direccion in listaDeDirecciones {
        listaNueva := listaNueva ++ [ opuesto(direccion) ]
    }

    return (listaNueva)
}

// --- Ejercicio 14 --- //
function siguientesDe_(listaDeDirecciones) {
/*
    PROPOSITO: Describe una lista de direcciones siguientes a las del listado de direcciones dado
    PARAMETROS:
        * listaDeDirecciones: Lista de Direcciones
    TIPO: Lista de Direcciones
    PRECONDICION: La lista no debe estar vacia
*/

    listaNueva := []
    foreach direccion in listaDeDirecciones {
        listaNueva := listaNueva ++ [ siguiente(direccion) ]
    }

    return (listaNueva)
}
```