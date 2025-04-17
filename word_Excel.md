# Integración con Microsoft Excel


Ejemplo basico:
```foxpro
oExcel = CREATEOBJECT("Excel.Application")
oExcel.Visible = .T. && Muestra Excel

oBook = oExcel.Workbooks.Add()
oSheet = oBook.Sheets(1)

oSheet.Cells(1,1).Value = "Nombre"
oSheet.Cells(1,2).Value = "Edad"

oSheet.Cells(2,1).Value = "Juan"
oSheet.Cells(2,2).Value = 30

* Guardar archivo
oBook.SaveAs("C:\datos.xlsx")
oExcel.Quit()
RELEASE oExcel

```

- Abrir un Archivo en Excel

```foxpro
oExcel = CREATEOBJECT("Excel.Application")
oExcel.Workbooks.Open("Archivo.xlsx")
oSheet = oBook.Sheets(1) && Seccionar hoja 
```

- Pegar de Vfp a Excel

```foxpro
oSheet.range("A2").Select && Selecionar celda 1
_VFP.DataToClip('TMP',,3) && tabla VFP a Papelera 

oSheet.ActiveSheet.PasteSpecial

oSheet.Rows("7:7").Select && Selecionar Titulos de la abla BDF
oSheet.Selection.Delete  
oSheet.ActiveWorkbook.Save
oSheet.Application.CutCopyMode = .F.
oSheet.ScreenUpdating = .T.
```

-  Insertar fórmulas

```foxpro
oSheet.Cells(1,1).Value = "Subtotal"
oSheet.Cells(1,2).Value = 100
oSheet.Cells(2,1).Value = "ITBIS"
oSheet.Cells(2,2).Formula = "=B1*0.18"
oSheet.Cells(3,1).Value = "Total"
oSheet.Cells(3,2).Formula = "=B1+B2"
```
Puedes usar cualquier fórmula de Excel tal cual: =SUM(A1:A5), =IF(...), =VLOOKUP(...), etc.

---
Cambiar formato de celdas
```foxpro
oSheet.Range("A1:B1").Font.Bold = .T.
oSheet.Columns("A:B").AutoFit()
```

## Word y las Plantillas

Imagina que tienes un documento llamado plantilla.docx con el siguiente texto:

```txt
Estimado <NOMBRE>,

Gracias por su compra del producto <PRODUCTO>.

Fecha: <FECHA>
```

En VFP puedes usar la fincion **Find** de Word para realizar la busqueda en el documento y luego remplazarla.

```foxpro
oWord = CREATEOBJECT("Word.Application")
oWord.Visible = .T.

oDoc = oWord.Documents.Open("C:\plantilla.docx")

* Reemplazar campos
WITH oWord.Selection.Find
	.ClearFormatting
	.Replacement.ClearFormatting
	.Text = "<NOMBRE>"
	.Replacement.Text = "Carlos Pérez"
	.Execute(.T., .F., .F., .F., .F., .F., .F., 1, .F., , 2)
ENDWITH

WITH oWord.Selection.Find
	.Text = "<PRODUCTO>"
	.Replacement.Text = "Laptop Dell"
	.Execute(.T., .F., .F., .F., .F., .F., .F., 1, .F., , 2)
ENDWITH

WITH oWord.Selection.Find
	.Text = "<FECHA>"
	.Replacement.Text = DTOC(DATE())
	.Execute(.T., .F., .F., .F., .F., .F., .F., 1, .F., , 2)
ENDWITH

* Guardar como nuevo documento
oDoc.SaveAs("C:\documento_final.docx")
oWord.Quit()
RELEASE oWord
```

---

[Volver atrás](./Dll.md) | 	[Siguiente tema](./Errors.md)