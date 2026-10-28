# Historias de usuario

## Introducción

El backlog tiene 30 historias de usuario en 7 épicas y cubre el sistema de gestión del taller automotriz automatizado: citas, órdenes de trabajo, diagnóstico OBD-II, inventario, facturación y notificaciones. Las historias corresponden a los diagramas de las 4+1 vistas del proyecto (contexto, componentes, clases y despliegue).

**Roles del sistema**

| Rol | Quién es | Qué hace en el sistema |
| --- | --- | --- |
| Cliente | Dueño del vehículo | Se registra, agenda citas, aprueba cotizaciones, paga y sigue el estado de su vehículo |
| Recepcionista | Empleado de recepción | Recibe vehículos, crea órdenes de trabajo, asigna mecánicos y emite facturas |
| Mecánico | Técnico del taller | Ejecuta diagnósticos, registra avances y repuestos usados |
| Administrador | Dueño o gerente | Gestiona usuarios, tarifas, inventario, proveedores y reportes |
| Sistema | Procesos automáticos | Envía notificaciones, lee el escáner OBD-II y genera alertas |

**Formato de cada historia**

- **Enunciado:** Como *[rol]*, quiero *[acción]*, para *[beneficio]*.
- **Criterios de aceptación:** escenarios en formato Dado / Cuando / Entonces.
- **Prioridad (MoSCoW):** Must (obligatoria), Should (importante), Could (deseable), Won't (fuera de esta versión).
- **Estimación:** puntos de historia en escala Fibonacci (1, 2, 3, 5, 8, 13).

## Épica 1: Gestión de clientes y vehículos

Esta épica da a cada persona una cuenta con su rol y deja registrados los vehículos con su historial. Tiene 5 historias y suma 18 puntos.

### HU-01 Registrarse como cliente

Como **cliente**, quiero crear una cuenta con mis datos personales, para agendar citas y seguir mis vehículos en línea.

- Dado que no tengo cuenta, cuando ingreso nombre, documento, teléfono, correo y contraseña válidos, entonces el sistema crea mi cuenta y me envía un correo de confirmación.
- Dado que el correo o el documento ya están registrados, cuando envío el formulario, entonces el sistema muestra "El usuario ya existe" y no crea otra cuenta.
- Dado que la contraseña tiene menos de 8 caracteres, cuando envío el formulario, entonces el sistema la rechaza e indica el requisito.

Prioridad: Must · Estimación: 3 puntos

### HU-02 Iniciar sesión según mi rol

Como **usuario del sistema**, quiero iniciar sesión con correo y contraseña, para acceder solo a las funciones de mi rol.

- Dado un usuario registrado, cuando ingresa credenciales correctas, entonces entra a su panel (cliente, recepcionista, mecánico o administrador).
- Dado que las credenciales son incorrectas, cuando intenta entrar, entonces el sistema muestra un mensaje genérico sin indicar cuál dato falló.
- Dado que falla 5 veces seguidas, cuando intenta de nuevo, entonces la cuenta se bloquea 15 minutos.

Prioridad: Must · Estimación: 3 puntos

### HU-03 Registrar mis vehículos

Como **cliente**, quiero registrar uno o varios vehículos, para no repetir sus datos en cada cita.

- Dado que inicié sesión, cuando ingreso placa, marca, modelo, año, kilometraje y VIN, entonces el vehículo queda asociado a mi cuenta.
- Dado que la placa ya existe en el sistema, cuando intento registrarla, entonces el sistema lo rechaza y sugiere contactar al taller.

Prioridad: Must · Estimación: 2 puntos

### HU-04 Consultar el historial de un vehículo

Como **cliente** o **mecánico**, quiero ver el historial de servicios de un vehículo, para conocer reparaciones y diagnósticos anteriores.

- Dado un vehículo con órdenes cerradas, cuando abro su historial, entonces veo fecha, servicios, repuestos, kilometraje y total de cada orden, del más reciente al más antiguo.
- Dado que soy cliente, cuando consulto el historial, entonces solo veo mis propios vehículos.

Prioridad: Should · Estimación: 5 puntos

### HU-05 Administrar usuarios y roles

Como **administrador**, quiero crear, editar y desactivar cuentas de empleados con su rol, para controlar quién accede a cada función.

