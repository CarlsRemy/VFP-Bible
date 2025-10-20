## ⚙️ Ejecución de Comandos y Scripts Dinámicos

Visual FoxPro permite ejecutar comandos del sistema, scripts externos y evaluaciones de código en tiempo de ejecución, lo que brinda una gran flexibilidad para automatizar tareas y adaptarse a diferentes entornos o entradas.


- **EXECSCRIPT("DO prueba")**   
Ejecuta código VFP como string

- **`RUN` / `!`**   
Ejecuta un comando del sistema operativo.

	```foxpro
	RUN notepad.exe
	!dir *.dbf
	```

	Puedes pasar el comando desde una variable:

	```foxpro
	lcCommand = "notepad.exe"
	RUN /N &lcCommand  && Ejecuta sin mostrar la ventana de consola
	```
---
### 🔁 `&NombreVariable`
Ejecuta el contenido de una variable como si fuera código (evaluación macro).

Cuando Visual FoxPro encuentra el símbolo & seguido de una palabra, interpreta esa palabra como el nombre de una variable. Si la variable existe, su valor se sustituye y evalúa como si fuera parte del código.Permite generar bloques de código dinámicamente dentro de una construcción TEXT o un String

```foxpro
lcMacro = "DO miProceso"
&lcMacro

name = "VfP"
? "Estoy Aprendiendo &name"
* Eso Imprimera: Estoy Aprendiendo Vfp
```
uso del operador macro (&) en nombres de propiedades o controles de manera dinámica. Vamos a desglosarlo

```foxpro
kw = "09."
THIS.P&kw.Caption = ""
** es equivalente a: THIS.P09.Caption = ""
```

### ¿Para que sirve?
Esto es útil cuando quieres acceder dinámicamente a múltiples controles (por ejemplo, en un ciclo), sin tener que escribir cada uno por nombre

### && Comentario en linea
En Visual FoxPro, && es el operador de comentario de una línea, por lo tanto todo lo que esté a su derecha en la misma línea es ignorado por el compilador/interprete.

---

### `SET MACROEXPANSION ON|OFF`

Activa o desactiva la expansión de macros (&). Muy útil para depurar o controlar ejecución dinámica.


### `SHELL`
Alternativa a RUN, permite ejecutar comandos del sistema operativo.

```foxpro
SHELL "dir"
```

## ¿Qué es _VFP?

`_VFP` es una variable de sistema que da acceso al Application Object de Visual FoxPro.

### Algunos miembros útiles de _VFP

- `_VFP.DataToClip()`  
Copia al portapapeles los datos del área de trabajo actual (puede usarse para exportar datos a Excel, por ejemplo).

- `_VFP.Do(filename)`
Ejecuta un PRG o procedimiento.

- `_VFP.DoCmd(cComando)`  
Ejecuta una línea de comando como si la escribieras en la ventana de comandos.

- `_VFP.Eval(cExpresión)`   
Evalúa una expresión en forma de cadena y retorna el resultado. Similar a EVALUATE() pero con un poco más de tolerancia a expresiones compuestas.

	```foxpro
	_VFP.SetVar("mPrecio", 120)
	_VFP.DoCmd("STORE mPrecio * 1.18 TO mTotal")
	? mTotal  && Resultado: 141.6

	? _VFP.Eval("mTotal / 2")  && Resultado: 70.8
	```

- `_VFP.SetVar(cNombreVar, xValor)`  
Asigna un valor a una variable en tiempo de ejecución, como si usaras STORE xValor TO cNombreVar, pero de forma dinámica.

- `_VFP.ActiveProject`
Devuelve el proyecto actualmente activo en el IDE (el .PJX abierto).

- `_VFP.Projects`
Colección de todos los proyectos abiertos actualmente (normalmente solo hay uno).

- `_VFP.Projects.Item(1).Build(lcSaveAs, 3)`   
Este comando compila el proyecto en un tipo específico de archivo ejecutable o librería.

	```foxpro
	lcSaveAs = "MiApp.exe"
	_VFP.Projects.Item(1).Build(lcSaveAs, 3)  && 3 = EXE
	```

	| valor |	Tipo de build |
	|-------|---------------|
	| 1     | APP           |
	| 2     | DLL           |
	| 3     | EXE           |


- `_VFP.Caption, _VFP.Visible, _VFP.Height, etc.`   
Permiten modificar el entorno de ejecución de VFP como si fuera una ventana más.

[Volver atrás](./evaluations.md) | 	[Siguiente tema](./printer.md)