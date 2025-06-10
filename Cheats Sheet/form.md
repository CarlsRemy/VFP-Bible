# Validaciones de Formulario

- **` _SCREEN`**  

	Es una instancia de la clase Form que contiene todos los formularios no de tipo top-level.
	Si abres formularios sin ShowWindow = 2 (Top-Level), aparecen dentro de _SCREEN.

	```foxpro
	&&& Cerrar Otras istancias de formularios
	lnCantidadForms = _Screen.FormCount
	
	FOR lnI = lnCantidadForms TO 1 STEP -1
		loForm = _Screen.Forms(lnI)
		WAIT windows loForm.Name
		IF loForm.Name <> "Form1"
			loForm.Release()
		ENDIF
	ENDFOR
	```

- **`WEXIST("Carlos_test")`**

	Devuelve .T. si existe una ventana definida con ese nombre

- **`ZOOM WINDOW`**

	Permite cambiar el tamaño o visibilidad de una ventana

	```foxpro
	ZOOM WINDOW MiVentana NORM  && Restaura el tamaño normal
	ZOOM WINDOW MiVentana MAX   && Maximiza
	ZOOM WINDOW MiVentana MIN   && Minimiza
	```