- Dado que soy administrador, cuando creo un empleado con rol "Mecánico", entonces ese usuario solo ve las funciones de mecánico.
- Dado un empleado que se retiró, cuando lo desactivo, entonces ya no puede iniciar sesión y su historial de trabajo se conserva.

Prioridad: Must · Estimación: 5 puntos

## Épica 2: Agendamiento de citas

Esta épica permite al cliente reservar un turno sin llamar y le da al taller una agenda ordenada. Tiene 5 historias y suma 17 puntos.

### HU-06 Agendar una cita en línea

Como **cliente**, quiero agendar una cita eligiendo vehículo, servicio, fecha y hora, para no tener que llamar al taller.

- Dado que tengo un vehículo registrado, cuando elijo un servicio y un horario libre, entonces la cita queda en estado "Pendiente" y recibo una confirmación por correo.
- Dado que el horario se ocupó mientras lo elegía, cuando confirmo, entonces el sistema me avisa y me muestra los horarios libres más cercanos.
- Dado que describo el problema en un campo de texto, cuando se crea la cita, entonces la descripción queda visible para el recepcionista.

Prioridad: Must · Estimación: 5 puntos

### HU-07 Ver la disponibilidad del taller

Como **cliente**, quiero ver un calendario con los horarios libres, para escoger el que me convenga.

- Dado un día laboral, cuando abro el calendario, entonces veo los bloques de 1 hora libres según la capacidad de mecánicos y bahías.
- Dado un domingo o festivo, cuando lo selecciono, entonces aparece como no disponible.

Prioridad: Must · Estimación: 3 puntos

### HU-08 Reprogramar o cancelar una cita

Como **cliente**, quiero reprogramar o cancelar mi cita, para ajustarla si cambian mis planes.

- Dado que faltan más de 2 horas, cuando cancelo, entonces el horario se libera y la cita pasa a "Cancelada".
- Dado que faltan menos de 2 horas, cuando intento cancelar, entonces el sistema me pide llamar al taller.
- Dado que reprogramo, cuando elijo un nuevo horario libre, entonces se conserva la misma cita con la nueva fecha.

Prioridad: Should · Estimación: 3 puntos

### HU-09 Recibir recordatorio de la cita

Como **cliente**, quiero recibir un recordatorio antes de mi cita, para no olvidarla.

- Dada una cita confirmada, cuando faltan 24 horas, entonces el sistema envía un recordatorio por correo y WhatsApp o SMS.
- Dado que la cita fue cancelada, cuando llega la hora del recordatorio, entonces no se envía nada.

Prioridad: Should · Estimación: 3 puntos

### HU-10 Gestionar la agenda diaria

Como **recepcionista**, quiero ver y confirmar las citas del día, para preparar la recepción de los vehículos.

- Dado el inicio de la jornada, cuando abro la agenda, entonces veo las citas del día ordenadas por hora con cliente, vehículo y servicio.
- Dada una cita pendiente, cuando la confirmo, entonces pasa a "Confirmada" y se notifica al cliente.
- Dado un cliente que llega sin cita, cuando hay cupo, entonces puedo registrar la cita en el momento.

Prioridad: Must · Estimación: 3 puntos

## Épica 3: Recepción y órdenes de trabajo

Esta épica es el núcleo del taller: la orden de trabajo sigue al vehículo desde que entra hasta que se entrega. Tiene 6 historias y suma 22 puntos. Los estados de una orden son: Recibida → En diagnóstico → Esperando aprobación → En reparación → Lista para entrega → Entregada.

### HU-11 Crear la orden de trabajo al recibir el vehículo

Como **recepcionista**, quiero crear una orden de trabajo cuando llega el vehículo, para registrar formalmente su ingreso.

- Dada una cita confirmada, cuando el vehículo llega, entonces creo la orden con los datos de la cita precargados y el sistema le asigna un número consecutivo.
- Dado el ingreso, cuando registro kilometraje, nivel de combustible, daños visibles y fotos, entonces quedan guardados en la orden.
- Dada la orden creada, cuando se guarda, entonces queda en estado "Recibida" y el cliente recibe la notificación.

Prioridad: Must · Estimación: 5 puntos

