# Programar recorrido de arreglos

Los ejercicios de esta seccion te permitiran entender la programacion de recorridos de arreglos.
Es **importantısimo descomponer los problemas**. En general suele ser util pensar una subrutina que se encargue de procesar un solo elemento del arreglo y sea llamada desde la rutina principal

1- Implementar la rutina sumaElementos 
| sumaElementos | <!----> |
|-------|--------|
| Requiere: | Un arreglo de 5 valores en BSS(16) almacenado a partir de la celda 0x3333 |
| Modifica: | R0 |
| Retorna: | En R6, la suma de los elementos del arreglo |

```js
sumaElementos: MOV R6, 0x0000  // Sumador
               MOV R0, 0x3333  // Celda inicial del array

repetir: CMP R0, 0x3338
         JE fin
         ADD R6, [[R0]]
         ADD R0, 0x0001
         JMP repetir

fin: RET
```

2- Implementar la rutina cantElementos
| cantElementos | <!----> |
|-------|-------|
| Requiere: | Un arreglo de valores en BSS (16) almacenado a partir de la dirección que indica R0 y que finaliza con el primer elemento cuyo valor es 0x0000 |
| Modifica: | R0 |
| Retorna: | En R6 la cantidad de elementos del arreglo |

**Nota**: R0 tiene la direccion del primer elemento del arreglo y |R0| el valor de dicho elemento

```js
cantElementos: MOV R6, 0x0000  // Contador de elementos

repetir: CMP [[R0]], 0x0000
         JE fin
         ADD R0, 0x0001
         ADD R6, 0x0001
         JMP repetir

fin: RET
```

3- Escribir la rutina **copiarArreglo** en funcion de su documentacion

| copiarArreglo | <!----> |
|-------|-------|
| Requiere: | Un arreglo de valores en BSS(16) almacenados a partir de la celda 8400 y que finaliza con el primer valor FFFF |
| Modifica: | COMPLETAR |
| Retorna: | Una copia del arreglo original a partir de la celda 9400 |

```js
copiarArreglo: MOV R0, 0x8400

repetir: CMP [[R0]], 0xFFFF
         JE fin
         ADD R0, 0x0001
         MOV [0x9400], [[R0]]
         JMP fin

fin: RET
```

4- Escribir la rutina **aplicarAbsolute** 

| aplicarAbsolute | <!----> |
|-------|-------|
| Requiere: | Un arreglo de valores en CA2(16) almacenado a partir de la celda 0x4486 y cuya longitud está en la celda 4485 |
| Modifica: | COMPLETAR |
| Retorna: | El mismo arreglo con sus elementos en valor absoluto |

```js
aplicarAbsolute: MOV R0, 0x4486
                 MOV R1, [0x4485]
                 MOV R2, 0x0000

repetir: CMP R2, R1
         JE fin
         ADD R2, 0x0001
         AND [[R0]], 0x7FFF
         JMP repetir

fin: RET
```

**Nota**: usar la rutina absolute de la práctica anterior

5- Simule la ejecución de la rutina aplicarAbsolute sobre el siguiente mapa de memoria: 

| <!----> | ... |
|--------|--------|
| 0x4485 | 0004 |
| 0x4486 | 000A |
| 0x4487 | FFFF | <-- 7FFF
| 0x4488 | 8000 | <-- 0000
| 0x4489 | 00FF |

6- Modifique la rutina **aplicarAbsolute** para que reciba como parámetro la dirección inicial del arreglo en R0

```js
//Literal mi ej 4
```

7- En una fabrica de ventanas se codifican los pedidos en cadenas de 16 bits, y en caso de que la ventana esté pintada o lleve vidrio de seguridad es necesario usar un embalaje distinto. Se pide escribir la rutina necesitaEmbalajePremium, que determine si el pedido es uno de esos casos.

| necesitaEmbalajePremiun | <!----> |
|--------|--------|
| Requiere: | En R5, un código de pedido de ventana, donde el bit 3 indica si debe estar pintada y el bit 9 indica si lleva vidrio de seguridad |
| Modifica: | - |
| Retorna: | Un 1 en R7 si el pedido que está en R5 requiere un embalaje premium, es decir, si se trata de una ventana pintada o con vidrio de seguridad |

**Nota**: Tener en cuenta que los demas bits tambien representan distintas caracteristicas, pero de momento nos interesan esos dos

```js 
necesitaEmbalajePremium: AND R5, 0x0208
                         CMP R5, 0x0001
                         JGE siNecesita

siNecesita: MOV R7, 0x0001
```

8- Escriba la rutina **cantEmbalajeComun** a partir de su documentación y complete el campo modifica

| cantEmbalajeComun | <!----> |
|--------|--------|
| Requiere: | Un arreglo de pedidos a partir de la celda 0x0001, cuya longitud esta en la celda 0x0000 |
| Modifica: | - |
| Retorna: | En R6 la cantidad de pedidos que **no necesitan embalaje premium** |

```js
cantEmbalajeComun: MOV R0, 0x0000  // Contador de vueltas
                   MOV R1, 0x0001  // Celda inicial
                   MOV R6, 0x0000  // Contador de pedidos

repetir: CMP R0, [0x0000]
         JG fin
         ADD R0, 0x0001  // Incrementa una vuelta
         MOV R2, [[R1]]  // R2 <-- [[R1]]
         CALL check
         
check: AND [R2], 0x0208
       CMP [R2, 0x0001]
       JGE noNecesita
       RET

noNecesita: ADD R6, 0x0001
            JMP repetir

```

9- Implementar una rutina de test para verificar el funcionamiento de la rutina cantEmbalajeComun

```js

```

10- Contando con las nuevas herramientas incorporadas a Q en esta unidad, volver a escribir la rutina mapearCeldas de la guia 6 (ej 5) Utilizando la rutina esPar de la misma guia. mapearCeldas debe guardar un 0 o un 1 en las celdas 0x0000 a 0x0005 segun si los numeros de las celdas 0xF000 a 0xF0005 son pares o no

```js

```