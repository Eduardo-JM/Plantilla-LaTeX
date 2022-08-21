# Plantilla-LaTeX

Esta plantilla es propuesta para el desarrollo del protocolo de investigación pedido en la **Unidad Profesional Interdisciplinaria en Ingeniería y Tecnologías Avanzadas**. Es importante saber que esta plantilla **NO ES OFICIAL** pero es puesta a tu disposición para que la puedas usar de acuerdo a cómo te convenga.

## Utilizar esta plantilla

Yo recomiendo altamente utilizar un gestor de versiones para no perder tus avances y poder acceder a ellos fácilmente desde la nube. 

Si usas instalación local de LaTeX, por favor lee la guía de [como hacer un fork en Github](https://docs.github.com/en/get-started/quickstart/fork-a-repo).

Si usas otro gestor de versiones, por favor lee su propia guía para importar, proyectos desde Github o descarga los archivos de github con el botón `Code > Download Zip`

Si usas un editor como [Overleaf](https://www.overleaf.com/learn/how-to/How_do_I_connect_an_Overleaf_project_with_a_repo_on_GitHub%2C_GitLab_or_BitBucket%3F) o [Papeeria](https://www.papeeria.com/help/git/sync), lee su propia guía para conectarlo al repositorio

### Requerimientos

* Se usó la distribución TeX Live 2022: El único paquete que requiere esta versión o superior es tabularray, pues fue incluido recientemente.
* Se usa el motor de compilación XeLaTeX o LuaLaTeX
* La compilación dada que hace uso de la externalización debe incluir el flag `--shell-escape`

### Ejemplo de compilación completa

```
xelatex -synctex=1 -interaction=nonstopmode --shell-escape %.tex
makeindex -t %.glg -s %.ist -o %.gls %.glo
makeindex -t %.alg -s %.ist -o %.acr %.acn
biber %
xelatex -synctex=1 -interaction=nonstopmode --shell-escape %.tex
```

**Descripción de lo sucedido:**

* Se compila el archivo con XeLaTeX
* Se indexa el archivo con MakeIndex
  * 1 vez para el glosario
  * 1 vez para las abreviaciones y acrónimos
* Se vuelve a compilar con XeLaTeX

## Estructura

La arquitectura del documento está seccionada en partes mínimas que ayudan a tener un buen manejo de de los paquetes,  configuraciónes, comandos y contenido del protocolo de investigación. Las partes fundamentales que identificaremos son:

### Preámbulo

Consiste de 4 archivos más el propio `Preámbulo.tex`:

* `Packages.tex`: En este archivo se encuentran todos los paquetes que se utilizarán a lo largo del documento. Revisa este documento pues ya tiene algunos paquetes cargados que en el momento del desarrollo de esta plantilla se consideraron indispensables o extremadamente útiles. Su uso está totalmente a tu consideración pero es sugerido su uso.
* `Config.tex`: En este archivo se encuentran todas las configuraciones de los paquetes importados en el documento anterior más las configuraciones generales del documento.
* `CustomKeys.tex`: En este archivo se definen algunas llaves que son utilizadas por los paquetes, por ejemplo, paquetes dependientes de PGF y llaves personalizadas de enumitem
* `ComplexCommands.tex`: Aunque no son realmente comandos complejos, su intención es que en este documento vengan algunos comandos definidos por el usuario.

Dentro del propio documento, se encuentran algunos comandos referidos al documento:

- Comandos para imprimir el autor, fecha y título del documento
- Comandos para incluir documentos configurados como externalizables
- Se definen el autor, fecha y título del documento

**Importante:** Conserva el orden en el que son importados los documentos.

### Documento

Se separa por documentos en carpetas:

* `beginning/`: En esta carpeta se encuentran los documentos que crean la portada y resumen
* `chapters/`: Propiamente los capítulos del documento
* `appendix/`: Se incluyen todos los apéndices a utilizar; como ejemplo se incluyeron algunas páginas de la *datasheet* de Arduino UNO A000066
* `bib/`: En esta carpeta se definen 3 archivos relacionados a la bibliografía, abreviaciones, acrónimos y glosario del documento
* `tikz/`: El propósito de esta carpeta es para guardar las imágenes tikz que se usen a lo largo del documento para externalizarlas
* `diagrams/`: El propósito de esta carpeta es para guardar los diagramas (*forest*) que se usen a lo largo del documento para externalizarlas
* `tcolorbox/`: El propósito de esta carpeta es para guardar las *color boxes* que se usen a lo largo del documento para externalizarlas

---

#### Importante

---

Si se hace uso de la externalización, se deben crear las carpetas **`pictures`** y **`boxes`**, de lo contrario saltará un error pues LaTeX no creará estas carpetas y no podrá escribir los archivos generados

---

#### .gitignore

---

Por favor lean y modifiquen lo que necesiten del `.gitignore`; por defecto está configurado para ignorar todos los archivos a excepción de unos específicos y unos por extensiones; pero eso ya está a su decisión, si no quieren ignorar ningún archivo, sólo basta con eliminar el contenido del archivo
