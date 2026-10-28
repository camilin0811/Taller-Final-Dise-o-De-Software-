# Requerimientos funcionales

El sistema tiene 34 requerimientos funcionales en 7 módulos; cada uno indica qué debe hacer el sistema y de qué historia de usuario sale. La prioridad usa la misma escala MoSCoW de las historias.

## M1. Usuarios, clientes y vehículos

| ID | El sistema debe… | Prioridad | HU |
| --- | --- | --- | --- |
| RF-01 | Permitir el registro de clientes con nombre, documento, teléfono, correo y contraseña, validando que el correo y el documento no estén repetidos | Must | HU-01 |
| RF-02 | Autenticar a los usuarios con correo y contraseña | Must | HU-02 |
| RF-03 | Restringir las funciones según el rol del usuario: cliente, recepcionista, mecánico o administrador | Must | HU-02, HU-05 |
| RF-04 | Bloquear la cuenta durante 15 minutos después de 5 intentos fallidos de inicio de sesión | Must | HU-02 |
| RF-05 | Permitir al administrador crear, editar y desactivar empleados y asignarles un rol | Must | HU-05 |
| RF-06 | Permitir al cliente registrar vehículos con placa, marca, modelo, año, kilometraje y VIN, sin placas repetidas | Must | HU-03 |
| RF-07 | Mostrar el historial de órdenes de un vehículo, de la más reciente a la más antigua | Should | HU-04 |

## M2. Citas

| ID | El sistema debe… | Prioridad | HU |
| --- | --- | --- | --- |
| RF-08 | Mostrar un calendario con los bloques de 1 hora disponibles según la capacidad de mecánicos y bahías | Must | HU-07 |
| RF-09 | Permitir agendar una cita indicando vehículo, servicio, fecha, hora y descripción del problema | Must | HU-06 |
| RF-10 | Permitir reprogramar o cancelar una cita hasta 2 horas antes de su inicio | Should | HU-08 |
| RF-11 | Enviar un recordatorio automático 24 horas antes de cada cita confirmada | Should | HU-09 |
| RF-12 | Mostrar al recepcionista la agenda del día y permitirle confirmar citas y registrar clientes sin cita | Must | HU-10 |

## M3. Órdenes de trabajo

| ID | El sistema debe… | Prioridad | HU |
| --- | --- | --- | --- |
| RF-13 | Crear órdenes de trabajo con número consecutivo y registrar el estado de ingreso del vehículo (kilometraje, combustible, daños y fotos) | Must | HU-11 |
| RF-14 | Permitir asignar la orden a un mecánico mostrando su especialidad y su carga de órdenes activas | Must | HU-12 |
| RF-15 | Mostrar al mecánico, en la app de tablet, sus órdenes activas ordenadas por fecha de ingreso | Must | HU-13 |
| RF-16 | Controlar el flujo de estados de la orden (Recibida → En diagnóstico → Esperando aprobación → En reparación → Lista para entrega → Entregada) y guardar cada cambio con fecha, hora y usuario | Must | HU-14 |
| RF-17 | Permitir registrar los repuestos usados en una orden y validar que haya stock | Must | HU-15 |
| RF-18 | Permitir al cliente consultar en línea el estado, la línea de tiempo y la fecha estimada de entrega de su orden | Should | HU-16 |

## M4. Diagnóstico automatizado

| ID | El sistema debe… | Prioridad | HU |
| --- | --- | --- | --- |
| RF-19 | Leer los códigos de falla del escáner OBD-II a través del gateway IoT y guardarlos en el diagnóstico de la orden | Must | HU-17 |
| RF-20 | Permitir registrar códigos de falla manualmente cuando el escáner no responda | Must | HU-17 |
| RF-21 | Traducir cada código de falla a su descripción, sistema afectado y gravedad, usando un catálogo de códigos | Must | HU-18 |
| RF-22 | Sugerir servicios y repuestos según los códigos detectados | Must | HU-18 |
| RF-23 | Generar un reporte de diagnóstico en PDF para el cliente | Should | HU-19 |
| RF-24 | Mostrar en tiempo real las lecturas de los sensores y resaltar los valores fuera de rango | Could | HU-20 |

## M5. Inventario y proveedores

