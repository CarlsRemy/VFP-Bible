# Funcines Utiles para evaluacines

- **TYPE("NameOfVariable")** 
Esta Funcion nos permite Evaluar el tipo de una Variable, siendo **"U"** o **"L"** los valores para variables no definidas

	| Código | Tipo de dato         |
	|--------|-----------------------|
	| "C"    | Carácter (string)     |
	| "N"    | Numérico              |
	| "L"    | Lógico (booleano)     |
	| "D"    | Fecha                 |
	| "U"    | No definida           |
	| "O"    | Objeto                |
	| "Y"    | Currency              |
	| "T"    | DateTime              |
	| "G"    | Imagen (General/Binary) |

- **VARTYPE(variable)**  
Muy similar a TYPE(), pero acepta directamente variables u objetos en vez de una cadena con su nombre.

- **ISNULL(expresion)**  
Retorna .T. si la expresión es NULL, de lo contrario .F.
- **EMPTY(expresion)**  
Retorna .T. si la expresión está vacía ("" en strings, 0 en números, .F. en lógicos, etc.).

- **LEN(cadena)**  
Devuelve la longitud de una cadena.

- **EVALUATE("nombreVariable")**  
Evalúa el contenido de una variable por su nombre (útil para acceso dinámico).

- **IIF(condición, valorSiVerdadero, valorSiFalso)**   
Devuelve un valor u otro dependiendo de si la condición es verdadera o falsa (forma abreviada de un IF).

- **TRANSFORM(valor [, formato])**  
Convierte cualquier tipo de dato a texto. Puedes aplicar formatos numéricos, fechas, etc.


[Volver atrás](../Errors.md) | 	[Siguiente tema](./run.md)