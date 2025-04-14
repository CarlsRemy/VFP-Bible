# ¿Qué es una clase en VFP?
Una clase en VFP es una plantilla para crear objetos que contienen propiedades, métodos, eventos y datos.

Las clases pueden definirse de dos formas:

- En un archivo .VCX (librería visual de clases)

- En código (DEFINE CLASS ... ENDDEFINE) → más común para clases COM o reutilizables

## Sintaxis básica: DEFINE CLASS

```foxpro
DEFINE CLASS NombreClase AS TipoBase [OLEPUBLIC]
    
	* Propiedades
	Propiedad1 = "valor"
	Propiedad2 = 123

	* Constructor
	PROCEDURE Init(p1, p2)
			* Lógica al crear el objeto
	ENDPROC

	* Método personalizado
	PROCEDURE Metodo1()
			? "Este es un método"
	ENDPROC
ENDDEFINE
```

cuando usas DEFINE CLASS, normalmente estás creando una clase que se usa dentro del propio VFP. Pero también puedes definir una clase "COM visible", es decir, que otros programas (como VB, C#, Excel, etc.) puedan usarla como si fuera un componente COM registrado.

## ¿Qué es una clase COM en VFP?
Una clase COM (OLEPUBLIC) en VFP es una clase que tú defines para exponerla al sistema como un servidor COM, lo cual permite que otras aplicaciones instancien y usen esa clase desde fuera de VFP.

Se define con OLEPUBLIC

```foxpro
DEFINE CLASS SaludoCom AS Session OLEPUBLIC
	cMensaje = "Hola desde VFP COM"

	PROCEDURE Saludar(nombre)
		RETURN "Saludos " + nombre + "! " + THIS.cMensaje
	ENDPROC
ENDDEFINE
```

###  Clases base comunes:

| Clase base |	Propósito |
|------------|------------|
| Custom	|Clase básica sin interfaz visual
|Session	| Ideal para clases COM (controla el contexto y el entorno de ejecución)
| Form	| Para crear ventanas
| CommandButton, Textbox, etc.	 | Para controles visuales
| CursorAdapter, DataEnvironment, etc.	| Para acceso a datos

Ejemplo de CommandButton: 
```foxpro
DEFINE CLASS CmdDEPT AS CommandButton
	name = "CmdDEPT"
	Caption = "DEPARTAMENTO"
	Top = 238
	Left = 445
	width = 107
	Height = 50
	ToolTipText =""
	FontBold= .T.
	FontSize = 8
	FontName = "Century Gothic"
	Style = 0
	Themes = .F.
	WordWrap = .t.
	SpecialEffect = 1
	visible  = .F.
	
	PROCEDURE Click
		DEPARTA=LEFT(THIS.TOOLTIPTEXT,12)
		COLORF=THIS.BACKCOLOR
		COLORL=THIS.FORECOLOR
		thisform.DEPARTAMENTO.click
   ENDPROC
ENDDEFINE

```

Este Se puede Agregar a Formulario actua de esta forma:

```foxpro
THISFORM.AddObject("NewBtn", "CmdDEPT")
&& donde primero indicamos en Nombre del objeto, y luego la Clase
```

### Notas finales
- Init() = constructor
- Destroy() = destructor
- Usa THIS para referirte al objeto actual
- Puedes heredar clases usando AS OtraClase
- Puedes agregar eventos/métodos visuales si defines la clase desde un VCX