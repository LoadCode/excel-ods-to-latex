### Estructura de una hoja ODS (Libreoffice Calc)

A grandes rasgos, mediante la ingeniería inversa de un documento .*ods* podemos darnos cuenta que la estructura en XML es la siguiente:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<office:document-content>

    <office:scripts/>

    <office:font-face-decls>
    ... Iformación sobre tipos de fuentes
    </office:font-face-decls>


    <office:automatic-styles>
    ... Definición de los estilos de tabla, columnas, filas, celdas, etc
    </office:automatic-styles>

    <office:body>
        <office:spreadsheet>
            <table:calculation-settings table:automatic-find-labels="false"/>

            <table:table table:name="Sheet1" table:style-name="ta1">
            ...Declaración del contenido de la hoja de cálculo
            </table:table>

        <table:named-expressions/>
        </office:spreadsheet>
	</office:body>
</office:document-content>
```



