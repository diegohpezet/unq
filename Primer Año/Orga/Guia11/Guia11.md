# Memoria y Caché

1. La biblioteca de la escuela de magia Howards está en una habitación secreta donde acceden la profesora Hooch solo cuando alguna persona necesita estudiar alg´un hechizo. Adem´as de que acceder a esa habitacion le lleva mucha energıa maagica, estos libros son tan especiales que no pueden retirarse de esa habitacion. Entonces Hooch hace una copia de las paginas que le han pedido antes de salir de ahi.

a. Suponer que Hermione va el lunes a buscar el primer hechizo del libro monstruoso de los monstruos, y el martes vuelve en busqueda del
segundo hechizo del mismo libro, ¿cuantas veces la profesora Hooch entra a la habitacion secreta?
- La profesora Hooch entra 2 veces a la habitación secreta

b. Suponer que el mi´ercoles Harry pide el hechizos de la pagina 3 del mismo libro, ¿como puede Hooch ahorrar su energıa magica?

- Puede hacerlo dejando el libro a mano

c. La profesora McGonnagal la autoriza a Hooch
a hacer copias de los libros completos que les
han pedido para tenerlos en su escritorio y que
puedan leerlos all´ı. Si ella lo hiciera, ¿qu´e libros
tendr´ıa en su oficina?

- Tendría el libro monstruoso de los monstruos

## Correspondencia Asociativa

1. Suponer una memoria principal de 32 celdas de un byte y una memoria caché con 4 lineas y capacidad de almacenar un bloque de 4 celdas en cada linea.
<center>

Memoria de 32 Celdas:
| Dir    | Dato |
| ------ | ---- |
| 0x0000 | AAAA |
| 0x0001 | BBBB |
| 0x0002 | CCCC |
| ....   | .... |
| 0x002F | 2F2F |

Memoria Cache:
|Dir | Dato
00 |  |  | 
01 |  |  |
10 |  |  |
11 |  |  |

</center>
(a) ¿Cuantos bloques tiene la memoria principal?

- 32 bloques que se pueden almacenar 4 en cada linea, repartidas en 4 lineas = (32/4) = 8, siendo 2 por linea

(b) ¿Que tamaño tiene el tag?

- 32 c

(c) ¿Que capacidad total de datos debe tener la caché?

5. Suponer una memoria principal con direcciones de 16 bits y una memoria cache con 256 lineas y capacidad de almacenar un bloque de 4 celdas en cada linea. Si la CPU pide la lectura de la celda FA32, ¿Que tag se debe buscar en la cache?

- 1111 1010 0011 0010


