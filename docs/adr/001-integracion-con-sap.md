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
