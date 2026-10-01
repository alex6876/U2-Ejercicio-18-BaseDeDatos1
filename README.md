# Base de Datos de Gestión de Producción Industrial y Línea de Montaje



Proyecto enfocado en la modelación Entidad-Relación (DER / MER) e implementación de base de datos relacional para la gestión de procesos de fabricación industrial, administración de productos, estructura de lista de materiales (BOM / Composición), órdenes de fabricación, líneas de montaje, asignación de personal, unidades producidas y controles de inspección de calidad.

---

## Descripción

El sistema modela una estructura de datos relacional para el control operativo y la trazabilidad de procesos de manufactura industrial. Permite definir el catálogo de productos terminados y sus componentes asociados mediante detalles de composición (BOM - *Bill of Materials*), programar y dar seguimiento a las órdenes de fabricación en las distintas líneas de montaje, gestionar los empleados intervinientes y registrar el loteo o unidades producidas junto con sus correspondientes inspecciones y controles de calidad.

---

## Funcionalidades e Implementación

### Entidades y Atributos

* Producto:


* id_Codigo articulo: Clave primaria única identificadora del producto.


* nombre comercial: Nombre comercial del artículo producido.


* descripción: Descripción técnica o comercial del producto.


* tiempo fabricación: Tiempo estimado o estándar requerido para su elaboración.


* tipo producto: Categorización o clasificación del producto.




* Componente:


* id_codigo componente: Clave primaria identificadora del componente o materia prima.


* nombre: Denominación del componente.


* decripción: Detalles o especificaciones del insumo.


* tipo de componente: Clasificación de la materia prima o parte.


* unidad de producto: Unidad de medida utilizada (ej. piezas, kg, metros).




* Detalle BOM producto:


* id_Codigo articulo: Clave foránea referenciando al producto.


* id_codigo componente: Clave foránea referenciando al componente necesario.


* cantidad necesaria: Cantidad requerida del componente para la fabricación del producto.




* Composición:


* id_codigo componente: Clave foránea referenciando al componente base o subensamble.


* cantidad necesaria: Proporción requerida en la estructura del ensamble.




* Orden de Fabricación:


* id_Numero de orden: Clave primaria identificadora de la orden de producción.


* fecha de emision: Fecha de creación o emisión de la orden.


* cantidad planificada: Unidades programadas a fabricar.


* estado: Estado operativo de la orden (ej. en proceso, pendiente, finalizada).


* fecha de finalización: Fecha real o estimada de conclusión del lote.




* Linea de montaje:


* id_Codigo linea: Clave primaria identificadora de la línea de ensamblado o producción.


* descripción: Detalle de la infraestructura o sección de la línea.


* supervisor a cargo: Responsable asignado a la línea.


* capacidad producción: Capacidad nominal o volumen máximo de procesamiento.


* ubicación: Sector o planta física donde se encuentra la línea.




* Empleado:


* id_empleado: Clave primaria identificadora del trabajador.


* DNI: Documento Nacional de Identidad.


* nombre: Nombre del empleado.


* apellido: Apellido del empleado.


* Rol: Cargo o función dentro de la planta (ej. operador, supervisor, inspector).




* Unidad:


* id_Unidad: Clave primaria identificadora de la unidad o lote fabricado.


* cantidad producida: Número de piezas efectivas logradas en el lote.


* fecha producida: Fecha y hora de finalización del empaque/producción.


* estado: Condición de la unidad (ej. aprobada, para reproceso, rechazada).




* Inspección de calidad:


* id_Unidad: Clave foránea referenciando a la unidad o lote inspeccionado.


* cantidad producida: Cantidad evaluada durante la auditoría.


* fecha de producción: Registro de fecha de la evaluación técnica.


* estado: Dictamen del control (ej. Aprobado, Rechazado).


* observaciones: Anotaciones, fallas detectadas o comentarios del auditor.





---

## Relaciones del Modelo

1. Producto ↔ Detalle BOM producto ↔ Componente (Relación N:M):


* Un producto requiere múltiples componentes para su fabricación y un componente puede formar parte de la estructura de múltiples productos. Esta lista de materiales se consolida a través de la entidad asociativa `Detalle BOM producto`.




2. Componente ↔ Composición (Relación Recursiva / Subensambles):


* Los componentes pueden estructurarse jerárquicamente o combinarse en subcomponentes mediante la relación de `Composición`.




3. Producto ↔ Orden de Fabricación (Relación 1:N):


* Un producto puede ser objeto de múltiples órdenes de fabricación en distintos momentos, pero cada orden se emite para la producción de un producto determinado.




4. Linea de montaje ↔ Orden de Fabricación (Relación 1:N):


* Una línea de montaje ejecuta y procesa múltiples órdenes de fabricación a lo largo del tiempo, pero cada orden de fabricación es asignada a una línea de montaje específica.




5. Empleado ↔ Linea de montaje / Orden de Fabricación (Relación 1:N / N:1):


* Un empleado puede intervenir o estar asignado al funcionamiento de líneas de montaje y en la supervisión/operación de las órdenes de fabricación.




6. Producto ↔ Inspección de calidad / Unidad (Relación 1:N):


* Un producto da origen a múltiples unidades físicas o lotes producidos e inspeccionados.




7. Unidad ↔ Inspección de calidad (Relación 1:N / 1:1):


* Las unidades físicas finalizadas son sometidas al proceso de `Inspección de calidad` para verificar el cumplimiento de especificaciones y estándares antes de su liberación.