### HU-12 Asignar un mecánico a la orden

Como **recepcionista**, quiero asignar la orden a un mecánico disponible, para repartir la carga de trabajo.

- Dada una orden "Recibida", cuando abro la asignación, entonces veo los mecánicos disponibles con su especialidad y número de órdenes activas.
- Dado que asigno un mecánico, cuando confirmo, entonces la orden aparece en su lista de trabajo.

Prioridad: Must · Estimación: 3 puntos

### HU-13 Ver mis órdenes asignadas

Como **mecánico**, quiero ver en la tablet las órdenes que tengo asignadas, para saber qué vehículo atender primero.

- Dado que inicio sesión en la app del técnico, cuando abro "Mis órdenes", entonces veo mis órdenes activas ordenadas por fecha de ingreso, con placa, servicio y estado.
- Dada una orden, cuando la abro, entonces veo la descripción del problema, las fotos de ingreso y el historial del vehículo.

Prioridad: Must · Estimación: 3 puntos

### HU-14 Registrar el avance de la reparación

Como **mecánico**, quiero registrar el avance y cambiar el estado de la orden, para que el taller y el cliente sepan cómo va.

- Dada una orden asignada, cuando cambio su estado, entonces el sistema guarda la fecha, la hora y mi usuario.
- Dado que agrego una nota de avance o una foto, cuando la guardo, entonces queda en la bitácora de la orden.
- Dada una orden "Esperando aprobación", cuando intento pasarla a "En reparación", entonces el sistema lo impide hasta que el cliente apruebe la cotización.

Prioridad: Must · Estimación: 5 puntos

### HU-15 Registrar los repuestos usados

Como **mecánico**, quiero registrar los repuestos que uso en la orden, para que se cobren y se descuenten del inventario.

- Dada una orden "En reparación", cuando busco un repuesto por código o nombre y digito la cantidad, entonces se agrega a la orden con su precio.
- Dado que no hay stock suficiente, cuando intento agregarlo, entonces el sistema avisa y notifica al administrador.

Prioridad: Must · Estimación: 3 puntos

### HU-16 Seguir el estado de mi vehículo

Como **cliente**, quiero consultar en línea el estado de mi vehículo, para no tener que llamar a preguntar.

- Dado que tengo una orden activa, cuando entro al portal, entonces veo el estado actual, la línea de tiempo de cambios y la fecha estimada de entrega.
- Dado que el mecánico subió fotos de avance, cuando abro la orden, entonces puedo verlas.

Prioridad: Should · Estimación: 3 puntos

## Épica 4: Diagnóstico automatizado (OBD-II / IoT)

Esta épica es lo que hace al taller "automatizado": el escáner OBD-II envía los códigos de falla al sistema a través del gateway IoT. Tiene 4 historias y suma 24 puntos.

### HU-17 Ejecutar el escaneo OBD-II desde la tablet

Como **mecánico**, quiero lanzar un escaneo OBD-II desde la app, para leer los códigos de falla sin pasarlos a mano.

- Dado que el escáner está conectado al vehículo y enlazado por Bluetooth al gateway IoT, cuando pulso "Escanear", entonces en menos de 60 segundos el sistema guarda los códigos de falla en el diagnóstico de la orden.
- Dado que el escáner no responde, cuando pasan 60 segundos, entonces la app muestra "Escáner sin conexión" y permite reintentar o registrar los códigos a mano.
- Dado un escaneo exitoso, cuando termina, entonces la orden pasa a "En diagnóstico".

Prioridad: Must · Estimación: 8 puntos

### HU-18 Interpretar los códigos de falla

Como **mecánico**, quiero ver la descripción y la gravedad de cada código, para decidir rápido la reparación.

- Dado un código como P0301, cuando se muestra el resultado, entonces aparece su descripción ("Falla de encendido en cilindro 1"), el sistema afectado y la gravedad (alta, media o baja).
- Dado un código que no está en la base de datos, cuando se muestra, entonces aparece como "Código desconocido" para revisión manual.
- Dados los códigos detectados, cuando reviso el resultado, entonces el sistema sugiere los servicios y repuestos asociados para la cotización.

Prioridad: Must · Estimación: 5 puntos

### HU-19 Recibir el reporte de diagnóstico

