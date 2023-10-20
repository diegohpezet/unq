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

