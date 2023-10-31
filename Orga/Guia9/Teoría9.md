# Arreglos y recorridos sobre arreglos

**Estructura**: Conjunto de valores en el mismo sistema almacenados en un bloque de celdas de memoria consecutivas. El **tamaño** se determina por la cantidad de celdas que ocupa

**Recorrido de arreglo**: Se pueden recorrer empleando repeticion
```js
recorrido: MOV R0, 0x0000  // Inicia el acumulador
           MOV R1, 0x0000  // Inicia el contador

ciclo: CMP R1, 0x0004
       JG fin
       ADD R0, [0x2000]  // Problema!
       ADD R1, 0x0001
       JMP ciclo

fin: RET
```
El problema aqui es que siempre añade el mismo elemento (suponiendo que el array inicia en 0x2000), por lo cual surge un nuevo modo de direccionamiento, el **Modo de direccionamiento indirecto**.

Este nuevo modo permite indica el espacio de valor de memoria almacenado en un Registro o espacio de memoria. Ej: suponiendo que en R0 se encuentra el valor FFFF, [[R0]] busca el valor almacenado en la celda FFFF (señalada por R0)