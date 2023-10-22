# Repeticiones
1- Escribir y documentar una rutina que calcule la multiplicación de los valores que se encuentran en los registros R5 Y R6 respectivamente pero sin usar la instrucción MUL
```js
multiSinMul: 
    MOV R4, 0x0000  //Acumulador
repetir:            
    //Añade a R4 el valor de R6, R5 cant de veces
    CMP R5, 0x0000  
    JE salir
    ADD R4, R6
    SUB R5, 0x0001
    JMP repetir
salir:
    RET
```
2- Realizar una prueba de escritorio con valores que prueben la rutina del ejercicio anterior

Prueba de escritorio:
Valores iniciales
R5: 5, R6:5
Resul. esperado: R4 <- 25
Ejecución paso a paso:
```js
multiSinMul:
    MOV R4, 0x0000  // R4 <- 0
repetir:
    CMP R5, 0x0000  //
    JE salir
    ADD R4, R6      // R4 <- 5
    SUB R5, 0x0001  // R5 <- 4      (5-1)
    JMP repetir
salir:
    RET
```

3- Escribir y documentar una rutina que calcule
la división entera entre los valores de R0 y R1 respectivamente sin usar la instrucción DIV
R0 dividendo R1 divisor

| divSinDiv | <!----> |
|-----------|-----------|
| Requiere: | - |
| Modifica: | R2 |
| Retorna: | El valor 0 en el registro R2 |

| repetir | <!----> |
|-----------|-----------|
| Requiere: | Valores en los registros R0, R1. R2 debe iniciar en 0 |
| Modifica: | R1 |
| Retorna: | En R2 el resultado de la división entre R0 y R1 | 

```js
divSinDiv:
    MOV R2, 0x0000
repetir:
    CMP R0, R1
    JE salir
    ADD R2, 0x0001
    ADD R1, R1
    JMP repetir
salir:
    RET
```

4- Escribir y documentar una rutina que cuente la cantidad de dígitos "1" en la cadena  almacenada en R6

R6 <- 1011

```js
cantDeUnos:


```

5- Escribir y documentar una rutina que calcule el factorial del valor almacenado en R5. Dicho valor está representado en BSS

| factorial | <!----> |
|-----------|-----------|
| Requiere: | Valores en BSS en el registro R5 |
| Modifica: | R0 |
| Retorna: | En R5, el factorial de su valor inicial en BSS | 

```js
factorial: 
    MOV R0, R5
repetir:
    CMP R0, 0x0000
    JE salir
    SUB R0, 0x0001
    MUL R5, R0
    JMP repetir
salir:
    RET
```

# Operaciones lógicas bit a bit

6- ¿Cuál es el resultado de las siguientes operaciones?
- 1101 AND 0111 = 0101
- NOT 0100 = 1011
- ((1010 AND 1100) OR 0101) XOR 1100 = (1000 OR 0101) XOR 1100 = 1101 XOR 1100 = 0001

7- Complete las operaciones lógicas dada una cadena de bits [cadena]

- [cadena] OR 11111000 = 11111[c2][c1][c0]
- [cadena] AND 10001111 = [c7]000[c3][c2][c1][c0]

8- Implementar la rutina absolute siguiendo su documentación

| Requiere | <!----> |
|-----------|-----------|
| Requiere: | Un valor en SM(16) en el registro R0 |
| Modifica: | COMPLETAR |
| Retorna: | El valor absoluto en R0, donde el primer bit se cambió por un 0 | 

```js
absolute: AND R0, 0x7FFF  // 0111 1111 1111 1111
          RET
```

9- Implementar la rutina xor en funcion de su documentacion:
| xor | <!----> |
|--------|---------|
| Requiere: | Un valor en SM(16) en el registro R0 |
| Modifica: | COMPLETAR |
| Retorna: | El valor absoluto en R0, donde el primer bit se cambió por un 0 |
```js
//Xor: (-a^b) + (a^-b)
xor: MOV R3, R6     //Copio las variables y las niego
     MOV R4, R7
     NOT R3
     NOT R4 
     AND R3, R7     //(-a^b)
     AND R6, R4     //(a^-b)
     OR R3, R6
     MOV R7, R3
     RET
```

10- Programar una rutina de test para Xor
```js
testXor: MOV R6, 0x0005
         MOV R7, 0x0003
         CALL xor
         CMP R7, 0x0006
         JE funcionaBien
         MOV R0, 0x0000
         JMP fin

funcionaBien: MOV R0, 0x0001
              JMP fin

fin: RET
```

11- Implementar la rutina invImp que dada una cadena de 16 bits en R1, invierta el valor de las posiciones impares. Utilice maascaras y operaciones logicas. Para resolver este ejercicio es necesario
descomponer el problema
```js
invImpar: MOV R7, 0xAAAA
          CALL xor
          RET
```

12- Implementar la rutina opuesto, que calcule el opuesto aditivo del  numero almacenado en el registro R2 sin usar SUB. Dicho numero esta representado en CA2(16)
```js
opuesto: NOT R1
         ADD R1, 0x0001
         RET
```

13- . Un registro meteorologico es aquel donde sus bits indican la  recipitacion en cada dıa, para una estacion meteorologica determinada, durante 14 dıas (los 14 bits de la derecha). En el sistema occidental se indica con 0 si llovio y con un 1 el caso contrario. En el sistema oriental se indica al inverso. Por ejemplo, la cadena 0011001100110011 se convierte ası: 0000110011001100 (notar que los primeros 2 bits siempre estan en cero). Implementar la rutina occidentalAOriental segun la documentacion:
```js
meteoOriental: OR R3, 0xC000
               NOT R3
               RET
```

14- Implementar la rutina diasDeLluvia segun la documentacion:
| diasDeLluvia | <!----> |
|----------|---------|
| Requiere: | Un registro meteorologico en sistema oriental en R6 |
| Modifica: | COMPLETAR |
| Retorna: | En R2 la cantidad de días de lluvia registrados |

**Pista**: puede usar la rutina desplazarIzq que tiene la siguiente documentacion:

| desplazarIzq | <!----> |
|---------|---------|
| Requiere: | Una cadena en R0 |
| Modifica: | - |
| Retorna: | En R1 desplaza los bits de la cadena contenida en R0 un lugar hacia la izquierda |


```js
EscenarioInicial:
R6: 0000110011001100

ResultadoEsperado:
R2 <- 0x0006  

[assembly: 0xA000]
diasDeLluvia: MOV R1, R6 
              MOV R2, 0x0000  // Contador de unos
              MOV R3, 0X0000  // Contador del bucle

repetir: MOV R0, R1  // Prepara para el siguiente bucle
         COMP R2, 0x00010
         JLE comparar
         JMP fin

comparar: ADD R3, 0x0001  // Agrega una vuelta al bucle
          AND R1, 0x0001
          COMP R1, 0x0001
          JE sumarUno
          JMP repetir

sumarUno: ADD R2, 0x0001
          JMP repetir

fin: RET

```
