# 🐺 Introduccion

Visual FoxPro (VFP) es un lenguaje de programación orientado a objetos y un sistema de gestión de bases de datos (DBMS) desarrollado por Microsoft, que permite crear aplicaciones de escritorio (principalmente para Windows) con acceso directo y muy eficiente a datos.

## Sintaxis básica

Visual FoxPro tiene una sintaxis muy simple y legible. No se usan llaves {} ni punto y coma ; para delimitar bloques de código. En su lugar, se usan palabras clave como IF ... ENDIF, FOR ... ENDFOR, DO

❌ No se usan:
Llaves {} para bloques de código

Punto y coma ; para cerrar instrucciones (aunque se puede usar para continuar líneas)

Indentación obligatoria (aunque se recomienda para legibilidad)

```foxpro
IF edad > 18
  ? "Mayor de edad"
ELSE
  ? "Menor de edad"
ENDIF
```

## Palabras clave de apertura y cierr

| Bloque lógico	 | Inicio	 |  Fin |
|----------------|---------|------|
| Condicional IF | IF      | ENDIF|
|Bucle FOR	     | FOR	   | ENDFOR
|Bucle DO WHILE	 | DO WHILE	|ENDDO |
|Equivalente de switch    |	DO CASE	| ENDCASE |
|Función / Procedimiento	| FUNCTION / PROCEDURE	|ENDFUNC / ENDPROC |
|Definición de clase |	DEFINE CLASS |	ENDDEFINE |

##  Operadores comunes
```foxpro
=     && asignación
= / ==   && comparación, si se usa = no diferncia plurales
<>    && distinto
AND   && y lógico
OR    && o lógico
NOT   && negación
```

---
#### Sintaxis de CASE

```foxpro
DO CASE
	CASE x = 1
		? "Uno"
	CASE x = 2
		? "Dos"
	OTHERWISE
		? "Otro"
ENDCASE
```

#### Sintaxis de For y Scan


```foxpro
FOR i = 0 TO 45
  ? "Valor de i:", i
ENDFOR
```
Con incremento personalizado

```foxpro
FOR i = 0 TO 100 STEP 10
  ? i  && Imprime: 0, 10, 20, ..., 100
ENDFOR
```
#### scan

```foxpro
USE clientes
SCAN
  ? nombre, edad
ENDSCAN
```
####  ¿Y EOF()?

`EOF()` significa "End Of File", es decir, si se llegó al final del archivo o tabla.

Por lo general, `EOF()` se usa más con bucles `DO WHILE`, así:

```foxpro
USE clientes
GO TOP
DO WHILE !EOF()
  ? nombre
  SKIP
ENDDO
```

[Volver atrás](./readme.md) | 	[Siguiente tema](./Types/String.md)