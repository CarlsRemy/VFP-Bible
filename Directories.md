# 📁 Manejo de Directorios y Archivos en Visual FoxPro 9

## 📂 Rutas y Utilidades

- **`ADDBS("Ruta")`**  
  Asegura que una ruta termine con `\`.  
  Ejemplo: `ADDBS("C:\Datos\texr.pdf")` devuelve `"C:\Datos\"`.

- **`FULLPATH("archivo.txt")`**  
  Devuelve la ruta absoluta del archivo.

- **`FORCEEXT("documento", "txt")`**  
  Cambia o agrega la extensión: `"documento.txt"`.

- **`JUSTEXT("documento.pdf")`**  
  Devuelve la extensión del archivo: `"pdf"`.

- **`JUSTSTEM("documento.pdf")`**  
  Devuelve solo el nombre sin la extensión: `"documento"`.

---

## 🗂️ Manejo de Directorios

- **`DIRECTORY("Ruta", 1)`**  
  Verifica si la ruta existe y lista archivos y subcarpetas.  
  El parámetro `1` incluye subdirectorios. Retorna `.T.` o `.F.`.

- **`ADIR(laCarpeta, "*.txt")`**  
  Llena un arreglo con los archivos `.txt` del directorio actual.

- **`MKDIR "nuevaCarpeta"`** / **`MD`**  
  Crea una nueva carpeta.

- **`RMDIR "nuevaCarpeta"`** / **`RD`**  
  Elimina una carpeta vacía.

---

## 🧹 Eliminación de Archivos

- **`DELETE FILE "archivo.txt"`** / **`ERASE "archivo.txt"`**  
  Elimina un archivo del disco.

---

## 🧪 Verificación de Existencia

- **`FILE("archivo.txt")`**  
  Verifica si existe un archivo o directorio.

- **`ISFILE("archivo.txt")`**  
  Verifica si existe y si es un archivo (no carpeta).

---

## 📄 Funciones de Bajo Nivel para Archivos

Visual FoxPro permite trabajar directamente con archivos usando handles y control detallado.

### 🛠 Crear y Abrir Archivos

- **`FCREATE(cFileName [, nAttribute])`**  
  Crea un archivo (sobrescribe si existe).  
  Atributos opcionales:

  | Valor | Atributo        |
  |-------|-----------------|
  | 0     | Normal          |
  | 1     | Solo lectura    |
  | 2     | Oculto          |
  | 4     | Sistema         |

- **`FOPEN(cFileName [, nMode])`**  
  Abre un archivo existente. Devuelve un handle (número) o -1 si falla.  
  Modos de apertura:

  | Valor | Modo de acceso              |
  |-------|-----------------------------|
  | 0     | Solo lectura                |
  | 1     | Solo escritura              |
  | 2     | Lectura y escritura         |
  | 10    | Solo lectura compartida     |
  | 11    | Solo escritura compartida   |
  | 12    | Lectura/escritura compartida|

---

### ✏️ Lectura, Escritura y Posicionamiento

- **`FREAD(nHandle, nBytes)`**  
  Lee `nBytes` del archivo abierto.

- **`FWRITE(nHandle, cTexto [, nBytes])`**  
  Escribe texto en el archivo.

- **`FSEEK(nHandle, nOffset [, nOrigin])`**  
  Mueve el puntero del archivo:

  | Valor | Desde                     |
  |-------|---------------------------|
  | 0     | Inicio del archivo        |
  | 1     | Posición actual           |
  | 2     | Final del archivo         |

- **`FEOF(nHandle)`**  
  Retorna `.T.` si se ha llegado al final del archivo.

- **`FCLOSE(nHandle)`**  
  Cierra el archivo abierto.

---

## 🧾 Lectura/Escritura de Texto

- **`FILETOSTR("archivo.txt")`**  
  Lee todo el contenido del archivo como cadena.

- **`STRTOFILE(cTexto, "archivo.txt", 1)`**  
  Guarda el contenido de `cTexto` en un archivo.  
  - `1` = Sobrescribe  
  - `2` = Agrega al final

---

## 📌 Archivos Temporales

- **`TEMPFILE()`**  
  Devuelve un nombre único de archivo temporal con ruta completa.  
  Utiliza internamente `SYS(2023)` y `SYS(2015)`.

- **`SYS(2015)`**  
  Genera un nombre único de archivo (sin ruta).

- **`SYS(2023)`**  
  Devuelve la ruta del directorio temporal del sistema.

---


[Volver atrás](./Types/Number.md) |  	[Siguiente tema](./Data/Cursors.md)