# Automatización con COM y DLLs

Integra VFP con componentes externos: automatiza Word, Excel, Outlook o llama a funciones de DLLs personalizadas desde tus programas, asi como Classes COM.

Para ver como Se defne una Clase o Clase COM lea: [Clases VFP](./Class.md)

### `CREATEOBJECT(classname [, eParameter1 [, eParameter2]...])`

En Visual FoxPro (VFP), la función CREATEOBJECT() se utiliza para crear instancias de objetos COM (Component Object Model) o ActiveX. Esta función permite a un programa acceder y manipular objetos de otros lenguajes o aplicaciones, como Microsoft Excel, Word, o incluso otras aplicaciones COM personalizadas, desde dentro de un programa VFP.

`classname`: 
Es el nombre de la clase o el ProgID del objeto COM que se desea crear.  
Ejemplos:

`oExcel = CREATEOBJECT("Excel.Application")`	 

`eParameter` y `eParameter2` (opcionales)
Estos dos parámetros se pasan al método Init de la clase (cuando es una clase VFP, no COM).
Son útiles cuando tú defines una clase propia y necesitas pasarle argumentos durante su instanciación.

#### ¿Para qué sirven eParameter1 y eParameter2?
Son valores que tú puedes pasar al constructor (Init) de una clase definida en Visual FoxPro cuando usas CREATEOBJECT().


Importante: Estos solo aplican cuando el classname es una clase VFP, no un objeto COM externo (como Excel o Word).

```foxpro
DEFINE CLASS Cliente AS Custom
    cNombre = ""
    nEdad = 0

    PROCEDURE Init(nombre, edad)
        THIS.cNombre = nombre
        THIS.nEdad = edad
        ? "Cliente creado:", THIS.cNombre, "-", THIS.nEdad
    ENDPROC
ENDDEFINE

oCliente = CREATEOBJECT("Cliente", "Ana", 25)
```

### Limpiar de DLLs de la Memoria

```foxpro
    CLEAR DLLS [ DLLList ]
```
---

[Volver atrás](./Data/ODBC.md) | 	[Siguiente tema](./word_Excel.md)