# Regristro de decisiones de arquitectura

### Introducción

Una decisión de arquitectura es una elección sobre el diseño, propuesta y/o solución de un requerimiento funcional o no funcional sobre un sistema de software. Estas pueden ser por ejemplo la decisión sobre que tecnología y librerias se utilizarán en el proyecto, el tipo de bases de datos, el diseño de la arquitectura, etc.

En este documento se estarán registrando todas las decisiones de arquitectura que tomemos a lo largo del proyecto de **[proyect_name]**.

Para más información sobre esta técnica de registro de decisiones de arquitectura, pueden encontrarla en [Thoughtworks Radar](https://www.thoughtworks.com/radar/techniques/lightweight-architecture-decision-records).

## Índice

- [Template](https://github.com/Gonzacerbelli/ADRs/#template)
- [Ejemplo](https://github.com/Gonzacerbelli/ADRs/#ejemplo)
- [Crear un nuevo ADR](https://github.com/Gonzacerbelli/ADRs/#crear-un-nuevo-adr)
- [ADRs en Microsoft Word](https://github.com/Gonzacerbelli/ADRs/#adrs-en-microsoft-word)
- [Otras herramientas](https://github.com/Gonzacerbelli/ADRs/#otras-herramientas)

## Template

El template a utilizar para generar un nuevo registro de decisión es la siguiente:

    ## ADR [NNN] - [title]

    ### Fecha
    Indicar en qué fecha se tomó el registro de la decisión, en formato YYYY-MM-DD.

    ### Contexto y requerimiento

    Cuál es el problema o el tema por el cual estamos proponiendo una nueva decisión de arquitectura, un cambio o una solución. Agregar link de JIRA si existe la tarea.

    ### Alternativas evaluadas
    Cuales son las alternativas propuestas o consideradas para la nueva decisión, el cambio o la solución que se está proponiendo.

    ### Decisión tomada
    Cuál es la nueva decisión, el cambio o la solución que se eligió.

    ### Participantes
    Quienes son los participantes en la toma de la decisión.

    ### Estado
    Cuál es el estado: propuesto, aceptado, deprecado, rechazado.

    ### Consecuencias y comentarios
    Cuales son las ventajas y desventajas de aplicar esta nueva decisión o cambio, qué será más fácil o difícil.

    ### Decisiones relacionadas
    Cuales son las decisiones existentes en este documento que se relacionen con esta.

Este template se encuentra en [docs/adr/template.md](https://github.com/Gonzacerbelli/ADRs/blob/main/docs/adr/template.md).

## Ejemplo

    ## ADR 001 - Integración con SAP

    ### Fecha

    2020-10-12

    ### Contexto y requerimiento

    Con el fin de consumir información ya existente sobre los usuarios, órdenes y estados de los pedidos, necesitamos realizar una integración con el sistema de gestión SAP.
    Desde el equipo de desarrollo se realiza una revisión y descubrimiento de datos que los usuarios necesiten visualizar en el nuevo sistema y que sean obtenidos desde SAP.

    ### Alternativas evaluadas

    - Realizar una integración a una API REST que nos brinde la información necesaria en cada uno de los casos. Para esto, eventualmente se estarán evaluando proveedores para desarrollar dicha API.
    - Mientras esta integración no esté disponible, se propone hacer una réplica de la base de datos con el fin de mockear los datos y que desde el equipo de desarrollo se pueda avanzar, utilizando datos reales.
    - Realizar el desarrollo de un bot mediante RPA (ETL) que realice la extracción de datos de las bases de datos y reportes de SAP e importe dicha información en una base de datos PostgreSQL en la instancia de AWS, a fin de consumir desde los microservicios esa información.

    ### Decisión tomada

    Se realizará el desarrollo de un bot mediante RPA que realice la extracción de datos de las bases de datos y reportes de SAP e importe dicha información en una base de datos PostgreSQL en la instancia de AWS, a fin de consumir desde los microservicios esa información.
    Eventualmente se estará trabajando en una integración mediante API REST con SAP para reemplazar este bot de extracción de datos y la réplica de la base de datos.

    ### Participantes

    Gonzalo Cerbelli, Nombre Apellido

    ### Estado

    Aprobado el día 2020-12-17

    ### Consecuencias y comentarios

    - Ya contamos con un usuario del ambiente de QA de SAP para el bot de RPA. Debemos verificar si debemos gestionar la cuenta de SAP para el entorno productivo.
    - El proveedor debe entregar a su equipo de TI los requisitos de la API que exponga los datos necesarios de SAP.
    - Desde el equipo de innovación no se tiene la certeza de la participación y asignación con la que vamos a contar por parte del equipo de TI.
    - Si el equipo de TI se retrasa con el desarrollo de esta API necesaria, ese retraso impactaría directamente en los tiempos de desarrollo e integraciones propuestos por Wolox.
    - Desarrollar un bot RPA es mucho menos costoso a nivel económico y de esfuerzos (este desarrollo es viable en los tiempos y fechas comprometidas de este proyecto cerrado).
    - El desarrollo de un bot RPA es más riesgoso a nivel integración por indisponibilidades y riesgos al simular un comportamiento humano, es una aplicación poco robusta

    ### Decisiones relacionadas

    Todavía no existen decisiones realcionadas a esta.


Este ejemplo se encuentra en [docs/adr/001-integracion-con-sap.md](https://github.com/Gonzacerbelli/ADRs/blob/main/docs/adr/001-integracion-con-sap.md).

## Crear un nuevo ADR

1.  Crear la carpeta `docs/adr` en tu proyecto.
2.  Copiar el archivo `template.md`a `NNN-titulo-con-guiones`, donde `NNN` indica el siguiente número en secuencia.
3.  Editar el archivo `NNN-titulo-con-guiones`.
4.  Actualizar el archivo `docs/adr/README.md`.

Las decisiones estarán ubicadas en la carpeta `docs/adr`. Los documentos tendrán la nomenclatura `NNN-titulo-con-guiones.md` ([ADR-001](https://github.com/Gonzacerbelli/ADRs/blob/main/docs/adr/001-integracion-con-sap.md)), donde:

- El nombre del archivo utiliza un número consecutivo al último registro de decisión creado, y un título separado por guiones.
- El sufijo es `.md` porque es un archivo Markdown.

## ADRs en Microsoft Word

En el caso de que no sea posible utilizar este método para el registro de la toma de decisiones, contamos con un [template de ADRs](https://arcosdoradosgroup.sharepoint.com/:w:/s/ArquiteturaCorporativa/EVkUqBr08eBOonyPnvSToMEBEoO2MLhwp2qoqK7h6EaJUQ?e=lhUM6p) utilizando Microsoft Word y manteniendo las mismas entradas. Además este template cuenta con una tabla de versionado, el cual será de forma manual.
Las decisiones de arquitectura se crearán manteniendo el mismo formato: `ADR [NNN] - [title]` donde `NNN` es el número consecutivo al último registro de decisión creado.

## Otras herramientas

Existen varias herramientas para el registro de toma de decisiones de arquitectura, entre ellas:

- [madr](https://adr.github.io/madr/)
- [adr-tools](https://github.com/npryce/adr-tools)

Si bien estas herramientas apuntan a gestionar estos registros de forma más automatizada de lo que se propone en este documento, requieren de varios pasos (instalar paquetes la primera vez, ejecutar comandos específicos para la creación o forkear un repositorio) que complejizan la acción de registrar una nueva decisión de arquitectura. Además, estas herramientas cuentan con un template con algunas entradas menos respecto al propuesto.
