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
- **`Instanciar Un Formulario`**

```foxpro
	LOCAL i, loForm, cFormName
	cFormName ="ejemplo_form"

	FOR i = 1 TO _SCREEN.FormCount && Recorer Objeto de Formularios en Ejecucion
		loForm = _SCREEN.Forms(i) 
		IF UPPER(loForm.Name) == UPPER(cFormName)
			RETURN loForm
		ENDIF
	ENDFOR
```

### Objeto Form

Los Formularios son un Objeto que puede ser recorido, leido o modificado como si de una
Tabla se tratase siempte que usamos la sentencia **"Use"**

- **`Estrutura del Objeto Form`**
Permite Ver la structura que compone un Form
```foxpro
	USE "Ejemplo.scx"
	DISPLAY STRUCTURE
```

##### Ejemplo de Estructura

| FIELD NAME |	TYPE      | Descripccion |
|------------|------------|--------------|
| PLATAFORM  | CHARACTER  |
| UNIQUEID   | CHARACTER  | Identificador interno único (GUID o secuencia usada por el diseñador).
| TIMESTAMP  | NUMERIC    | Marca de tiempo usada para sincronización (última modificación).
| CLASS MENO | MEMO | Nombre de la clase que hereda (por ejemplo "CommandButton", "Textbox").
| CLASSLOC   | MEMO | Ruta al archivo .VCX donde está definida la clase si es una clase visual personalizada.
| BASECLASS  | MEMO | Tipo base de control o formulario, como "Form", "CommandButton", "Textbox", "Pageframe".
| OBJNAME    | MEMO | Nombre lógico del objeto o control (por ejemplo "cmdAceptar", "txtCliente").
| PARENT     | MEMO | Nombre del contenedor donde está el objeto (por ejemplo, el formulario o una página). Si está vacío, es el objeto raíz (el formulario).
| PROPIETIES | MEMO | Texto plano con todas las propiedades del objeto.
| PROTECTED  | MEMO | Propiedades marcadas como protegidas en clases personalizadas
| METHODS    | MEMO | Contiene todo el código fuente de los eventos y métodos del objeto. 
| OBJCODE    | MEMO (BINARY) | Código compilado de los métodos (versión binaria del campo Methods), usado para ejecución.
| OLE        | MEMO | Contiene datos binarios o texto OLE si el control usa objetos OLE (por ejemplo, un control ActiveX). En formularios normales casi siempre está vacío.
| OLE2       | MEMO |
| RESERVED1  | MEMO | Campos reservados por el diseñador de Visual FoxPro para futuras versiones o compatibilidad interna. Generalmente vacíos.
| RESERVED2  | MEMO |
| RESERVED3  | MEMO |
| RESERVED4  | MEMO |
| RESERVED5  | MEMO |
| RESERVED6  | MEMO |
| RESERVED7  | MEMO |
| RESERVED8  | MEMO |

- **`Extrar todos los Eventos de un formulario Form`**

```foxpro
	lcForm ="ejemplo.sxc"
	lc = ""

	USE (lcForm) SHARED
	SCAN FOR Upper(ALLTRIM(OBJNAME)) == Upper("Form_name")
		lc = lc + "Objeto: "+OBJNAME + CHR(13)+chr(10) +  Methods +CHR(13)+chr(10)+""
	ENDSCAN
	USE

	STRTOFILE(lc , 'code.txt', 1)
```
- **`Modificar Ruta de ClassLoc`**

```foxpro
	LOCAL lcPath, lcFile, lcDir. lcClass
	lcDir = "D:\Contaprosql\"
	lcPath = ".\clases\"  && ruta deseada para las clases
	lcForm =""
	lcClass ="lmcal.vcx"

	ALINES(aFiles, "ccotroing01-hotel.scx", 1, ",")

	CREATE CURSOR rutas (formulario C(50), classloc C(200))
	cld=""
	TRY 

		FOR EACH lcFile IN aFiles
			lcForm = lcDir + lcFile
		
			USE (lcForm ) SHARED
			
				SCAN FOR NOT EMPTY(ClassLoc)
		
					IF lcClass $ ALLTRIM(ClassLoc)
						lname =  JUSTFNAME(ClassLoc) 
						if empty(lname)
							lname = lcClass
						endif
						
						REPLACE  ClassLoc WITH lcPath + lname 
					ENDIF 
				ENDSCAN

		ENDFOR
	
	CATCH
		
	FINALLY
		USE 
		CLOSE TABLES
	ENDTRY	
```