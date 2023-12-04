En cada uno de los siguientes resueltos en la Práctica 5 de Normalización, se han agregado restricciones (identificadas con verde) para incluir dependencias multivaluadas. 
Para cada ejercicio dado:
- Analizar si las dependencias funcionales identificadas son suficientes o si deben agregar alguna otra dependencia funcional adicional
- Identificar la nueva clave de la relación en base a las nuevas restricciones (que va a afectar las claves en las relaciones residuales)
- Construir la última relación considerando la nueva clave identificada
- Identificar las Dependencias Multivaluadas
- Llevar a 4ta Forma Normal

## PASEADORES DE PERROS

Sea la siguiente tabla que representa a los paseadores de perros, los perros que se pasean y sus respectivos dueños en Bernal
```js
PASEO<DNI_paseador, DNI_cliente, nombre_cliente, domicilio_cliente, nombre_perro, edad_perro, raza_perro, correa_raza, comida_raza, categoria_paseo, monto_categoria_paseo,servicio_paseo>
```
con las restricciones:
1. Cada paseador se identifica por su DNI (único por paseador). Cada paseador pasea varios perros.
2. Cada cliente está identificado por su DNI (único por cliente). De cada cliente registramos su DNI, su
nombre y un domicilio. Sabemos que un nombre puede repetirse para diferentes DNI, y que varios clientes
pueden vivir en el mismo domicilio.
3. Cada cliente tiene varios perros, los cuales se identifican por el nombre.
4. Los nombres de los perros son únicos para cada cliente, pero se pueden repetir entre diferentes clientes
(aún cuando los clientes vivan en el mismo domicilio).
Por ejemplo, Lucía tiene dos perros: Blanquita y Coky; y Daniel tiene tres perros: Duque, Coky y Felipe.
5. De cada perro conocemos su nombre, su edad y qué raza de perro es.
6. Una raza de perro determinada siempre utiliza un solo tipo de collar y come un solo tipo de comida, sin
importar quién es el paseador. Por ejemplo, para los perros Labradores se utilizan collares de cuero y se le
da comida Premium, y para los perros Rottweiler se utilizan collares reforzados de nylon y se le da comida
Especial. Sin embargo, para diferentes razas de perro, pueden utilizarse el mismo tipo de collar y el mismo
tipo de comida,
7. Todos los paseadores ofrecen diferentes categorías de paseos. Cada categoría tiene
varios servicios asociados durante el paseo (sin importar el paseador que lo ofrece). Por
ejemplo, todos los paseadores de la relación PASEOS ofrecen las categorías común y
completa. La categoría común incluye la comida y juegos en una zona verde. Sin
embargo, la categoría completa incluye comida, un baño en veterinaria, vacunas (si
corresponde) y juegos en un parque.
8. Cada paseador cobra un precio diferente en cada categoría, pero siempre el mismo a todos los clientes. Por
ejemplo, el paseador Javier cobra $200 por la categoría común y $400 por la categoría completa, mientras
que el paseador Alejandro cobra $150 por categoría común y $450 por categoría completa. Puede darse que
dos paseadores cobren lo mismo por algunas de las categorías de paseo, pero no se cumple para todos los
paseadores

### DF's
  - DNI_cliente <- nombre_cliente, domicilio_cliente
  - DNI_cliente, nombre_perro <- edad_perro, raza_perro
  - raza_perro <- correa_raza, comida_raza
  - DNI_paseador, categoria_paseo <- monto_categoria_paseo

### Clave candidata
- $CC = (DNIPaseador, DNICliente, nombre_perro, razaPerro) - (nombreCliente, domicilioCliente, edadPerro, razaPerro, correaRaza, comidaRaza, montoCategoriaPaseo) + servicio_paseo
\\
CC = (DNIPaseador, DNICliente, nombrePerro, categoriaPaseo, servicio_paseo)$

### Normalización
- PASEO está en 1FN
- Para pasar a 2FN se distinguen grupos de repetición, resultando en:
  - De la DF1 se genera: CLIENTES <**DNI_cliente**, nombre_cliente, domicilio_cliente> // Cumple con 1,2 y 3FN
  - De la DF4 se genera: PASEOS <**DNI_Paseador**, categoria_paseo, monto_categoria_paseo> // Cumple con 1,2 y 3FN
  - De la DF2 y DF3 se genera: Perros: <**DNI_Cliente, nombre_perro**, edad_perro, raza_perro, correa_raza, comida_raza> //Cumple con 1,2 FN
  - **Residual** = <DNI_Cliente,DNI_paseador,nombre_perro,categoria_paseo,servicio_paseo>
- Para pasar a 3FN se divide PERROS:
  - RAZAS <**raza_perro**, correa_raza, comida_raza>
  - PERROS <**DNI_Cliente, nombre_perro**, edad_perro, **raza_perro**>
- Para pasar a 4FN se identifican las Dependencias Multivaluadas:
  - DM1: categoria_paseo -> -> servicioPaseo  (Cada categoria tiene 2 servicios)
    - SERVICIOS <**categoria_paseo**, servicioPaseo>
  - DM2: DNI_cliente -> -> nombre_perro  (Los clientes pueden tener varios perros)
    - PERROSM <**DNI_Cliente, nombre_perro**>
  - Residual: <**DNI_Paseoador, DNI_cliente, categoria_paseo**>