Como **cliente**, quiero recibir un reporte claro del diagnóstico, para entender qué tiene mi vehículo antes de aprobar la reparación.

- Dado un diagnóstico terminado, cuando el mecánico lo publica, entonces recibo un reporte en PDF con las fallas explicadas en lenguaje sencillo y su gravedad.
- Dado el reporte, cuando lo abro desde el portal, entonces veo también la cotización asociada.

Prioridad: Should · Estimación: 3 puntos

### HU-20 Monitorear sensores en tiempo real

Como **mecánico**, quiero ver en vivo las lecturas de los sensores (RPM, temperatura, voltaje), para encontrar fallas intermitentes.

- Dado un vehículo conectado, cuando abro "Datos en vivo", entonces veo las lecturas actualizadas cada segundo en gráficas.
- Dada una lectura fuera de rango, cuando ocurre, entonces el valor se resalta en rojo.
- Dada una sesión de monitoreo, cuando la detengo, entonces puedo guardarla en el diagnóstico de la orden.

Prioridad: Could · Estimación: 8 puntos

## Épica 5: Inventario de repuestos y proveedores

Esta épica evita que una reparación se detenga por falta de repuestos: el stock se descuenta solo y avisa cuando hay que pedir. Tiene 4 historias y suma 14 puntos.

### HU-21 Gestionar el catálogo de repuestos

Como **administrador**, quiero crear y editar repuestos con su código, precio, stock y stock mínimo, para tener el inventario al día.

- Dado un repuesto nuevo, cuando ingreso código, nombre, precio de venta, stock inicial, stock mínimo y proveedor, entonces queda disponible para las órdenes.
- Dado un código que ya existe, cuando intento crearlo, entonces el sistema lo rechaza.
- Dado que ajusto el stock a mano, cuando guardo, entonces el sistema registra el motivo y el usuario que hizo el ajuste.

Prioridad: Must · Estimación: 3 puntos

### HU-22 Descontar el stock automáticamente

Como **administrador**, quiero que el stock se descuente al registrar repuestos en una orden, para no actualizar el inventario a mano.

- Dado un repuesto con stock 10, cuando un mecánico registra 2 unidades en una orden, entonces el stock queda en 8.
- Dado que el repuesto se retira de la orden antes de cerrarla, cuando se elimina, entonces las unidades vuelven al stock.

Prioridad: Must · Estimación: 3 puntos

### HU-23 Recibir alertas de stock mínimo

Como **administrador**, quiero recibir una alerta cuando un repuesto llega a su stock mínimo, para pedirlo a tiempo.

- Dado un repuesto con stock mínimo 5, cuando su stock baja a 5 o menos, entonces recibo una alerta en el panel y por correo.
- Dado el panel de inventario, cuando lo abro, entonces los repuestos bajo el mínimo aparecen primero y resaltados.

Prioridad: Should · Estimación: 3 puntos

### HU-24 Hacer pedidos a proveedores

Como **administrador**, quiero generar un pedido de repuestos al proveedor, para reponer el stock.

- Dados los repuestos bajo el mínimo, cuando pulso "Generar pedido", entonces el sistema arma un pedido por proveedor con las cantidades sugeridas, que puedo editar.
- Dado un pedido confirmado, cuando lo envío, entonces el proveedor lo recibe por correo y el pedido queda "Enviado".
- Dado que llega la mercancía, cuando registro la recepción con la factura de compra, entonces el stock aumenta y el pedido queda "Recibido".

Prioridad: Should · Estimación: 5 puntos

## Épica 6: Cotización, facturación y pagos

Esta épica asegura que el cliente apruebe el costo antes de la reparación y pueda pagar sin hacer fila. Tiene 4 historias y suma 21 puntos.

### HU-25 Generar la cotización

Como **recepcionista**, quiero generar una cotización a partir del diagnóstico, para informar al cliente el costo antes de reparar.

- Dado un diagnóstico terminado, cuando genero la cotización, entonces incluye los servicios (mano de obra según tarifa) y los repuestos sugeridos con sus precios.
- Dada la cotización, cuando se calcula, entonces muestra subtotal, IVA (19 %) y total.
- Dada la cotización lista, cuando la envío, entonces la orden pasa a "Esperando aprobación" y el cliente recibe la notificación.

