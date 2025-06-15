# Acceso a Datos Remotos

Conecta tu app con bases de datos externas como MySQL, SQL Server o PostgreSQL usando ODBC o conexiones nativas. Ejecuta consultas SQL directamente desde VFP.

## SQL Server

Si usamo una String de Coneccion:

```prg
lcConnStr = "DRIVER={SQL Server};SERVER=MI_SERVIDOR;" + ;
"DATABASE=mi_base;UID=usuario;PWD=clave"

lnConn = SQLSTRINGCONNECT(lcConnStr)
```

Si Usamos Una Conecion con ODBC:

```prg
lnConn = SQLCONNECT("mi_dsn", "usuario", "clave")
```

## SQLEXEC

Ejecuta una sentencia SQL sobre una conexión abierta.

```foxpro
IF SQLEXEC(nConn, "SELECT * FROM productos", "productosCursor") < 0
   AERROR(aError)
   ? "Error al ejecutar consulta: ", aError[2]
ENDIF
```

## SQLSETPROP
Permite establecer propiedades de la conexión como el modo asincrónico, tiempo de espera, etc.

```foxpro
SQLSETPROP(nConn, "Asynchronous", .F.)
SQLSETPROP(nConn, "ConnectTimeout", 15)
```

## SQLDISCONNECT

Cierra una conexión activa con la base de datos.

```foxpro
IF SQLDISCONNECT(nConn) = 1
  ? "Conexión cerrada correctamente"
ENDIF
```

## Conexión a Archivos DBF (locales o en red)

Los archivos .DBF son la base de datos nativa de VFP. Puedes abrirlos directamente sin necesidad de conexión:

```prg
USE \\servidor\datos\clientes.dbf SHARED
BROWSE
```

- SHARED: permite que otros usuarios accedan al mismo tiempo.

- EXCLUSIVE: bloquea el archivo para uso exclusivo.

También puedes trabajar con múltiples tablas en una misma ruta:

```prg
SET PATH TO \\servidor\datos
USE clientes
USE ventas IN 0

```
Si se tiene el Driver ODBC DBF para VFP

```prg
cn  ='Driver={Microsoft Visual FoxPro Driver};SourceType=DBF;SourceDB=c:\bak;Exclusive=No;Collate=Machine;NULL=NO;DELETED=NO;BACKGROUNDFETCH=NO;'
cn = SQLSTRINGCONNECT(cn)

select * from tablax
```

## Conección a MySQL
Para conectar con MySQL, necesitas el MySQL ODBC Driver instalado.

```prg
lcConnStr = "DRIVER={MySQL ODBC 8.0 ANSI Driver};" + ;
"SERVER=localhost;DATABASE=mi_base;" + ;
"UID=usuario;PWD=clave;PORT=3306"

lnConn = SQLSTRINGCONNECT(lcConnStr)
```
[Volver atrás](./Cursors.md) | 	[Siguiente tema](../Dll.md)