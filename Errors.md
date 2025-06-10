# Errores Comunes y Soluciones

Esta sección cubre errores típicos que se presentan durante el desarrollo con Visual FoxPro, junto con sus posibles causas y soluciones.

- Variable no definid

	Estás usando una variable que no ha sido definida o está fuera de alcance.

	Asegúrate de declarar la variable con LOCAL, PUBLIC, PRIVATE o de haberla inicializado antes.

	```foxpro
		** verificar si la variable No esta Definida
    IF INLIST(TYPE("NameOfVariable"), "U", "L")
			NameOfVariable = ""
		ENDIF
	```

- Type mismatch  
	Estás intentando asignar valores de distinto tipo sin conversión explícita.

	Usa funciones como STR(), VAL(), INT(), etc., para convertir valores.

- Object required  
	Estás accediendo a un objeto que no ha sido creado con CREATEOBJECT().

	Verifica que el objeto fue correctamente instanciado.

- Argument count mismatch

	Llamaste a una función o método con más (o menos) parámetros de los definidos.

	Verifica la definición de la función y asegúrate de pasar los argumentos necesarios.

-  File access denied / File in use

	El archivo está abierto por otro proceso o usuario.

	Usa USE ... EXCLUSIVE si necesitas control exclusivo.
	Verifica si el archivo está abierto con USED() o ISFILE().

- `TRY ... CATCH ... FINNALY`  

	La estructura **TRY...CATCH...FINALLY** comienza con una cláusula **TRY** que marca el inicio de un bloque **TRY**. En este bloque se puede especificar un grupo de cláusulas que pueden producir un error en tiempo de ejecucion. Si el programa completa el bloque **TRY** sin generar ninguna excepción, este salta el bloque **CATCH** y busca el bloque **FINALLY** y ejecuta las sentencias de ese bloque. Si el bloque **FINALLY** no existe, el programa ejecuta la primera sentencia despues de la clausula ENDTRY que marca el final de la estructura **TRY...CATCH...FINALLY**

	```foxpro
	&& Estructura basica de TRY

	TRY
		[Comandos a ser intentados]
	CATCH [TO NombreDeVariable] [WHEN lExpresión]
		[Comandos para reportar y procesar el error]
		[ EXIT]
		[THROW uExpresión]
	CATCH [TO NombreDeVariable] [WHEN lExpresión]    && para un error diferente
		[Comandos para reportar y procesar el error]
		[EXIT]
		[THROW uExpresión]
	FINALLY
		[Código a ejecutar siempre]
	ENDTRY	
	```
	La repetición de la cláusula CATCH no es un error tipográfico. CATCH puede funcionar un poco como DO CASE si es que hay varios errores posibles. lExpresión debe devuelver un valor lógico para que esto funcione. Normalmente lExpresión se refiere a la propiedad ErrorNo de la variable nombrada, así:

	```foxpro
	TRY
    * Código que puede lanzar un error
    LOCAL a, b
    a = 10
    b = 0
    ? a / b   && Esto lanza error 4
	CATCH TO lEx WHEN lEx.ErrorNo = 1
    ? "Archivo no encontrado"
	CATCH TO lEx WHEN lEx.ErrorNo = 4
    ? "División por cero"
	CATCH TO lEx WHEN lEx.ErrorNo = 11
		? "Variable no definida"
	ENDTRY
	```

- `ON ERROR` Manejador Global de errores

	```foxpro
	&& Aqui definimos que que el procedimiento ErrTrap menejara los errore no controlados

	ON ERROR DO ErrTrap WITH ERROR(), MESSAGE(), MESSAGE(1)
	```


	# El objeto Exception

	Los objetos basados en esta clase son creados al ejecutar una cláusula CATCH, y también con el nuevo comando THROW. Permiten describir más robustamente los errores que tengamos. Se pueden leer y escribir sus propiedades durante la ejecución del programa

	## Métodos
	 
	- AddProperty
	- ReadExpression
	- ReadMethod
	- ResetToDefault
	- SaveAsClass
	- WriteExpression
	- WriteMethod

	## Eventos
 
	- Destroy
	- Error
	- Init

	## Propiedades

	| Propiedad   | Tipo | descripcion |   
	|-------------|------|-------------|
	| BaseClass   | Char | Exception  |
	| Class       | Char | Nombre de Clase |
	| ClassLibrary | Char | Biblioteca de clase |
	| Comment     | Char | Comentario |
	| Details     | Char | Detalles  |
	| ErrorNo     | Num  | Número de Error |
	| LineContents | Char | Código que causó el error |
	| LineNo      | Num  | Línea del programa donde ocurrió el error |
	| Message     | Char | El mensaje de error |
	| Name        | Char | Nombre |
	| Parent      | Char | Padre |
	| ParentClass | Char | Clase del Padre |
	| Procedure   | Char | Nombre del Procedimiento donde ocurrió |
	| StackLevel  | Num  | Nivel en el Call Stack del procedimiento |
	| Tag         | Char | Disponible al programador	|

	## Fumciones
	en VFP hay unas funciones que devuelven valores similares a las propiedades del **Objeto Exception**.

	| Nombre       | Propiedad equivalente |
	|--------------|-----------------------|
	|	ERROR()      | ErrorNo      |
	| LINENO()     | LineNo       |
	| MESSAGE()    | Message      |
	| MESSAGE(1)   | LineContents |
	| PROGRAM()    | Procedure    |
	| ASTACKINFO() | StackLevel   |




[Volver atrás](./word_Excel.md) | 	[Siguiente tema](./Cheats%20Sheet/evaluations.md)