# Taller Automotriz Automatizado

Sistema de gestión para un taller automotriz automatizado: citas en línea, órdenes de trabajo, diagnóstico con escáner OBD-II/IoT, inventario de repuestos, facturación con pago en línea y notificaciones al cliente.

Este repositorio contiene la documentación de análisis y diseño del proyecto.

## Contenido

| Carpeta / archivo | Qué contiene |
| --- | --- |
| [docs/01-requerimientos-funcionales.md](docs/01-requerimientos-funcionales.md) | 34 requerimientos funcionales en 7 módulos y la matriz de trazabilidad con las historias de usuario |
| [docs/02-requerimientos-no-funcionales.md](docs/02-requerimientos-no-funcionales.md) | 18 requerimientos no funcionales según ISO/IEC 25010, cada uno con criterio medible |
| [docs/03-historias-de-usuario.md](docs/03-historias-de-usuario.md) | 30 historias de usuario en 7 épicas con criterios de aceptación, prioridad MoSCoW, puntos, plan de sprints y Definición de Terminado |
| [diagramas/](diagramas/) | Diagramas del modelo de vistas 4+1 en Visual Paradigm (`.vpp`), un archivo por diagrama |

## Diagramas (modelo 4+1)

| # | Vista | Tipo de diagrama | Qué muestra |
| --- | --- | --- | --- |
| 1 | Vista de contexto | Diagrama de flujo de datos (nivel 0) | El sistema y sus 6 entidades externas: cliente, mecánico, administrador, proveedor, pasarela de pagos y equipos OBD-II/IoT |
| 2 | Vista funcional | Diagrama de componentes | Portal web, app del técnico, panel administrativo, API Gateway y servicios de citas, órdenes, diagnóstico, inventario, facturación, notificaciones e integración OBD-II |
| 3 | Vista lógica | Diagrama de clases (dominio) | Persona, Cliente, Empleado, Mecánico, Recepcionista, Vehículo, Cita, OrdenTrabajo, Diagnóstico, Servicio, Repuesto, Factura, Pago y Proveedor |
| 4 | Vista de desarrollo | Diagrama de clases (implementación) | Paquetes presentación, aplicación, persistencia e integración, con controladores, servicios, repositorios y adaptadores |
| 5 | Vista de despliegue | Diagrama de despliegue | Dispositivos del cliente y del técnico, servidor de aplicaciones con Docker, servidor PostgreSQL, gateway IoT, escáner OBD-II y servicios externos |

### Qué versión de Visual Paradigm usar

Cada diagrama está en dos versiones, porque Visual Paradigm 18.1 convierte los archivos de 17.3 al abrirlos y después la 17.3 ya no los puede leer:

- `diagramas/VP 17.3/` → abrir con **Visual Paradigm 17.3**
- `diagramas/VP 18.1/` → abrir con **Visual Paradigm 18.1**

No abras los archivos de la carpeta 17.3 con la 18.1, para no convertirlos.
