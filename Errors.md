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


[Volver atrás](./word_Excel.md) | 	[Siguiente tema](./Cheats%20Sheet/evaluations.md)