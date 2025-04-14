## Cursores y Tablas

En Visual FoxPro 9, las tablas DBF y los cursores son el corazón del manejo de datos. Saber cómo usarlos correctamente te permite crear aplicaciones robustas, rápidas y eficientes.

### ¿Qué es una tabla DBF?
Una tabla .DBF (DataBase File) es el formato nativo de base de datos de FoxPro. Contiene registros (filas) y campos (columnas) que pueden ser accedidos directamente sin necesidad de conexión a un servidor.

```prg
lTabla = "ejemplo"

IF !FILE("ejemplo.dbf")
	* Crear una tabla con diferentes tipos de campos
	CREATE TABLE ejemplo (
		nombre C(50),         && Campo de texto (carácter) de 50 caracteres
		edad N(3,0),          && Campo numérico con 3 dígitos, sin decimales
		salario N(8,2),       && Campo numérico con 8 dígitos, 2 decimales
		fecha_nacimiento D,   && Campo de fecha
		activo L,             && Campo lógico (booleano)
		descripcion M         && Campo memo para texto largo
	)
ENDIF 

CLOSE DATABASES                   && Cerrar Tablas
USE (lTabla) ALIAS TempConnecion && Usar la tabla con un Alias

&& Update

USE (lTabla) 
REPLACE nombre WITH "New Value" FOR nombre = ""
USE IN (lTabla) 
```

```prg
USE clientes EXCLUSIVE         && Abre la tabla "clientes.dbf" en modo exclusivo
APPEND BLANK                   && Agrega un nuevo registro vacío
REPLACE nombre WITH "Pedro"    && Cambia el valor del campo "nombre"
BROWSE                         && Muestra una tabla para editar manualmente
COPY TO copia.dbf              && Copia la tabla actual a un nuevo archivo DBF
DELETE                         && Marca el registro actual como eliminado
PACK                           && Elimina físicamente los registros marcados
ZAP                            && Borra todos los registros
```

### ¿Qué es un cursor?
Un cursor en VFP es una tabla temporal en memoria, generada típicamente mediante una instrucción SELECT. No se guarda en disco a menos que tú lo decidas.

```prg
SELECT nombre, ciudad FROM clientes WHERE activo = .T. INTO CURSOR clientes_activos
```
- INTO CURSOR: crea un cursor llamado clientes_activos
- Puedes modificarlo si agregas READWRITE:

```prg
* Crear un cursor
CREATE CURSOR mi_cursor (campo1 C(20), campo2 N(5,2))

* Insertar datos en el cursor
INSERT INTO mi_cursor (campo1, campo2) VALUES ("Valor1", 10.50)
INSERT INTO mi_cursor (campo1, campo2) VALUES ("Valor2", 20.75)
```

### Tipos De datos para Cursores y Tablas

- C (Carácter):
	- Almacena cadenas de texto (caracteres).
	- La longitud del campo debe especificarse entre paréntesis.

- N (Numérico):
	- Almacena números.
	- Se debe especificar la longitud total del número y la cantidad de decimales.

- I (Entero):
	- Almacena enteros (números sin decimales).

- F (Fecha):
	- Almacena fechas en formato YYYY-MM-DD.

- D (Fecha y hora):
	- Almacena fecha y hora en formato YYYY-MM-DD HH:MM:SS.

- L (Lógico):
	- Almacena valores lógicos (booleanos).

- M (Memo):
	- Almacena texto largo o grandes cantidades de datos, como descripciones extensas o documentos.

- B (Binario):
	- Almacena datos binarios. Usado para almacenar archivos o datos que no son texto (por ejemplo, imágenes o archivos).

- T (Timestamp):
	- Almacena fecha y hora con precisión de fracciones de segundo.

### Consultas 
Las consultas en VFP son muy parecidas a las Consultas de cualquier
entorno **SQL**, permitiendo usar **JOIN**, **WHERE**, **GROUP** , **HAVING** y **subConsultas**

```prg

SELECT Customer.Customer_ID, COUNT(*) ;
FROM TasTrade!Customer ;
JOIN TasTrade!Orders ;
ON Customer.Customer_ID=Orders.Customer_ID ;
WHERE YEAR(Orders.Order_Date)=1994 ;
GROUP BY 1 HAVING COUNT(*)>=10 ;
INTO CURSOR OrderCount

* Find all the customers with no orders.
SELECT * FROM Customer WHERE Customer_ID NOT IN (SELECT Customer_ID FROM Orders)

```
### Clausula Where

La cláusula WHERE puede usar comodines para encontrar cadenas mediante el operador LIKE (similar a LIKE()la función de FoxPro). Por alguna razón, los comodines que se usan aquí son "%" para cero o más caracteres y "_" para exactamente un carácter. Por lo tanto, para encontrar cualquier cadena que contenga la letra "j", la cláusula WHERE podría verse así:

```prg
WHERE cMyField LIKE "%j%"
```
El uso del operador LIKE y de comodines tiene consecuencias de optimización. En nuestras pruebas, la simple inclusión de LIKE cambia la optimización de un campo indexado de total a parcial. Usar un comodín al principio de la cadena no optimiza esa condición. Todo esto nos parece lógico, basándonos en nuestra comprensión del funcionamiento de Rushmore.

Dado que ocasionalmente podría necesitar realizar una búsqueda con comodines donde uno de los caracteres que busca es "%" o "_", también existe una palabra clave especial ESCAPE que permite especificar un carácter antes del comodín para indicar que no se trata de un comodín. Por ejemplo, para buscar en cMyField cadenas que empiezan con "_" y terminan con "_", pero con cualquier carácter intermedio, podría escribir:

```prg
WHERE cMyField LIKE "\_%\_" ESCAPE "\"
```
Esta cláusula dice que el carácter de escape es “\”, por lo que cualquier carácter comodín precedido por “\” debe tratarse como un carácter regular.

**IN** y **BETWEEN**. **IN** comprueba si el campo o expresión especificado está contenido en una lista dada.(**IN** es muy similar a **INLIST()**). Es útil para comprobar cosas como si el estado del cliente es uno de algún subconjunto, como ("PA", "NJ", "DE"). **BETWEEN** comprueba si el campo o expresión está en el rango especificado.

Estos tres operadores especiales (**LIKE**, **IN** y **BETWEEN**) pueden ir precedidos de **NOT** para elegir los registros que no coincidan con la condición especificada.


## Funciones 

- `ISDBF("archivo.dbf")`  
	verifica si es una tabla DBF

- `USED("alias")`  
	Devuelve .T. si el alias (tabla/cursor) está abierto.
	
- `DBUSED("archivo")`  
Verifica si el archivo DBF está abierto.

- `DBF("alias")`  
Devuelve la ruta completa del DBF abierto.

- `ALIAS()`  
Retorna el alias de la tabla actual.

- `FIELD(n)`  
Devuelve el nombre del campo número n de la tabla activa.

- `FCOUNT()`  
Número de campos de la tabla activa.

- `RECCOUNT()`  
Total de registros en la tabla.

- `RECNO()`  
Número del registro actual.

- `BOF()` / 	`EOF()`  
Devuelven .T. si está al principio o final de la tabla.
- `RLOCK()` / 	`FLOCK()`  
Bloquea registro o archivo completo.
- `ISREADONLY()`  
Retorna si el archivo está en modo solo lectura.

[Volver atrás](../introduction.md) | 	[Siguiente tema](./ODBC.md)