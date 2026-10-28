# Requerimientos no funcionales

El sistema tiene 18 requerimientos no funcionales, organizados con las características de calidad de la norma ISO/IEC 25010. Cada uno tiene un criterio medible para poder verificarlo en las pruebas.

| ID | Categoría (ISO/IEC 25010) | Requerimiento | Criterio de aceptación | Prioridad |
| --- | --- | --- | --- | --- |
| RNF-01 | Eficiencia de desempeño | Las operaciones comunes (consultar, agendar, cambiar estado) deben responder rápido | 95 % de las respuestas en menos de 2 s con 50 usuarios simultáneos | Must |
| RNF-02 | Eficiencia de desempeño | La lectura del escáner OBD-II debe ser ágil | Escaneo completo en menos de 60 s; datos en vivo actualizados cada 1 s | Must |
| RNF-03 | Fiabilidad (disponibilidad) | El sistema debe estar disponible en el horario del taller | 99 % de disponibilidad de lunes a sábado, de 7:00 a 19:00 | Must |
| RNF-04 | Fiabilidad (recuperación) | La base de datos debe poder recuperarse ante fallos | Copia de seguridad diaria, guardada 30 días; pérdida máxima de 24 h de datos y restauración en menos de 4 h | Must |
| RNF-05 | Fiabilidad (tolerancia a fallos) | Las integraciones externas no deben perder mensajes | Notificaciones con hasta 3 reintentos; mensajes MQTT del gateway IoT con QoS 1 | Should |
| RNF-06 | Seguridad (confidencialidad) | Las comunicaciones deben ir cifradas | Todo el tráfico por HTTPS con TLS 1.2 o superior | Must |
| RNF-07 | Seguridad (autenticidad) | Las contraseñas y sesiones deben estar protegidas | Contraseñas guardadas con hash bcrypt; tokens JWT que vencen a las 8 h | Must |
| RNF-08 | Seguridad (control de acceso) | Los permisos por rol deben validarse en el servidor | Ninguna API devuelve datos de otro rol o de otro cliente, aunque se manipule la petición | Must |
| RNF-09 | Seguridad (pagos) | El sistema no debe guardar datos de tarjetas | Los pagos pasan solo por la pasarela certificada PCI DSS; la base de datos no tiene números de tarjeta | Must |
| RNF-10 | Seguridad (trazabilidad) | Los cambios importantes deben quedar auditados | Registro de usuario, fecha, hora y acción en órdenes, inventario y facturas | Must |
| RNF-11 | Usabilidad | El portal del cliente debe ser fácil de usar | Un cliente nuevo agenda una cita en menos de 3 minutos y en máximo 5 pasos | Should |
| RNF-12 | Usabilidad (adaptabilidad) | Las interfaces deben funcionar en varios dispositivos | Portal adaptable desde 360 px de ancho; app del técnico en tablets Android 10 o superior | Must |
| RNF-13 | Usabilidad (idioma) | La interfaz debe estar en el idioma y formato local | Textos en español, moneda en pesos colombianos (COP) y fechas en formato dd/mm/aaaa | Must |
| RNF-14 | Compatibilidad | El sistema debe funcionar con los navegadores y equipos del taller | Chrome, Edge y Firefox (últimas 2 versiones); escáneres OBD-II compatibles con ELM327 | Must |
| RNF-15 | Mantenibilidad | El código debe ser fácil de mantener y probar | Arquitectura en capas (presentación, aplicación, persistencia, integración) y cobertura de pruebas de al menos 70 % | Should |
| RNF-16 | Portabilidad | El sistema debe poder desplegarse en cualquier servidor | Servicios empaquetados en contenedores Docker sobre Linux | Should |
| RNF-17 | Escalabilidad | El sistema debe crecer sin rediseñarse | Soporta hasta 3 sedes y 10.000 órdenes por año con la misma arquitectura | Could |
| RNF-18 | Legal | El sistema debe cumplir la normativa colombiana | Tratamiento de datos personales según la Ley 1581 de 2012 (Habeas Data), con autorización del cliente al registrarse; facturación alineada con la factura electrónica de la DIAN | Must |

Los RNF-06 a RNF-10 dependen de la vista de despliegue (HTTPS entre clientes y servidor, pasarela de pagos externa), y los RNF-15 y RNF-16 dependen de la vista de desarrollo (paquetes por capas y contenedores Docker).
