**Punto Fijo**

BSS(n,m)

- Met. Escalado: Se representa la cadena en BSS y se la divide por $2^m$
- Representación: $I:{BSS}(x*2^m)$
- Rango: Se representan el min y el max
- Resolución: $2^m$
- Error: $ValorObtenido - ValorAproximadoRepresentable$

**Punto Flotante**

mantisa: BSS(m) / exponente:SM(n)

- Met. Escalado: Se Interpreta la mantisa y el exponente por separado. Se reemplazan en la formula: $m*2^{e}$
- Representación: $I:{BSS}(x*2^m)$
- Rango = $[Mmin * 2^{Emax}; Mmax * 2^{Emax}]$
- Resolución mínima y máxima: $I_{BSS}(0001) * 2^{Emin} o bien I_{BSS}(0001) * 2^{Emax}$
- Error: $ValorObtenido - ValorEsperado$

**Memoria caché**

- $\dfrac{2^{16}}{celdasPorBloque} = \dfrac{2^16}{2^{}} 2^{bitsTag}$

**Performance de la caché**

- Default/Write back = fallos * (t_cache + t_mem) + aciertos * t_cache

- Write Through = (fallos + cant_w) * (t_cache + t_mem) + aciertos * t_cache


