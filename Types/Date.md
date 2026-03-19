## Funcines para Trabajar con Date

- `GOMONTH(dFecha, nMeses)`   
La joya de la corona para cálculos de vencimientos. Suma o resta meses exactos respetando si el año es bisiesto o si el mes tiene 30/31 días.

```prg
	ldVencimiento = GOMONTH(DATE(), 1) && Exactamente un mes después
	ldPasado = GOMONTH(DATE(), -3)      && Hace 3 meses


D_FECHA2 = GOMONTH(D_FECHA , 0) - DAY(GOMONTH(D_FECHA , 0)) && Ultimo dia de Mes Anterior
D_FECHA1 = GOMONTH(D_FECHA2, 0) - (DAY(GOMONTH(D_FECHA2 , 0) -1)) && Dia 1 del mes Anterior
```

- `CTOD() | DTOC()`   
Para evitar errores de formato (DMY vs MDY) al convertir texto a fecha:
CTOD("^2026-03-19"): El formato ^ es universal (Año-Mes-Día). No importa cómo esté configurado el Windows del cliente, siempre funcionará.   
DTOC(DATE(), 1): Devuelve la fecha como "20260319". Perfecto para nombres de archivos o índices.

- `DOW() | CDOW()` (Días de la semana)    
DOW(DATE()): Devuelve un número del 1 al 7.  
CDOW(DATE()): Devuelve el nombre del día (ej: "Thursday").  
Tip: DOW(ldFecha, 2) hace que el Lunes sea el día 1. 

- `QUARTER()`   
Devuelve el trimestre (1-4) de una fecha. Ideal para reportes contables

- `MDY() | DMY()`   
Convierten una fecha a formato de texto largo rápidamente:
```prg
? MDY(DATE()) && "March 19, 2026"
? DMY(DATE()) && "19 March 2026"
```

- `WEEK()`   
Calcula el número de semana del año (1-52). Muy útil para reportes de producción o ventas semanales:
```prg
lnSemana = WEEK(DATE(), 1, 1) && El segundo parámetro define el modo de cálculo
```