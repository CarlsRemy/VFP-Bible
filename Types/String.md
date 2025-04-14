## Funcines para Trabajar con Strings

- `StrExtract(cExp, cBegDelim, cEndDelim [, nFlags])`  
se utiliza para extraer una subcadena de una cadena de texto, delimitada por cadenas específicas de inicio y fin.

	**Parámetro	Descripción**  
	- **cExp**	Cadena de texto de entrada.
	- **cBegDelim**	Delimitador inicial (inicio de lo que quieres extraer).
	- **cEndDelim**	Delimitador final (fin de lo que quieres extraer).
	- **nFlags**	(Opcional) Un número que controla cómo se hace la extracción. Valores comunes:
		- 0: Ignora delimitadores no encontrados (retorna cadena vacía).
		- 1: Incluye delimitadores en el resultado.
		- 2: Comienza después del delimitador de inicio.
		- 4: Extrae hasta el final si no encuentra delimitador final. Puedes sumar valores para combinar comportamientos.


- `STRTRAN(cExp, cBuscar, cReemplazar [, nInicio [, nVeces]])`   
Reemplaza todas (o algunas) apariciones de una subcadena dentro de otra cadena.

- `AT(cBuscar, cExp [, nOcurrencia])`   
Devuelve la posición de una subcadena dentro de otra.

- `SUBSTR(cExp, nInicio [, nLong])`   
Extrae una subcadena a partir de una posición.

- `OCCURS(cBuscar, cExp)`  
Cuenta cuántas veces aparece una subcadena.

- `Operador $`   
Evalua si una subcadena esta cintenida en otra
```foxpro
? "hola soy Juan" $ "juan" & retorna .T.
```

[Volver atrás](../introduction.md) | 	[Siguiente tema](./Number.md)