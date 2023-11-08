# Memoria y Caché

1. La biblioteca de la escuela de magia Howards está en una habitación secreta donde acceden la profesora Hooch solo cuando alguna persona necesita estudiar alg´un hechizo. Adem´as de que acceder a esa habitacion le lleva mucha energıa maagica, estos libros son tan especiales que no pueden retirarse de esa habitacion. Entonces Hooch hace una copia de las paginas que le han pedido antes de salir de ahi.

    a. Suponer que Hermione va el lunes a buscar el primer hechizo del libro monstruoso de los monstruos, y el martes vuelve en busqueda del segundo hechizo del mismo libro, ¿cuantas veces la profesora Hooch entra a la habitacion secreta?

   - La profesora Hooch entra 2 veces a la habitación secreta

    b. Suponer que el mi´ercoles Harry pide el hechizos de la pagina 3 del mismo libro, ¿como puede Hooch ahorrar su energıa magica?

   - Puede hacerlo dejando el libro a mano

    c. La profesora McGonnagal la autoriza a Hooch a hacer copias de los libros completos que les han pedido para tenerlos en su escritorio y que puedan leerlos allı. Si ella lo hiciera, ¿qu´e libros tendrıa en su oficina?

   - Tendría el libro monstruoso de los monstruos

## Correspondencia Asociativa

4. Suponer una memoria principal de 32 celdas de un byte y una memoria caché con 4 lineas y capacidad de almacenar un bloque de 4 celdas en cada linea.

    (a) ¿Cuantos bloques tiene la memoria principal?

   - 32 bloques en memoria principal.Se pueden almacenar 4 celdas en cada linea. Hay 4 lineas. Entonces: $\dfrac{32}{4}$ = $\dfrac{2^5}{2^2}$ = $2^3$ = 8

    (b) ¿Que tamaño tiene el tag?

   - Se usan 3 bits para el tag

    (c) ¿Que capacidad total de datos debe tener la caché?

    - Cada dato se conforma de 5 bits, 3 para el tag y 2 para el indice. Sabiendo esto, la cache debe tener $(5*4)*4 = 80$ bits

5. Suponer una memoria principal con direcciones de 16 bits y una memoria cache con 256 lineas y capacidad de almacenar un bloque de 4 celdas en cada linea. Si la CPU pide la lectura de la celda FA32, ¿Que tag se debe buscar en la cache?

   - **Forma intuitiva**: Sabiendo que hay 4 celdas por bloque y que para referenciar 4 celdas solo se requieren 2 bit, el tag son los 14 restantes
   - **Fórmula**: $\dfrac{2^16}{2^2}$ = $2^14$

6. Suponer una memoria caché que tiene el siguiente contenido:
<table>
    <tr>
        <td>345</td>
        <td>00112233445566778899AABBCCDDEEFF</td>
    </tr>
    <tr>
        <td>345</td>
        <td>FFEEDDCCBBAA99887766554433221100</td>
    </tr>
    <tr>
        <td>345</td>
        <td>00112233445566778899AABBCCDDEEFF</td>
    </tr>
    <tr>
        <td>345</td>
        <td>FFEEDDCCBBAA99887766554433221100</td>
    </tr>
<table>

    (a) Si las direcciones de memoria tienen 16 bits y el tag es de 12 bits entonces hay 4 bits que se usan para distinguir la palabra/índice. ¿Cuántas celdas entran en un bloque?
   - 4 celdas de índice pueden referenciar 16 celdas (2<sup>4</sup>)

    (b) ¿Está cacheada la celda 3451?

   - Sí, está cacheado

    (c) ¿Qué valor retorna la caché para esa celda?

   - Retorna: 44556677
  
7. El chip 80286 (fabricado entre 1982 y 1993) tenıa un bus de datos de 16 bits, pero un bus de direcciones de 24 bits, lo que lo hacıa la primera arquitectura de Intel capaz de soportar 16Mb de RAM. Suponer la siguiente memoria cache, adaptada a dicha arquitectura:
   
(a) 32 celdas por bloque

(b) 256 lineas

(c) correspondencia asociativa

**Determinar**:

a. ¿Como se divide una direccion de memorıa en tag y palabra?

- $\dfrac{2^{24}}{2^{8}}$ = $2^{16}$. La dirección de 24 bits se divide usando 16 para el tag y 8 para el indice

b. ¿Como se decide si la direccion FAFAFA esta en cache?

- ???

c. ¿Cuantas celdas contiene dicha memoria cache?

- cantCeldasPorBloque * cantLineas = $32 * 256 = 8192$ celdas

## Correspondencia Directa

Para los ejercicios de esta seccion se asume que las memorias cache tienen correspondencia directa
8. Suponiendo una memoria cache de 4 lineas y 4 celdas por bloque, calcular aciertos y fallos en el escenario del ejercicio 2.
   
9.  Considerar una computadora con una memoria de 64 celdas de un byte y una memoria cache con 4 lineas y bloques de 8 celdas por linea.

    (a) Que tamaño tienen las direcciones de estamemoria?

    (b) ¿Cuantos bits de una direccion se destinan a: tag, linea y palabra?

    (c) Explicar lo anterior usando una direccion como ejemplo.
    
10. Considerando el escenario del ejercicio 9, mencionar el tag y la linea de la cache a la que corresponde cada dirección:

| dir    | tag | nroLinea |
| ------ | --- | -------- |
| 111000 |     |          |
| 011001 |     |          |
| 111111 |     |          |
| 101000 |     |          |
| 101001 |     |          |

11. Considerando el escenario del ejercicio 9, listar todas las direcciones en la misma liınea que la direccion 111000.

12. Suponer que la cach´e descripta en el ejercicio 9 esta vacia, y que se realizan lecturas de direcciones en el siguiente orden. Determinar para cada lectura si esta produjo un fallo o un acierto.
