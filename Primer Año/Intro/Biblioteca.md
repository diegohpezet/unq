# Biblioteca

```js
/* --- Procedimientos ---*/

// Poner de a muchas
procedure Poner_De_Color_(cantidadAPoner, colorAPoner) {
	/*
		PROPOSITO: Coloca tantas bolitas como **cantidadAPoner**
		de color **colorAPoner** en la celda actual
		PARAMETROS:
			- cantidadAPoner: Numero- Cantidad de bolitas a poner
			- colorAPoner: Color - Color de las bolitas a poner
		PRECONDICION: Ninguna
	*/
	repeat(cantidadAPoner) {
		Poner(colorAPoner)
	}
}

// Poner si se cumple cierta condicion
procedure Poner_Si_(color, condicion) {
/*
	PROPOSITO: Pone en la celda actual una bolita de color **color**
	PARAMETROS: 
		- color: Color - Color de la bolita a poner
		- condicion: Booleano - Condicion que se debe cumplir para colocar la bolita
	PRECONDICION: Debe cumplirse la condicion **condicion**	
*/
	if (condicion) {
		Poner(color)
	}
}

// Mover tantas veces como se desee en una direccion
procedure Mover_VecesAl_(cantidadAMover, direccionAMover) {
	/*
		PROPOSITO: Desplaza el cabezal tantas celdas como **cantidadAMover** 
		hacia **direccionAMover**
		PARAMETROS:
			- cantidadAMover: Numero - Cantidad de celdas a desplazar el cabezal
			- direccionAMover: Direccion - Direccion hacia la cual desplazar el cabezal
		PRECONDICION: Deben existir **cantidadAMover** celdas hacia **direccionAMover**
	*/
	repeat(cantidadAMover) {
		Mover(direccionAMover)
	}
}

// Sacar de a muchas
procedure Sacar_DeColor_(cantidadASacar, colorASacar) {
	/*
		PROPOSITO: Saca tantas bolitas como **cantidadASacar**
		de color **colorASacar** de la celda actual
		PARAMETROS:
			* cantidadASacar: Numero - Cantidad de bolitas a sacar
			* colorASacar: Color - Color de las bolitas a sacar
		PRECONDICION: Deben existir **cantidadASacarr** bolitas
		de color **colorASacar** en la celda actual
	*/
	repeat(cantidadASacar) {
		Sacar(colorASacar)
	}
}

// Sacar todas las bolitas de un color
procedure SacarTodasLasDeColor_(colorASacar) {
	/*
		PROPOSITO: Saca todas las bolitas de color **colorASacar**
		de la celda actual
		PARAMETROS:
			- colorASacar: Color - Color de las bolitas a sacar
		PRECONDICION: Debe haber al menos una bolita color **colorASacar**
		en la celda actual
	*/
	repeat(nroBolitas(colorASacar)) {
		Sacar(colorASacar)
	}
}

// Sacar si se cumple cierta condicion
procedure Sacar_Si_(color, condicion) {
/*
	PROPOSITO: Saca de la celda actual una bolita de color **color**
	PARAMETROS: 
		- color: Color - Color de la bolita a sacar
		- condicion: Booleano - Condicion que se debe cumplir para sacar la bolita
	PRECONDICIONES: 
		- Debe cumplirse la condicion **condicion**
		- Debe existir al menos una bolita de color **color**	
*/
	if (condicion) {
		Sacar(color)
	}
}

procedure VaciarCelda() {
	/*
		PROPOSITO: Saca todas las bolitas de la celda actual. En caso de no
		haber ninguna bolita, no hace nada
		PRECONDICION: Ninguna
	*/
	SacarTodasLasDeColor_(Rojo)
	SacarTodasLasDeColor_(Verde)
	SacarTodasLasDeColor_(Azul)
	SacarTodasLasDeColor_(Negro)
}

procedure MoverEnDiagonalHacia_Y_(direccion1, direccion2) {
/*
	PROPOSITO: Mueve el cabezal hacia la celda lindante en diagonal hacia **direccion1**
	y **direccion2**
	PARAMETROS:
		- direccion1: Direccion - Direccion que compone una diagonal
		- direccion2: Direccion - Direccion que compone una diagonal
	PRECONDICION:
		- **direccion1** y **direccion2** no pueden ser iguales ni opuestas
		- Debe existir una celda hacia **direccion1** al igual que hacia el **direccion2**
*/
	Mover(direccion1) Mover(direccion2)
}

// Mueve si se cumple cierta condicion
procedure Mover_Si_(direccion, condicion) {
/*
	PROPOSITO: Mueve el cabezal hacia el **direccion**
	PARAMETROS: 
		- direccion: Direccion - Direccion hacia la cual mover el cabezal
		- condicion: Booleano - Condicion que se debe cumplir para mover el cabezal
	PRECONDICIONES: 
		- Debe cumplirse la condicion **condicion**
		- Debe existir al menos una celda hacia el **direccion**	
*/
	if (condicion) {
		Mover(direccion)
	}
}

// Ir a una esquina
procedure IrAEsquinaAl_Y_(primeraDireccion, segundaDireccion) {
	/*
		PROPOSITO: Situa el cabezal en la esquina en direcciones
		**primeraDireccion** y **segundaDireccion**
		PARAMETROS:
			- primerDireccion: Direccion - Una de las direcciones que conforman la esquina
			- segundaDireccion: Direccion - Segunda direccion que conforma la esquina
		PRECONDICION: Ninguna
	*/
	IrAlBorde(primeraDireccion)
	IrAlBorde(segundaDireccion)
}

// Copia las bolitas de un color en alguna direccion
procedure Copiar_Al_(colorACopiar, direccionAPegar) {
	/*
		PROPOSITO: "Copia y pega" las bolitas de color **color** en
		la celda lindante al **dirección**
		PRECONDICION: Debe existir una celda hacia **direccion**
		PARAMETROS:
			* colorACopiar: Color - Color a copiar
			* direccionAPegar: Direccion - Dirección de la celda
			en la que se van a colocar las bolitas
	*/
	cantBolitas := nroBolitas(colorACopiar)
		
	Mover(direccionAPegar)
  SacarTodasLasDeColor_(colorACopiar)
  Poner_De_Color_(cantBolitas, colorACopiar)
    
  Mover(opuesto(direccionAPegar)
}

// Copiar la celda actual en alguna direccion
procedure CopiarCeldaAl_(direccion) {
    /*
        PROPOSITO: Copia los contenidos de la celda actual a la celda lindante al 
        **direccion**
        PRECONDICION: Debe existir una celda hacia el **direccion**
        PARAMENTROS:
            * direccion: Direccion - Direccion de la celda en donde se va a "pegar"
                el contenido de la celda actual
    */
    indicadorDeColor := minColor()

    while (indicadorDeColor /= maxColor()) {
	    Copiar_Al_(colorACopiar, direccion)
	    indicadorDeColor := siguiente(indicadorDeColor)
    }
    Copiar_Al_(colorACopiar, direccion)
}
```

