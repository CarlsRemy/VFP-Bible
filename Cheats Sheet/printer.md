# Técnicas de Impresión y Reportes en VFP

- Forzar la impresora desde código  

	Aunque SET PRINTER TO y SET PRINTER TO NAME se usan para redireccionar la impresora, los reportes .FRX pueden guardar información de la impresora en sus campos TAG y TAG2. Esto puede forzar la salida a una impresora específica incluso si la cambias por código.

	Solución recomendada:

	```foxpro
		USE factura-monarca2.frx EXCLUSIVE
		REPLACE ALL tag WITH "", tag2 WITH "" FOR objtype = 1
		USE
	```

	Esto limpia la información de impresora incrustada.

- Obtener lista de impresoras instaladas

	```foxpro
		oWMI = GetObject("winmgmts:")
		colPrinters = oWMI.ExecQuery("Select * From Win32_Printer")
		FOR EACH oPrinter IN colPrinters
			? oPrinter.Name
		ENDFOR
	```
- Seleccionar impresora predeterminada por código

	```foxpro
		DECLARE INTEGER SetDefaultPrinter IN winspool.drv STRING pPrinterName
		SetDefaultPrinter("NombreDeLaImpresora")
	```

	⚠️ Esto cambia la impresora por defecto del sistema, así que deberías devolverla luego a la original si no es deseado.

- Obtener Nombre de Impresora Predeterminada
	```FOXPRO
		DECLARE INTEGER GetDefaultPrinter IN winspool.drv;
		STRING @pszBuffer, INTEGER @pcchBuffer 

		nlength = 256
		lName = SPACE(nlength)

		lResult  = GetDefaultPrinter(@lName ,nlength )

		IF lResult  !=0
			lName  = LEFT(lName, nlength -1)
		ELSE 
			lName  =""
		ENDIF  

		RETURN lName 
	```


- Usar PROMPT para mostrar cuadro de diálogo de impresión
	```foxpro
		REPORT FORM miReporte TO PRINTER PROMPT NOCONSOLE
	```
- Detectar impresora predeterminada

	```foxpro
		oWMI = GetObject("winmgmts:")
		colPrinters = oWMI.ExecQuery("Select * From Win32_Printer")
		FOR EACH oPrinter IN colPrinters
			IF oPrinter.Default
				? "Impresora predeterminada:", oPrinter.Name
			ENDIF
		ENDFOR
	```
- Previsualización antes de imprimir
	```foxpro
		REPORT FORM miReporte PREVIEW
	```
	Ideal para evitar impresiones innecesarias.

- Realizar Corte de Papel
	```FOXPRO
		???CHR(27)+CHR(105) 
	```

- Abrir Cajon (CAJA REGISTRADORA)
	```FOXPRO
		???Chr(27) + Chr(112) + Chr(0)+ Chr(25)+ Chr(250)
	```

[Volver atrás](./run.md)