Prioridad: Must · Estimación: 5 puntos

### HU-26 Aprobar o rechazar la cotización

Como **cliente**, quiero aprobar o rechazar la cotización desde el portal, para autorizar la reparación sin ir al taller.

- Dada una cotización pendiente, cuando la apruebo, entonces la orden pasa a "En reparación" y se notifica al mecánico.
- Dado que apruebo solo algunos ítems, cuando confirmo, entonces el total se recalcula y solo se hacen esos trabajos.
- Dado que la rechazo, cuando confirmo, entonces la orden pasa a "Lista para entrega" y solo se cobra el diagnóstico.

Prioridad: Must · Estimación: 3 puntos

### HU-27 Emitir la factura

Como **recepcionista**, quiero emitir la factura al terminar la orden, para cobrar el servicio.

- Dada una orden "Lista para entrega", cuando genero la factura, entonces incluye los servicios y repuestos realmente usados, subtotal, IVA y total, con número consecutivo.
- Dada la factura emitida, cuando se guarda, entonces el cliente la recibe en PDF por correo y la puede descargar del portal.
- Dada una factura emitida, cuando alguien intenta editarla, entonces el sistema solo permite anularla con una nota crédito.

Prioridad: Must · Estimación: 5 puntos

### HU-28 Pagar en línea

Como **cliente**, quiero pagar la factura en línea con tarjeta o PSE, para retirar mi vehículo sin hacer fila.

- Dada una factura pendiente, cuando pago a través de la pasarela de pagos, entonces el sistema recibe la confirmación y la factura queda "Pagada".
- Dado que la pasarela rechaza el pago, cuando vuelvo al portal, entonces veo el motivo y puedo intentar con otro medio.
- Dado un pago en efectivo en el taller, cuando el recepcionista lo registra, entonces la factura también queda "Pagada".

Prioridad: Should · Estimación: 8 puntos

## Épica 7: Notificaciones y reportes

Esta épica mantiene informado al cliente sin esfuerzo del personal y le da al administrador los números para decidir. Tiene 2 historias y suma 8 puntos.

### HU-29 Notificar los cambios de estado

Como **cliente**, quiero recibir un aviso cada vez que mi vehículo cambia de estado, para saber cuándo debo actuar o recogerlo.

- Dada una orden activa, cuando cambia a "Esperando aprobación" o "Lista para entrega", entonces recibo un mensaje por el canal que elegí (correo, SMS o WhatsApp).
- Dado que desactivé las notificaciones de un canal, cuando ocurre un cambio, entonces no recibo mensajes por ese canal.
- Dado un envío que falla, cuando el servicio externo responde con error, entonces el sistema reintenta hasta 3 veces y registra el fallo.

Prioridad: Should · Estimación: 3 puntos

### HU-30 Consultar reportes operativos y financieros

Como **administrador**, quiero ver reportes del taller por rango de fechas, para tomar decisiones con datos.

- Dado un rango de fechas, cuando abro los reportes, entonces veo: ingresos totales, órdenes atendidas, tiempo promedio de reparación, servicios más solicitados y productividad por mecánico.
- Dado un reporte en pantalla, cuando pulso "Exportar", entonces se descarga en Excel o PDF.
- Dado que soy recepcionista o mecánico, cuando intento abrir los reportes financieros, entonces el sistema me niega el acceso.

Prioridad: Should · Estimación: 5 puntos

## Resumen del backlog

El backlog suma 124 puntos: 19 historias Must (75 pts), 10 Should (41 pts) y 1 Could (8 pts). Con una velocidad estimada de unos 22 puntos por sprint de 2 semanas, salen 6 sprints, y el producto mínimo viable (todas las Must) queda listo al cerrar el sprint 4.

