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

### Estructura de Estilos

En general, se econtró que la forma en la que se declara un estilo es la siguiente (en la estructura XML):
```xml
<style:style style:name="nombre" style:family="familia" [style:parent-style-name="Default"]>
----Definición de estilos particulares
</style:style>
```

Examinando el documento de experimentación que se creó (la hoja de cálculo), se puedieron identificar cuatro (4) entidades que poseen su nombre definido igual que sus estilos particulares, siendo éstas las siguientes:

*	**Tabla:** Declaración de estilo para la entidad tabla.
	*	**Ejemplo:**
	```xml
    <style:style style:name="ta1" style:family="table" style:master-page-name="Default">
    	<style:table-properties table:display="true" style:writing-mode="lr-tb"/>
</style:style>
    ```
	*	Atributo **name**: En este caso el atributo toma el valor `"ta<i>"` donde *i* corresponde a un número entero entre 1 y *n*.
	*	Atributo **family**: Para la entidad *table* el valor de este atributo es `"table"`.

*	**Fila:** Declaración de estilo para la entidad fila.
	*	**Ejemplo:**
	```xml
    <style:style style:name="ro1" style:family="table-row">
    <style:table-row-properties style:row-height="12.81pt" fo:break-before="auto" style:use-optimal-row-height="true"/>
</style:style>
    ```
    *	Atributo **name**: En este caso el atributo toma el valor `"ro<i>"` donde *i* corresponde a un número entero entre 1 y *n*.
	*	Atributo **family**: Para esta entidad el valor de este atributo es `"table-row"`.

*	**Columna:** Declaración de estilo para la entidad columna.
	*	**Ejemplo:**
	```xml
    <style:style style:name="co1" style:family="table-column">
    <style:table-column-properties fo:break-before="auto" style:column-width="64.01pt"/>
</style:style>
    ```
    *	Atributo **name**: En este caso el atributo toma el valor `"co<i>"` donde *i* corresponde a un número entero entre 1 y *n*.
	*	Atributo **family**: Para esta entidad el valor de este atributo es `"table-column"`.

*	**Celda:** Declaración de estilo para la entidad celda.
	*	**Ejemplo:**
	```xml
    ```

#### Valores de atributos
Los estilos de *Celda* son de particular interés, ya que entregan la información explícita tanto del texto de una celda determinada como de su fondo, etc. Es importante tener en cuenta que dentro de la definición de un estilo, es decir dentro de las etiquetas `<style:style>  </style:style>` se puede encontrar lo siguiente:

   * Atributos de `<style:style atributos..>` pueden ser:
   	*	`style:name="identificador"`: Como se mencionaba anteriormente corresponderá al nombre o *etiqueta* que se le da al estilo y con el cual será referenciado a lo largo del documento (hoja de cálculo). Puede tomar valores de la forma: `"ce<i>"` (celdas), `"T<i>"` (estilos para texto).
   	*	Son de particular interés los siguientes estilos que se indican al interior de las etiquetas `<style:style>  estilos  </style:style>`:
   		*	`<style:table-cell-properties  .... />` Cuyos atributos pueden ser:
   			*	`fo:background-color="#8DB4E2"`: Que indicará el color de fondo de la celda.

   		*	`<style:text-properties .../>` Cuyos atributos pueden ser:
   			*	`fo:color="#1F497D"`: Que indicará el color del texto.
   			*	`fo:font-size="18pt"`: Que indicará el tamaño de la letra.
   			*	`fo:font-style="italic"`
   			*	`style:text-underline-style="solid"`
   			*	`fo:font-weight="bold"`
   		*	`<style:paragraph-properties .../>`: Cuyos atributos pueden ser:
   			*	`fo:text-align="center"`: Que indicará la alineación del texto en la celda, los valores posibles para este atributo son: `center`, `right` y `left`.