```js
/* --- Funciones ---*/

// La celda está vacia
function esCeldaVacia() {
/*
	PROPOSITO: Indica si la celda actual se encuentra vacía
	PRECONDICION: Ninguna
	TIPO: Booleano
*/
	return (
		not hayBolitas(Azul) 
		&& 
		not hayBolitas(Negro) 
		&& 
		not hayBolitas(Rojo)
		&&
		not hayBolitas(Verde)	 
	)
}

// Hay al menos una de cada color
function hayAlMenosUnaDeCada() {
/*
	PROPOSITO: Indica si la celda actual tiene al menos una bolita de cada color
	PRECONDICION: Ninguna
	TIPO: Booleano
*/
	return (
		hayBolitas(Azul) 
		&& 
		hayBolitas(Negro) 
		&& 
		hayBolitas(Rojo)
		&&
		hayBolitas(Verde)	
	)
}

// Hay al menos una bolita
function esCeldaConBolitas() {
/*
	PROPOSITO: Indica si en la celda actual hay al menos una bolita de cualquier color
	PRECONDICION: Ninguna
	TIPO: Booleano
*/
	return (
		not hayBolitas(Azul) 
		|| 
		not hayBolitas(Negro) 
		|| 
		not hayBolitas(Rojo)
		||
		not hayBolitas(Verde)	
	)
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
	if (numero1 > numero2) {
		minimo := numero2
	}
	
	return (minimo)
}

function maximoEntre_Y_(valor1, valor2) {
	/*
		PROPOSITO: Describe el valor mas pequeño entre **valor1** y **valor2**
		PRECONDICION: Ninguna
		PARAMETROS: 
			* numero1: Expresion - Valor a comparar
			* numero2: Expresion - Valor a comparar
		TIPO: Expresion
	*/
	
	maximo := numero1
	if (numero1 < numero2) {
		maximo := numero2
	}
	
	return (maximo)
}

function distanciaAlBorde_(direccionDelBorde) {
	/*
		PROPOSITO: Describe la cantidad de celdas que hay
		entre la celda actual y el borde al **direccionDelBorde**
		PRECONDICION: Ninguna
		TIPO: Numero
	*/
	cantCeldas := 0
	
	while (puedeMover(direccion)) {
		Mover(direccion)
		cantCeldas := cantCeldas + 1
	}
	
	return (cantCeldas)
}

function coordenadaX() {
	/*
		PROPOSITO: Indica la coordenada de la columna de la	celda actual
		PRECONDICION: Ninguna
		TIPO: Numero
	*/
	coordenada := 0
	
	while (puedeMover(Oeste)) {
		coordenada := coordenada + 1
	}
	
	return (coordenada)
}

function coordenadaY() {
	/*
		PROPOSITO: Indica la coordenada de la fila de la celda actual
		PRECONDICION: Ninguna
		TIPO: Numero
	*/
	coordenada := 0
	
	while (puedeMover(Sur)) {
	    Mover(Sur)
		coordenada := coordenada + 1
	}
	
	return (coordenada)
}

function bordeMasLejanoEntre_Y_(direccion1, direccion2) {
/*
	PROPOSITO: Describe el borde más lejano entre dos direcciones
	PRECONDICION: La distancia al borde hacia ambas direcciones debe ser distinta
	PARAMETROS: 
		* direccion1: Direccion - Direccion a comparar
		* direccion2: Direccion - Direccion a comparar
	TIPO: Direccion
*/
    return (
        choose direccion1 when (distanciaAlBorde_(direccion1) > distanciaAlBorde_(direccion2))
        direccion2 otherwise
    )
}

function direccionConMayorDistanciaAlBorde() {
/*
    PROPOSITO: Describe la dirección hacia la cual existe
    mayor distancia al borde desde la celda actual.
    PRECONDICION: Existe una dirección hacia la cual la distancia al borde
    desde la celda actual es mayor al resto
    TIPO: Direccion
    OBSERVACION: Es un recorrido de máximos y mínimos sobre
    las direcciones, obteniendo aquella de mayor distancia al borde
*/
    direccion := minDir()
    direccionConMayorDistancia := direccion
    
    while (direccion /= maxDir()) {
        direccionConMayorDistancia := bordeMasLejanoEntre_Y_(direccion, direccionConMayorDistancia)
        direccion := siguiente(direccion)
    }
   direccionConMayorDistancia := bordeMasLejanoEntre_Y_(direccion, direccionConMayorDistancia)
    
    return (direccionConMayorDistancia)
}

function nroFilas() {
	/*
		PROPOSITO: Indica la cantidad de filas que posee el tablero
		PRECONDICIÓN: Ninguna
		TIPO: Numero
		OBSERVACIÓN: Es un recorrido de acumulacion por celdas sobre una columna, el
		cual se incrementa en 1 por cada celda recorrida
	*/
    return (coordenadaY() + 1)
}

function nroColumnas() {
	/*
		PROPOSITO: Indica la cantidad de columnas que posee el tablero
		PRECONDICIÓN: Ninguna
		TIPO: Numero
		OBSERVACIÓN: Es un recorrido de acumilación de celdas sobre una fila, el cual
		incrementa su contador en 1 por cada celda de la misma
	*/
    return (coordenadaX() + 1)
}


function nroVacias() {
/*
	PROPOSITO: Indica la cantidad de celdas vacías que existen en el tablero
	PRECONDICIÓN: Ninguna
	TIPO: Numero
	OBSERVACIÓN: Es un recorrido de acumulación por celdas del tablero, el cual
	incrementa en 1 por cada celda vacía del tablero
*/
	cantidadDeCeldasVacias := 0
	
	IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
	while (haySiguienteCeldaEnUnRecorridoAl_Y_(Este,Norte)) {
		cantidadDeCeldasVacias := choose cantidadDeCeldasVacias + 1 when (hayCeldaVacia())
																		 cantidadDeCeldasVacias otherwise
		IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
	}
	cantidadDeCeldasVacias := choose cantidadDeCeldasVacias + 1 when (hayCeldaVacia())
																		 cantidadDeCeldasVacias otherwise
	return (cantidadDeCeldasVacias)
}

function cantidadDeCeldasConBolitasDeColor_(color) {
/*
	PROPOSITO: Describe la cantidad de celdas que contienen al menos una bolita
	de color **color** 
	PRECONDICION: Ninguna
	PARAMETROS: 
		* color: Color - Color de las bolitas que tiene que haber en una celda
		para que se sume a la cantidad total
	TIPO: Numero
	OBSERVACION: Es un recorrido de acumulacion por celdas del tablero, el cual
	se incrementa en 1 por cada celda con bolitas de color **color** en el tablero
*/
	cantidadActual := 0
	IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
	while (haySiguienteCeldaEnUnRecorridoAl_Y_(Este,Norte)) {
		cantidadActual := choose cantidadActual + 1 when (hayBolitas(color))
																		 cantidadActual otherwise
		IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
	}
		cantidadActual := choose cantidadActual + 1 when (hayBolitas(color))
														 cantidadActual otherwise
	return (cantidadActual)
}

function nroBolitasTotalDeColor_(colorAContar) {
/*
	PROPOSITO: Describe la cantidad de bolitas de color **colorAContar**
	que haya en el tablero
	PRECONDICION: Ninguna
	PARAMETROS: 
		* colorAContar: Color - Color de las bolitas a contar
	TIPO: Numero
	OBSERVACION: Es un recorrido de acumulacion por celdas del tablero, el cual
	se incrementa segun cantidad de bolitas color **colorAContar** haya por cada celda
*/
	cantidadDeColor := 0
	
	IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
	while (haySiguienteCeldaEnUnRecorridoAl_Y_(Este,Norte)) {
		cantidadDecolor := cantidadDeColor + nroBolitas(colorAContar)
		IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
	}
	cantidadDecolor := cantidadDeColor + nroBolitas(colorAContar)

	return (cantidadDeColor)
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

```js
/* --- Recorridos --- */
procedure IrAPrimeraCeldaEnUnRecorridoAl_Y_(dirPrincipal, dirSecundaria) {
/*
    PROPOSITO: Coloca el cabezal al inicio de un recorrido en dirección
    **dirPrincipal** y **dirSecundaria**
    PRECONDICION: **dirPrincipal** y **dirSecundaria** no pueden ser
    iguales ni opuestas
    PARAMETROS:
        * dirPrincipal: Direccion - Direccion principal del recorrido
        * dirSecundaria: Direccion - Direccion secundaria del recorrido
*/
    IrAlBorde(opuesto(dirPrincipal))
    IrAlBorde(opuesto(dirSecundaria))
}