| ID | Historia | Rol | Épica | Prioridad | Puntos | Sprint |
| --- | --- | --- | --- | --- | --- | --- |
| HU-01 | Registrarse como cliente | Cliente | 1 | Must | 3 | 1 |
| HU-02 | Iniciar sesión según mi rol | Todos | 1 | Must | 3 | 1 |
| HU-03 | Registrar mis vehículos | Cliente | 1 | Must | 2 | 1 |
| HU-04 | Consultar el historial de un vehículo | Cliente / Mecánico | 1 | Should | 5 | 4 |
| HU-05 | Administrar usuarios y roles | Administrador | 1 | Must | 5 | 1 |
| HU-06 | Agendar una cita en línea | Cliente | 2 | Must | 5 | 1 |
| HU-07 | Ver la disponibilidad del taller | Cliente | 2 | Must | 3 | 1 |
| HU-08 | Reprogramar o cancelar una cita | Cliente | 2 | Should | 3 | 4 |
| HU-09 | Recibir recordatorio de la cita | Cliente | 2 | Should | 3 | 4 |
| HU-10 | Gestionar la agenda diaria | Recepcionista | 2 | Must | 3 | 2 |
| HU-11 | Crear la orden de trabajo | Recepcionista | 3 | Must | 5 | 2 |
| HU-12 | Asignar un mecánico a la orden | Recepcionista | 3 | Must | 3 | 2 |
| HU-13 | Ver mis órdenes asignadas | Mecánico | 3 | Must | 3 | 2 |
| HU-14 | Registrar el avance de la reparación | Mecánico | 3 | Must | 5 | 2 |
| HU-15 | Registrar los repuestos usados | Mecánico | 3 | Must | 3 | 2 |
| HU-16 | Seguir el estado de mi vehículo | Cliente | 3 | Should | 3 | 4 |
| HU-17 | Ejecutar el escaneo OBD-II | Mecánico | 4 | Must | 8 | 3 |
| HU-18 | Interpretar los códigos de falla | Mecánico | 4 | Must | 5 | 3 |
| HU-19 | Recibir el reporte de diagnóstico | Cliente | 4 | Should | 3 | 5 |
| HU-20 | Monitorear sensores en tiempo real | Mecánico | 4 | Could | 8 | 6 |
| HU-21 | Gestionar el catálogo de repuestos | Administrador | 5 | Must | 3 | 3 |
| HU-22 | Descontar el stock automáticamente | Administrador | 5 | Must | 3 | 3 |
| HU-23 | Recibir alertas de stock mínimo | Administrador | 5 | Should | 3 | 5 |
| HU-24 | Hacer pedidos a proveedores | Administrador | 5 | Should | 5 | 5 |
| HU-25 | Generar la cotización | Recepcionista | 6 | Must | 5 | 3 |
| HU-26 | Aprobar o rechazar la cotización | Cliente | 6 | Must | 3 | 4 |
| HU-27 | Emitir la factura | Recepcionista | 6 | Must | 5 | 4 |
| HU-28 | Pagar en línea | Cliente | 6 | Should | 8 | 5 |
| HU-29 | Notificar los cambios de estado | Cliente | 7 | Should | 3 | 5 |
| HU-30 | Consultar reportes | Administrador | 7 | Should | 5 | 6 |

**Plan de sprints**

1. **Sprint 1 (21 pts) – Acceso y citas:** HU-01, HU-02, HU-03, HU-05, HU-06, HU-07.
2. **Sprint 2 (22 pts) – Recepción y órdenes:** HU-10, HU-11, HU-12, HU-13, HU-14, HU-15.
3. **Sprint 3 (24 pts) – Diagnóstico, inventario y cotización:** HU-17, HU-18, HU-21, HU-22, HU-25.
4. **Sprint 4 (22 pts) – Cierre del MVP y seguimiento:** HU-26, HU-27, HU-04, HU-16, HU-08, HU-09.
5. **Sprint 5 (22 pts) – Pagos y automatización:** HU-28, HU-19, HU-23, HU-24, HU-29.
6. **Sprint 6 (13 pts) – Valor agregado:** HU-30, HU-20.

**Definición de Terminado (DoD)**

Una historia se considera terminada cuando cumple todo lo siguiente:

- [ ] Cumple todos sus criterios de aceptación.
- [ ] El código está revisado por otro integrante del equipo.
- [ ] Tiene pruebas unitarias y de integración que pasan.
- [ ] Funciona en el ambiente de pruebas (servidor con Docker).
- [ ] Respeta los permisos por rol definidos en HU-02 y HU-05.
- [ ] El Product Owner la aprobó en la revisión del sprint.
