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

- **EXECSCRIPT()**  
Es mucho más potente que EVALUATE(). Permite ejecutar múltiples líneas de código, comandos complejos, bucles o incluso un script entero guardado en un campo Memo.

- **IIF(condición, valorSiVerdadero, valorSiFalso)**   
Devuelve un valor u otro dependiendo de si la condición es verdadera o falsa (forma abreviada de un IF).

- **ICASE(condición..., Default)**   
Forma Corta de Hacer uso de Case (El Swict de VFP)

```prg
lcStatus = ICASE(lnSaldo > 0, "Deudor", ;
                 lnSaldo < 0, "Favor", ;
                 "Al día")
```
- **EVL**   
Devuelve el primer valor que no sea "vacío" (0, .F., "", {}, .NULL.). Ideal para inicializar variables o evitar errores de división por cero.

- **CREATEOBJECT()**   
Nos permite Crear Objetos a de la Base class que proporcinemos, util para crear Variables tipo Objeto, botones y componestes dinamicos, objetos de Dll com.

- **ADDPROPERTY**   
Nos permite Agregar una propiedad al Objeto con un valor inicial, de ya existir solo remplaza su valor

- **INPUTBOX**   
Si necesitas una entrada rápida del usuario sin crear un formulario .SCX:
```prg
	lcClave = INPUTBOX("Ingrese clave de autorización", "Seguridad", "", 5000) 
```

- **TRANSFORM(valor [, formato])**  
Convierte cualquier tipo de dato a texto. Puedes aplicar formatos numéricos, fechas, etc.


[Volver atrás](../Errors.md) | 	[Siguiente tema](./run.md)