function haySiguienteCeldaEnUnRecorridoAl_Y_(dirPrincipal, dirSecundaria) {
/*
    PROPOSITO: Indica si hay una celda siguiente en un recorrido hacia
    **dirPrincipal** y **dirSecundaria**
    PRECONDICION: **dirPrincipal** y **dirSecundaria** no pueden ser
    iguales ni opuestas
    PARAMETROS:
        * dirPrincipal: Direccion - Direccion principal del recorrido
        * dirSecundaria: Direccion - Direccion secundaria del recorrido
*/    
    return (puedeMover(dirPrincipal) || puedeMover(dirSecundaria))
}

procedure IrASiguienteCeldaEnUnRecorridoAl_Y_(dirPrincipal, dirSecundaria) {
/*
    PROPOSITO: Coloca el cabezal en la siguiente celda de un recorrido 
    en dirección **dirPrincipal** y **dirSecundaria**
    PRECONDICION: **dirPrincipal** y **dirSecundaria** no pueden ser
    iguales ni opuestas
    PARAMETROS:
        * dirPrincipal: Direccion - Direccion principal del recorrido
        * dirSecundaria: Direccion - Direccion secundaria del recorrido
*/
    if (puedeMover(dirPrincipal)) {
	    Mover(dirPrincipal)
	  } else {
		  Mover(dirSecundaria)
		  IrAlBorde(opuesto(dirPrincipal))
	  }
}
```

```js
/* -- Tipos de recorridos -- */

