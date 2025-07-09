# Técnicas de Impresión y Reportes en VFP

- Forzar la impresora desde código  
	Los comandos **SET PRINTER TO** y **SET PRINTER TO NAME** permiten redireccionar la salida de impresión, pero los reportes .FRX pueden guardar información de la impresora en los campos TAG y TAG2, lo que puede forzar el uso de una impresora específica, incluso si se cambia por código.

	Solución recomendada:

	```foxpro
		USE factura-monarca2.frx EXCLUSIVE
		REPLACE ALL tag WITH "", tag2 WITH "" FOR objtype = 1
		USE
	```

	Esto limpia la información de impresora incrustada.

## Uso WMI de en VFP
### Que es WMI ?


WMI significa Windows Management Instrumentation, y es una tecnología de Microsoft que permite a los programas y scripts acceder a información administrativa y de configuración del sistema operativo Windows.

###  Acciones comunes con impresoras usando WMI

- Verificación del estado de una impresora usando WMI en VFP

	```foxpro
		strComputer = "."
		NomImpresora = UPPER(ALLTRIM(lPrinter))

		TRY
			objWMIService = GETOBJECT("winmgmts:{impersonationLevel=impersonate}!\\" + strComputer + "\root\cimv2")

			colPrinters = objWMIService.ExecQuery("SELECT * FROM Win32_Printer")

			FOR EACH objPrinter IN colPrinters
				IF UPPER(ALLTRIM(objPrinter.Name)) == NomImpresora

					* Verifica si el estado de la impresora es "Ocupado" (2) o "Listo" (3)
					* Y si no está en modo sin conexión (WorkOffline = .F.)
					IF INLIST(objPrinter.PrinterStatus, 2, 3) AND NOT objPrinter.WorkOffline
						* La impresora está encendida y disponible
						Encendida = .T.
					ENDIF
					EXIT
				ENDIF
			ENDFOR
		CATCH
			* Si ocurre un error (por ejemplo, WMI desactivado), se asume que no está disponible
			Encendida = .F.
		ENDTRY
	```

- Obtener lista de impresoras instaladas

	```foxpro
		oWMI = GetObject("winmgmts:")
		colPrinters = oWMI.ExecQuery("Select * From Win32_Printer")
		FOR EACH oPrinter IN colPrinters
			? oPrinter.Name
		ENDFOR
	```
-  Detectar impresora predeterminada
	```foxpro
		oWMI = GetObject("winmgmts:")
		colPrinters = oWMI.ExecQuery("Select * From Win32_Printer")
		FOR EACH oPrinter IN colPrinters
			IF oPrinter.Default
				? "Impresora predeterminada:", oPrinter.Name
			ENDIF
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