| ID | El sistema debe… | Prioridad | HU |
| --- | --- | --- | --- |
| RF-25 | Permitir crear, editar y ajustar repuestos con código único, precio, stock, stock mínimo y proveedor, guardando el motivo de cada ajuste | Must | HU-21 |
| RF-26 | Descontar el stock al registrar un repuesto en una orden y devolverlo si se retira antes de cerrarla | Must | HU-22 |
| RF-27 | Alertar al administrador cuando un repuesto llegue a su stock mínimo | Should | HU-23 |
| RF-28 | Generar pedidos por proveedor, enviarlos por correo y registrar la recepción de la mercancía | Should | HU-24 |

## M6. Cotización, facturación y pagos

| ID | El sistema debe… | Prioridad | HU |
| --- | --- | --- | --- |
| RF-29 | Generar cotizaciones con servicios, repuestos, subtotal, IVA del 19 % y total | Must | HU-25 |
| RF-30 | Permitir al cliente aprobar la cotización completa, aprobar solo algunos ítems o rechazarla | Must | HU-26 |
| RF-31 | Emitir facturas con número consecutivo, enviarlas en PDF y permitir anularlas solo con nota crédito | Must | HU-27 |
| RF-32 | Recibir pagos en línea a través de la pasarela de pagos y registrar pagos en efectivo | Should | HU-28 |

## M7. Notificaciones y reportes

| ID | El sistema debe… | Prioridad | HU |
| --- | --- | --- | --- |
| RF-33 | Notificar los cambios de estado por correo, SMS o WhatsApp según la preferencia del cliente, con hasta 3 reintentos | Should | HU-29 |
| RF-34 | Generar reportes de ingresos, órdenes, tiempos de reparación, servicios y productividad por mecánico, exportables a Excel y PDF | Should | HU-30 |

## Matriz de trazabilidad

Las 30 historias de usuario quedan cubiertas por al menos un requerimiento funcional, y los 34 requerimientos funcionales salen de alguna historia.

| Historia | Requerimientos funcionales | Módulo |
| --- | --- | --- |
| HU-01 Registrarse como cliente | RF-01 | M1 |
| HU-02 Iniciar sesión según mi rol | RF-02, RF-03, RF-04 | M1 |
| HU-03 Registrar mis vehículos | RF-06 | M1 |
| HU-04 Consultar el historial de un vehículo | RF-07 | M1 |
| HU-05 Administrar usuarios y roles | RF-03, RF-05 | M1 |
| HU-06 Agendar una cita en línea | RF-09 | M2 |
| HU-07 Ver la disponibilidad del taller | RF-08 | M2 |
| HU-08 Reprogramar o cancelar una cita | RF-10 | M2 |
| HU-09 Recibir recordatorio de la cita | RF-11 | M2 |
| HU-10 Gestionar la agenda diaria | RF-12 | M2 |
| HU-11 Crear la orden de trabajo | RF-13 | M3 |
| HU-12 Asignar un mecánico a la orden | RF-14 | M3 |
| HU-13 Ver mis órdenes asignadas | RF-15 | M3 |
| HU-14 Registrar el avance de la reparación | RF-16 | M3 |
| HU-15 Registrar los repuestos usados | RF-17 | M3 |
| HU-16 Seguir el estado de mi vehículo | RF-18 | M3 |
| HU-17 Ejecutar el escaneo OBD-II | RF-19, RF-20 | M4 |
| HU-18 Interpretar los códigos de falla | RF-21, RF-22 | M4 |
| HU-19 Recibir el reporte de diagnóstico | RF-23 | M4 |
| HU-20 Monitorear sensores en tiempo real | RF-24 | M4 |
| HU-21 Gestionar el catálogo de repuestos | RF-25 | M5 |
| HU-22 Descontar el stock automáticamente | RF-26 | M5 |
| HU-23 Recibir alertas de stock mínimo | RF-27 | M5 |
| HU-24 Hacer pedidos a proveedores | RF-28 | M5 |
| HU-25 Generar la cotización | RF-29 | M6 |
| HU-26 Aprobar o rechazar la cotización | RF-30 | M6 |
| HU-27 Emitir la factura | RF-31 | M6 |
| HU-28 Pagar en línea | RF-32 | M6 |
| HU-29 Notificar los cambios de estado | RF-33 | M7 |
| HU-30 Consultar reportes | RF-34 | M7 |