// Procesamiento
/*
	...
	OBSERVACION: Es un recorrido de procesamiento
	sobre elementos en un grupo
	haciendo ...
*/
procedure RecorridoDeProcesamiento() {
   IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
    while (haySiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)) {
        ProcesarElemento()
        IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
    }
    ProcesarElemento()
}

// Acumulacion
function recorridoAcumulacion() {
	contador := 0
	
	IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
	while (haySiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)) {
		contador := contador + unoSi_CeroSiNo(condicion)
		IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
	}
	contador := contador + unoSi_CeroSiNo(condicion)
	
	return (contador)
}

// Busqueda sabiendo que hay elemento
procedure RecorridoDeBusquedaSabiendo() {
/*
	...
	OBSERVACION: Es un recorrido de busqueda
	sobre elementos 
*/
    IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
    while (not encontreLoQueBusco()) {
        IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
    }
    FinalizarRecorrido()
}


// Busqueda sin saber si hay elemento
function buscarSinSaberQueEsta() {
/*
	...
	OBSERVACION: Es un recorrido de busqueda sin saber si hay
	sobre elementos en un grupo
	buscando ...
*/		
    IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
    while (haySiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte) && not encontreLoQueBusco()) {
        IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
    }
    return (choose True when (encontreLoQueBusco()) False otherwise)
}

