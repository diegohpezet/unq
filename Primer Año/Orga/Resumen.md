# U7 - Q4: Flags, saltos y alternativa condicional

```js

```

# U8 - Q5: Repeticiones y máscaras

# U9 - Arreglos

**Arreglo**: Conj. de valores en el mismo sistema numerico almacenados en un bloque.

Mediante repeticion se pueden recorrer. Ejemplo:

```js
recorrido: MOV R1, 0x0000  // Inicia el contador

ciclo: CMP R1, 0x0004
       JG fin
       ADD R1, 0x0001
       JMP ciclo

fin: RET
```

## Método de direccionamiento indirecto

Sirve para indicar que se apunta al dato que indica el dato del registro indicado. Suponer:

[R0], donde R0 tiene almacenado el valor 2000. En este caso, se buscaría el valor dentro de la celda 0x2000

# U10 - Sistemas en punto fijo y punto flotante

Son sistemas binarios que permiten representar números con valores decimales.

Surge nuevos concepto, **resolución**, que es la distancia mínima entre dos valores y **error**, que es la diferencia entre el valor buscado y el valor obtenido

## Punto Fijo

Se dedican los primeros bits a la parte entera, el resto a la parte fraccionaria.

<center>

**Suponer un sistema BSS(8,3) y una cadena 10011101**

| Sistema  | Cadena   | Interpretación | Rango       | Resolución |
| -------- | -------- | -------------- | ----------- | ---------- |
| BSS(8,3) | 10011101 | 19,625         | [0; 31,825] | 0,125      |

</center>

### Interpretación

**Método por partes**: Se interpreta la cadena de la siguiente manera:
- $I_{BSS(8,3)}(10011101) = 1*2^{4} + 0*2^{3} + 0*2^{2} + 1*2^{1} + 1*2^{0} + 1*2^{-1} + 0*2^{-2} + 1*2^{-3} = 0.125 + 0.5 + 1 + 2 + 16 = 19,625$

**Método escalado**: Primero se interpreta la cadena como en BSS y luego se la divide por $2^{n}$, donde n es la cant de decimales
- $I_{BSS(8)}(10011101) = 2^{7} + 2^{4} + 2^{3} + 2^{2} + 2^{0} = 128 + 16 + 8 + 4 + 1 = 157$ <br /> <br /> $\dfrac{157}{2^3} = \dfrac{157}{8} = 19,625$

### Representación y error

$R_{BSS(5)}(19) = 2^{0} + 2^{1} + 2^{4} = 10011$


### Rango

- **Mínimo** = $I_{BSS(8,3)}(00000000) = 0$
- **Máximo** = $I_{BSS(8,3)}(11111111) = 31,825$
- **Rango** = [0; 31,825]

### Resolución

$2^{-m}$, donde m es la cantidad de bits que representan el valor decimal

Entonces: $2^{-3} = 0.125$

## Punto Flotante

Expresa el valor entero y luego lo desplaza para representar valores decimales

<center>

**Suponer un sistema de punto flotante con mantisa en BSS(5) y exponente en SM(3) y una cadena 10011101**

| Sistema                           | Cadena   | Interpretación | Rango       | Resolución |
| --------------------------------- | -------- | -------------- | ----------- | ---------- |
| mantisa: BSS(5), exponente: SM(3) | 10011101 | 9,5            | [0; 31,825] | 0,125      |

</center>

### Interpretación

Se interpreta por un lado la mantisa y por otro el exponente. Luego se reemplazan los valores en la formula: **$m * 2^e$**

- m = $I_{BSS(5)}(10011) = 2^4 + 2^1 + 2^0 = 19 $
- e = $I_{SM(3)}(101) = -1*(2^0) = -1$

<center>

$19 * 2^{-1} = 19 * 0.5 = 9,5$

</center>

### Representación

### Rango

Se calculan la mantisa máxima y mínima, el exponente máximo y mínimo y luego se reemplazan en la fórmula: $[Mmin * 2^{Emax}, Mmax * 2^{Emax}]$

- Mmin = $I_{BSS(5)}(00000) = 0$
- Mmax = $I_{BSS(5)}(11111) = 31$
- Emin = $I_{SM(4)}(111) = -3$
- Emax = $I_{SM(4)}(011) = 3$

<center>

$[0 * 2^{3}; 31 * 2{3}]$

</center>

### Resolución

Corresponde a la distancia que puede mínima que puede haber entre 2 valores consecutivos. Al hablarse de exponentes este valor puede ser fijo o exponencial, es decir ir aumentando, por lo que puede haber una resolución fija o una resolución máxima y una mínima.

Se obtiene haciendo la **interpretación de la mantisa que represente el valor 1** y multiplicandolo a $2^{Emin}$ (para la R.minima) o $2^{Emax}$ (para la R.maxima)

- $Rmin = I_{BSS(5)}(00001) * 2^{-3} = 0.125$
- $Rmax = I_{BSS(5)}(00001) * 2^{3} = 8$

# U11 - Caché

La memoria caché es una memoria de acceso rápido para la CPU, almacena información que supone que se requiere tener "a mano" para reducir tiempos de lectura

Almacena información en **bloques**, que son conjuntos de celdas consecutivas en memoria

