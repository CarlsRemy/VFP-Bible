## Funcines para Trabajar con Numeros

- `INT(nValor)`   
Devuelve la parte entera de un número (redondea hacia abajo).
- `ROUND(nValor, nDecimales)`  
Redondea un número a la cantidad de decimales que indiques.

- `NTOM() y MTON()` (Precisión Monetaria)   
VFP tiene un tipo de dato Currency ($) que evita errores de precisión decimal en cálculos financieros.   
**NTOM(n):** Convierte numérico a moneda (4 decimales fijos internos).  
**MTON(m):** Convierte moneda a numérico normal.   

- `MAX(NExp...) | MIN(NExp..)`  
Súper útiles para evitar valores negativos o exceder topes sin usar IF:
```prg
nDescuentoCalculado = 120
nResultado = MIN(nDescuentoCalculado, 100) 
* Devuelve 100, porque es el menor de los dos.
```

- `CEILING(nValor)`   
Redondea hacia arriba al entero más cercano.

- `FLOOR(nValor)`  
Redondea hacia abajo al entero más cercano.

- `ABS(nValor)`  
Devuelve el valor absoluto (quita el signo).
- `MOD(nDividendo, nDivisor)`  
Devuelve el residuo (módulo) de una división.
- `VAL(cCadena)`  
Convierte un string a número.
- `STR(nValor [, nLongitud [, nDecimales]])`  
Convierte un número a cadena (string).

- `ISDIGIT(cCadena)`   
Devuelve .T. si la cadena contiene solo dígitos.

- `PADL(exp, Nsize [,stringPad])  | PADR(exp, Nsize [,stringPad])`
Nos permite Agregar rellenar una exprecion a la Izquierda (PADL) o Derecha (PADR) con n cantidad de un Caracter
```prg
	padl(9, 4, "0") && retorna 00009
```



[Volver atrás](./String.md) | 	[Siguiente tema](../Directories.md)