// Maximo - Minimo
funcion maximoOMinimo() {
    elMas:= valorActual()
    
    IrAPrimeraCeldaEnUnRecorridoAl_Y_(Este, Norte)
    while (haySiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)) {
        IrASiguienteCeldaEnUnRecorridoAl_Y_(Este, Norte)
        elMas:= maximoEntre_Y_(elMas, valorActual())
    }
    
    return (elMas)
}

function sobreLista(lista) {
    listaRestante := lista
    while (not esVacia(listaRestante)) {
	// Procesar primero(listaRestante)
	listaRestante := resto(listaRestante)
    }
    return (algo)
}
```

```js
Elementos Sobre Los Que Se Recorre
========================================


Sobre Celdas De La Fila/Columna
----------------------------------
IniciarRecorrido() = irAlBorde(...)
quedanElementosPorRecorrer() = púedeMover(...)
IrASiguienteElemento() = Mover(...)



Sobre Filas/Columnas Del Tablero 
----------------------------------
IniciarRecorrido() = irAlBorde(...)
quedanElementosPorRecorrer() = púedeMover(...)
IrASiguienteElemento() = Mover(...)



Sobre Celdas Del Tablero
---------------------------
iniciarRecorrido() = irAPrimeraCeldaEnUnRecorridoAl_Y_(...)
quedanElementosPorRecorrer() = haySiguienteCeldaEnUnRecorridoAl_Y_(...)
IrASiguienteElemento() = IrASiguienteCeldaEnUnRecorridoAl_Y_(...)



Sobre Direcciones
--------------------
iniciarRecorrido() = direcciónActual:= minDir()
quedanElementosPorRecorrer() = direcciónActual /= maxDir()
IrASiguienteElemento() = direcciónActual := siguiente(direcciónActual)



Sobre Colores
-----------------
IniciarRecorrido() = colorActual:= minColor()
quedanElementosPorRecorrer() = colorActual /= maxColor()
IrASiguienteElemento() = colorActual := siguiente(colorActual)

// Movidas raras
function seCumpleCondicionHacia_(direccion) {
/*
	PROPOSITO: Indica si se cumple la condicion en la celda inmediantamente 
	al **direccion** de la celda actual
	PRECONDICION: Ninguna
	PARAMETROS:
		* direccion: Direccion - Direccion hacia donde se encuentra la celda a evaluar
	TIPO: Booleano
*/
	seCumple := False
	if (puedeMover(direccion)) {
		Mover(direccion)
		seCumple := choose True when (**Condicion**) False otherwise
	}
	return (seCumple)
}

function seCumpleCondicionHaciaTodosLados() {
/*
	PROPOSITO: Indica si se cumple la condicion en todas las celdas lindantes
	a la celda actual
	PRECONDICION: Ninguna
	TIPO: Booleano
*/
	direccion := minDir()
	while (direccion /= maxDir() && not(seCumpleCondicionHacia_(direccion))) {
		direccion := siguiente(direccion)
	} 
	return (seCumpleCondicionHacia_(direccion))
}
```

```js
/* --- Recorridos sobre listas --- */

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

function mínimoElementoDe_(lista) {
/*
    PROPOSITO: Describe el elemento mas chico de la lista
    PARAMETROS:
        - lista: Lista de elementos - Lista a recorrer
    TIPO: Elemento
    PRECONDICION: 
        - Debe haber al menos un elemento en la lista
    OBSERVACION: Es un recorrido de máximo - mínimo por elementos de la lista dada
*/
    mínimoVisto := primero(lista)
    listaRestante := resto(lista) 
    while (not esVacía(listaRestante)) {
        mínimoVisto := mínimoEntre_y_(mínimoVisto, primero(listaRestante))
        listaRestante := resto(listaRestante)
    }
    return (mínimoVisto)
}

function esSingular_(lista) {
/*
    PROPOSITO: Indica si la lista dada es singular
    PARAMETROS:
        * lista: Lista - Listado de elementos a evaluar
    PRECONDICION: Ninguna
    TIPO: Booleano
*/
    return (not esVacía(lista) && esVacía(resto(lista)))
}

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
```
