# Unidad 3 — Gestión y operación del centro de cómputo

**Asignatura:** Administración de Centros de Cómputo

**Material base:** las cuatro presentaciones de esta unidad, impartidas por Mgs. José Franco Lamilla.

**Propósito:** comprender cómo coordinar personas, activos, monitoreo y automatización para mantener servicios disponibles, seguros y eficientes.

Esta unidad responde a cuatro preguntas: **¿quién hace el trabajo?, ¿qué recursos administra?, ¿cómo detecta problemas? y ¿qué tareas puede automatizar?** La operación no consiste únicamente en reparar equipos: requiere responsables, procedimientos, registros y comprobación de resultados.

> **Cómo usar la guía:** estudiar los conceptos, seguir los ejemplos de razonamiento y desarrollar las prácticas. Los ejemplos y recomendaciones complementarias se identifican como tales; no son datos nuevos del caso ni instrucciones para intervenir en producción.

## 1. Materiales y ruta de estudio

| Bloque | Archivo de la materia | Diapositivas de referencia |
|---|---|---|
| Personal técnico | [Gestión del Recurso Humano Técnico](<Gestión del Recurso Humano Técnico en el Centro de Cómputo.pptx>) | 4–13: roles; 15–18: asignación; 20–22: evaluación |
| Activos y mantenimiento | [Inventario, Control y Mantenimiento de Hardware y Software](<Inventario, Control y Mantenimiento de Hardware y Software en la Administración de Centros de Cómput.pptx>) | 6–8: herramientas; 10–11: mantenimiento; 13–17: trazabilidad |
| Monitoreo y respuesta | [Monitoreo y Administración de Redes y Servicios](<Monitoreo y Administración de Redes y Servicios en el Centro de Cómputo.pptx>) | 4–7: monitoreo; 9–10: rendimiento; 12–14: fallos y escalamiento |
| Automatización | [Automatización de Procesos Administrativos en TI](<Automatización de Procesos Administrativos en TI.pptx>) | 4–6: algoritmos y scripts; 8–10: integración; 12–15: casos |

**Relación lógica entre los bloques:**

```text
Roles definidos + inventario confiable
                  ↓
Monitoreo de recursos y servicios
                  ↓
Alerta → diagnóstico → acción autorizada → validación
                  ↓
Registro del incidente y actualización del inventario
                  ↓
Mejora del procedimiento y automatización de tareas repetibles
```

Las unidades [1](<../Unidad 1/README.md>) y [2](<../Unidad 2/README.md>) aportan la estructura, las normas y la seguridad. La [unidad 4](<../Unidad 4/README.md>) utiliza la evidencia operativa para proyectar crecimiento, elaborar presupuestos y medir mejoras.

## 2. Gestión del recurso humano técnico

### 2.1. Conceptos y funciones

Un **rol** define responsabilidades y competencias, no necesariamente una persona distinta. En una institución pequeña alguien puede cubrir varios roles, pero deben quedar claros sus límites, las aprobaciones y quién lo reemplaza.

| Rol | Responsabilidad principal | Ejemplo de trabajo |
|---|---|---|
| Director o gerente | Estrategia, proveedores, presupuesto, cumplimiento y capacidad | Aprobar una renovación alineada con las necesidades institucionales |
| Administrador de sistemas, SysAdmin | Sistemas operativos, virtualización, SAN/NAS, respaldos y recuperación | Configurar un host y comprobar la restauración de una VM |
| Administrador de redes, NetAdmin | Conectividad, switches, routers, VLAN, VPN y perímetro | Investigar pérdida de paquetes o saturación de un enlace |
| Administrador de bases de datos, DBA | Integridad, disponibilidad, seguridad y rendimiento de datos | Optimizar consultas y validar respaldos de una base |
| Especialista de seguridad, SOC | Eventos de seguridad, vulnerabilidades e incidentes | Analizar una alerta del SIEM y coordinar la respuesta |
| Operador de NOC | Monitoreo, tareas programadas, atención inicial y escalamiento | Validar una alerta y seguir el manual de actuación |
| Técnico de infraestructura física, facilities | Racks, cableado, UPS, PDU, climatización y acceso físico | Revisar una alarma ambiental con personal autorizado |

**NOC y SOC no son equivalentes:** el primero se enfoca en operación y disponibilidad; el segundo, en seguridad. Deben colaborar cuando un incidente afecta ambos ámbitos.

### 2.2. Parte técnica: asignar y evaluar el trabajo

La **matriz de habilidades** registra quién domina cada tecnología y con qué nivel. Permite asignar tareas según competencia y detectar dependencias de una sola persona.

**Ejemplo didáctico de matriz:**

| Función | Titular por rol | Respaldo | Brecha que debe resolverse |
|---|---|---|---|
| Restauración de bases de datos | DBA | SysAdmin capacitado | Practicar recuperación y validación de datos |
| Administración de VLAN | NetAdmin | Segundo técnico de redes | Documentar configuración y procedimiento de reversa |
| Triaje de alertas | Operador NOC | Soporte técnico | Capacitar en clasificación y escalamiento |

La optimización combina **formación cruzada**, tickets, balance de carga, turnos y automatización. Cubrir 24/7 no significa que una persona deba estar permanentemente disponible: la planificación debe contemplar descansos, relevos y fatiga.

La evaluación debe combinar:

- **Resolución:** MTTR, volumen de tickets y FCR.
- **Calidad:** reaperturas, adherencia a procedimientos y documentación.
- **Proyectos:** cumplimiento de hitos y calidad de entregables.
- **Desarrollo:** retroalimentación frecuente y un Plan de Desarrollo Individual (PDI).

`FCR = tickets resueltos en primer contacto / tickets totales elegibles × 100`

`MTTR = tiempo total de reparación / número de reparaciones`

El universo de tickets y el inicio/fin del tiempo de reparación deben definirse antes de medir. Si no existen casos elegibles o reparaciones, el indicador se reporta como **no calculable**, no como cero.

### 2.3. Interpretación lógica

**Situación:** un técnico cierra muchos tickets, pero varios se reabren.

**Razonamiento:** el volumen mide producción, no resolución definitiva. Si se premia solo la cantidad, se incentivan cierres apresurados. Hay que revisar complejidad, reaperturas, satisfacción y cumplimiento del procedimiento antes de concluir que su desempeño es mejor.

**Decisión:** ajustar la evaluación, capacitar en diagnóstico y mejorar la documentación. No atribuir un MTTR alto únicamente al técnico: puede depender de falta de repuestos, accesos, escalamiento o soporte del proveedor.

## 3. Inventario, control y mantenimiento

### 3.1. Conceptos esenciales

**Inventario** significa identificar los activos existentes. **Control** significa gestionar su asignación, uso, estado y cambios. **Trazabilidad** permite reconstruir qué ocurrió con un activo, cuándo, por qué y quién intervino.

El inventario incluye servidores, equipos de laboratorio, periféricos, dispositivos de red, cableado y licencias. No debe limitarse a contar computadoras.

| Tipo de mantenimiento | Momento | Finalidad | Ejemplo |
|---|---|---|---|
| Preventivo | Antes de la falla, según programación y riesgo | Reducir probabilidad de incidentes | Revisar ventilación, respaldos, actualizaciones y UPS |
| Correctivo | Después de una falla | Recuperar el funcionamiento | Sustituir un disco dañado y validar el servicio |

**Complemento conceptual:** el mantenimiento predictivo utiliza señales e historial para anticipar fallas; se desarrolla con AIOps en la unidad 4. No es sinónimo de mantenimiento programado.

### 3.2. Parte técnica: qué registrar y qué herramienta utilizar

La presentación exige código, ubicación, responsable, adquisición, proveedor, estado e historial. Para las prácticas, conviene añadir los campos complementarios de garantía, versión, criticidad y dependencias:

| Campo | Utilidad administrativa o técnica |
|---|---|
| Identificador y número de serie | Evitar confundir equipos similares |
| Ubicación, rack y unidades U | Localizar y planificar espacio |
| Área responsable y custodio | Establecer responsabilidad por el activo |
| Fecha, proveedor y garantía | Planificar soporte y renovación |
| Estado: activo, reparación o baja | Conocer si está disponible |
| Hardware, SO, versión y firmware | Evaluar compatibilidad y actualizaciones |
| Licencia, cantidad y vencimiento | Verificar derechos de uso y renovaciones |
| Servicio soportado y criticidad | Priorizar mantenimiento según impacto |
| Historial y ticket asociado | Reconstruir cambios y fallas |

Una **CMDB**, como complemento técnico, registra elementos de configuración y relaciones entre servicios y componentes. Un inventario indica que existe un servidor; sus relaciones permiten saber qué aplicaciones se afectan si falla.

| Herramienta mencionada en clase | Uso principal en este contexto |
|---|---|
| GLPI + OCS Inventory NG | Inventario, descubrimiento y soporte mediante tickets |
| SCCM o Lansweeper | Detección de equipos y software en entornos corporativos |
| DWService | Acceso remoto para soporte; requiere controles de acceso |
| Zabbix | Monitoreo del estado y métricas de los activos |
| Grafana | Visualización de datos; no sustituye por sí sola el inventario |
| Etiquetas QR | Vincular el equipo físico con su ficha digital |

**Procedimiento de mantenimiento recomendado:**

1. Identificar activo, criticidad, responsable y dependencia de servicios.
2. Preparar diagnóstico, ventana autorizada, respaldo recuperable y plan de reversa.
3. Ejecutar la intervención por personal competente siguiendo el procedimiento.
4. Validar hardware, datos y funcionamiento del servicio, no solo el encendido.
5. Registrar fecha, diagnóstico, causa conocida, repuestos, responsable y resultado.
6. Actualizar inventario y revisar si corresponde otra acción preventiva.

La presentación propone mantenimientos trimestrales como ejemplo. La frecuencia real debe ajustarse al fabricante, las condiciones ambientales y el riesgo. Trabajos eléctricos, UPS y climatización corresponden a personal autorizado; esta guía no reemplaza sus procedimientos de seguridad.

### 3.3. Interpretación lógica

**Situación:** un servidor está fuera de garantía, pero todavía funciona.

**Razonamiento:** funcionar hoy no garantiza soporte, repuestos ni compatibilidad futura. También hay que distinguir el vencimiento de garantía del **fin de soporte** del fabricante.

**Decisión:** evaluar criticidad, costo y migración. No darlo de baja inmediatamente si sostiene un servicio necesario: primero mapear dependencias, probar el reemplazo y obtener aceptación. La baja debe incluir disposición segura de los datos y actualización formal del registro.

**Idea clave:** el historial de fallas transforma el inventario en evidencia para decidir. Si un mismo activo exige reparaciones frecuentes, puede ser más razonable renovarlo que continuar financiando correctivos.

## 4. Monitoreo de redes, infraestructura y servicios

### 4.1. Qué observar

El monitoreo convierte una operación reactiva en proactiva cuando sus datos generan acciones.

| Capa | Variables | Pregunta que responde |
|---|---|---|
| Red | Estado de puertos, tráfico, latencia, pérdida y errores | ¿La comunicación funciona y tiene capacidad suficiente? |
| Servidor | CPU, RAM, IOPS, espacio y temperatura | ¿El equipo dispone de recursos para la carga? |
| Entorno físico | UPS, PDU, temperatura y humedad | ¿Hay condiciones seguras para operar? |
| Aplicación o servicio | Respuesta, transacciones, errores y consultas | ¿El usuario puede completar su tarea? |
| Logs | Eventos y registros centralizados | ¿Qué pasó antes y durante el problema? |

**APM** es monitoreo del rendimiento de aplicaciones. Complementa las métricas del equipo: un servidor puede responder al ping y aun así tener una aplicación inutilizable.

### 4.2. Parte técnica: herramientas y métricas

**SNMP** permite consultar estado y contadores de dispositivos. **NetFlow/sFlow** ayudan a analizar los flujos de tráfico. Como recomendación complementaria, proteger las consultas y utilizar mecanismos seguros compatibles con los equipos.

Zabbix integra monitoreo de infraestructura y servicios; Prometheus recolecta métricas y Grafana las visualiza. Las diapositivas también mencionan SolarWinds NPM, Datadog y Dynatrace. La elección depende del entorno, costo, integración y capacidad del equipo, no del nombre de la herramienta.

| Concepto | Definición e interpretación |
|---|---|
| Disponibilidad | Porcentaje del periodo acordado en que el servicio estuvo operativo |
| Latencia o RTT | Tiempo de ida y vuelta; se expresa, por ejemplo, en milisegundos |
| Throughput | Transferencia efectiva; no equivale a la velocidad nominal del enlace |
| IOPS | Operaciones de entrada/salida por segundo; interpretar junto con latencia y carga |
| Tasa de errores | Solicitudes fallidas / solicitudes totales × 100 |
| SLA | Acuerdo con el negocio sobre nivel de servicio y condiciones de medición |

`Disponibilidad = (tiempo del periodo − tiempo de caída) / tiempo del periodo × 100`

**Ejemplo didáctico:** para un servicio 24/7 y un mes de 30 días:

```text
Tiempo del mes = 30 × 24 × 60 = 43.200 minutos
Caída permitida con SLA 99,9% = 43.200 × 0,001 = 43,2 minutos
Caída observada = 60 minutos
Disponibilidad = (43.200 − 60) / 43.200 × 100 = 99,8611%
Conclusión: no cumple el 99,9%.
```

Las exclusiones por mantenimiento deben estar acordadas; no se deben descontar unilateralmente para mejorar el indicador. Los tiempos anuales de caída de las diapositivas son aproximaciones para 365 días, no límites universales de criticidad.

### 4.3. Alertas, diagnóstico y escalamiento

Las diapositivas dan ejemplos de umbrales: CPU superior al 80% durante 10 minutos, CPU superior al 95% durante 5 minutos, espacio libre inferior al 5% y pérdida de paquetes superior al 2%. **Son referencias de clase, no valores obligatorios para cualquier servicio.**

Una alerta útil necesita activo, métrica, duración, severidad, impacto, responsable y procedimiento. Las dependencias reducen ruido: si cae un host, se deben correlacionar las alertas de sus VM sin perder visibilidad del impacto.

```text
Detección → triaje → ticket → procedimiento autorizado
                  ↓
¿Servicio recuperado y validado?
Sí → documentar y cerrar
No → escalar por especialidad, impacto y tiempo acordado
```

La presentación de monitoreo organiza el escalamiento como **nivel 0: NOC; nivel 1: soporte/junior; nivel 2: especialistas; nivel 3: ingeniería/proveedor**. La de personal llama al NOC atención de nivel 1. La numeración varía; lo importante es documentar responsables, competencias y tiempos sin ambigüedad.

El escalamiento gerencial comunica impacto y decisiones al negocio. Una incidencia grave puede exigirlo inmediatamente, sin esperar a recorrer todos los niveles técnicos.

### 4.4. Interpretación lógica

**Situación:** el portal está lento, el servidor responde al ping y la CPU está al 40%.

**Razonamiento:** el ping demuestra conectividad básica, no una transacción exitosa. Una CPU moderada no descarta espera de disco, consultas bloqueadas, red saturada o servicios externos lentos.

**Decisión:** observar tiempos de aplicación, errores, consultas, latencia de almacenamiento y red en el mismo intervalo. Formular y verificar hipótesis antes de reiniciar o comprar hardware. Una correlación temporal orienta el diagnóstico, pero no demuestra por sí sola la causa.

## 5. Automatización de procesos administrativos

### 5.1. Algoritmo, script y orquestación

| Concepto | Qué hace | Ejemplo de clase |
|---|---|---|
| Algoritmo | Define una secuencia lógica de pasos | Revisar discos y alertar si el uso supera el 90% |
| Script | Implementa la lógica en un lenguaje ejecutable | Consultar servidores y generar el reporte |
| Automatización | Ejecuta una tarea repetible | Crear una cuenta o aplicar un parche |
| Orquestación | Coordina varias tareas y sistemas | Aprobar solicitud, crear VM, configurarla y registrar el resultado |
| API | Permite interacción programática entre sistemas | El gestor de tickets solicita una operación a otra plataforma |
| IaC | Describe y gestiona infraestructura como código | Provisionar redes y VM con Terraform |

Bash es habitual en Linux/Unix; PowerShell trabaja con objetos y administración de entornos Microsoft; Python facilita lógica, datos y APIs.

**Ansible** se centra en configuración y estado deseado. **Terraform** se centra en aprovisionamiento. ServiceNow o Jira Service Management pueden coordinar solicitudes y aprobaciones. La integración real exige configurar APIs, permisos y ejecución; no aparece automáticamente al instalar las herramientas.

### 5.2. Parte técnica: lógica controlada

**Pseudocódigo didáctico de revisión de disco, no script ejecutable:**

```text
PARA CADA servidor autorizado del inventario:
    consultar capacidad y espacio utilizado
    SI la consulta falla O la capacidad no es válida:
        registrar el error y notificar fallo de monitoreo
        continuar con el siguiente servidor
    calcular porcentaje = utilizado / capacidad × 100
    registrar servidor, fecha y porcentaje
    SI porcentaje > 90:
        generar alerta asociada al activo
        evitar tickets duplicados para el mismo evento abierto
    NO borrar archivos automáticamente
FIN
```

La condición de error es fundamental: **no recibir datos no significa que el equipo esté sano**. Asimismo, una alerta de disco no autoriza a borrar logs o respaldos sujetos a retención.

**Controles complementarios para una automatización fiable:**

- Alcance explícito, cuenta de servicio con mínimo privilegio y secretos fuera del código.
- Pruebas en laboratorio, aprobación y ventana de ejecución cuando corresponda.
- Validación de entradas, errores visibles y registros sin datos sensibles.
- Idempotencia cuando sea posible: repetir la operación no crea duplicados ni cambios adicionales.
- Reintentos limitados, verificación posterior, reversa y escalamiento si falla.

**Auto-reparación:** detectar un servicio detenido, intentar una recuperación autorizada, comprobar una transacción y escalar si no funciona. Evitar bucles de reinicio: pueden ocultar la causa, empeorar una falla o interferir con una intervención de seguridad.

### 5.3. Casos de uso y razonamiento

| Proceso | Flujo automatizado | Validación indispensable |
|---|---|---|
| Alta de personal | Evento autorizado de RR. HH. → cuenta → grupos → licencias | Identidad, rol y permisos correctos |
| Baja de personal | Baja autorizada → revocar accesos → cerrar sesiones → gestionar datos | Sin accesos residuales y con retención institucional |
| Parches | Detectar faltantes → probar → aplicar por oleadas → comprobar | Aplicación sana y posibilidad de reversa |
| Respaldos | Ejecutar copia → registrar → verificar → probar restauración | Datos recuperables, no solo tarea finalizada |
| Nueva VM | Solicitud → aprobación → provisión → configuración → inventario | Capacidad, seguridad, monitoreo y responsable asignado |

**Interpretación lógica:** automatizar un procedimiento incorrecto multiplica su error. Primero estandarizar y probar; después automatizar. La ausencia de intervención manual en una ejecución no elimina la responsabilidad humana por su diseño y supervisión.

## 6. Prácticas importantes

Realizar las prácticas con datos simulados o en laboratorio autorizado. No usar credenciales reales ni intervenir equipos institucionales sin permiso.

### Práctica 1 — Inventario y mantenimiento trazable

**Objetivo:** vincular activos, servicios y responsables.

1. Registrar seis activos simulados: servidor, switch, UPS, equipo de laboratorio, VM y licencia.
2. Completar los campos de la sección 3 y relacionarlos con al menos dos servicios.
3. Diseñar un mantenimiento preventivo con ventana, responsable y criterio de aceptación.
4. Simular un correctivo y registrar diagnóstico, repuesto, validación y actualización del estado.

**Entregable:** inventario y dos fichas de mantenimiento. **Comprobación:** otra persona debe poder localizar el activo, conocer qué servicio afecta y reconstruir la intervención.

### Práctica 2 — Atención de un portal lento

**Datos didácticos:** CPU 45%, RAM 65%, enlace nominal de 1 Gbps con 920 Mbps medidos, RTT de 8 a 80 ms y respuesta web de 1 a 12 segundos durante el mismo intervalo.

**Trabajo:** formular una hipótesis, proponer mediciones, asignar roles y redactar un ticket con escalamiento.

**Interpretación esperada:** `920/1.000 × 100 = 92%` de utilización nominal; la subida de RTT sugiere congestión, pero no confirma la causa. NetAdmin debe revisar flujos, errores y colas; SysAdmin/DBA deben comprobar dependencias de aplicación. Validar una transacción antes de cerrar.

**Entregable:** ticket con evidencia, hipótesis, pruebas, acciones autorizadas y aceptación del servicio.

### Práctica 3 — Evaluación equilibrada del soporte

**Datos didácticos:** 200 tickets elegibles, 140 resueltos en primer contacto; 10 de los 180 tickets cerrados se reabren; cuatro reparaciones suman ocho horas.

```text
FCR = 140/200 × 100 = 70%
Tasa de reapertura = 10/180 × 100 = 5,56%
MTTR = 8/4 = 2 horas
```

**Trabajo:** explicar qué mide cada resultado y proponer una mejora del PDI. **Comprobación:** no concluir desempeño individual sin revisar complejidad, recursos y línea base.

### Práctica 4 — Diseñar una automatización segura

**Objetivo:** orquestar una solicitud de VM sin ejecutarla en producción.

Diseñar el flujo solicitud → aprobación → capacidad → aprovisionamiento → configuración → prueba → inventario → notificación. Incluir tres situaciones: ejecución correcta, solicitud duplicada y configuración fallida.

**Entregable:** pseudocódigo y tabla de entradas/resultados esperados. **Comprobación:** una solicitud repetida no crea otra VM; un fallo no genera mensaje de éxito; recursos parciales se gestionan según un procedimiento explícito.

### Práctica 5 — Conexión con la Integradora 3

Consultar el [caso original de crecimiento, presupuesto y KPIs](<../Integradora_tres/Caso_Crecimiento_Presupuesto_KPIs.docx>) y la [guía de resolución](<../Integradora_tres/readme_integradora3.md>).

El caso identifica **nueve servidores fuera de garantía**, con mantenimiento de **USD 48.000 anuales**. Diseñar su tratamiento desde esta unidad: inventario de cargas, prioridad, responsables, capacitación, migración, pruebas, monitoreo y baja.

**Comprobación:** el ahorro solo puede materializarse cuando se retiren las cargas y el contrato pueda cancelarse. No afirmar que los nueve equipos son los tres hosts del clúster: el caso no establece esa equivalencia.

## 7. Preguntas de comprensión con respuestas

| Pregunta | Respuesta razonada |
|---|---|
| ¿Por qué no basta con conocer el número de equipos? | Falta saber estado, ubicación, responsables, dependencias y ciclo de vida. |
| ¿Qué diferencia al NOC del SOC? | El NOC atiende operación; el SOC, seguridad. Coordinan incidentes compartidos. |
| ¿Qué evita la formación cruzada? | Que la operación dependa del conocimiento de una sola persona. |
| ¿Un correctivo termina al cambiar el componente? | No: exige validar el servicio y registrar la intervención. |
| ¿Responder al ping demuestra disponibilidad de la aplicación? | No: hay que comprobar su función desde la perspectiva del usuario. |
| ¿Por qué una alerta necesita duración? | Para distinguir un pico transitorio de una condición persistente relevante. |
| ¿Qué se debe hacer con alertas de VM tras caer su host? | Correlacionarlas mediante dependencias y conservar el impacto registrado. |
| ¿Algoritmo y script son lo mismo? | No: uno define la lógica y el otro la implementa. |
| ¿Qué añade la orquestación? | Coordinación entre tareas, sistemas, aprobaciones y resultados. |
| ¿Un respaldo exitoso demuestra recuperación? | No: debe probarse la restauración y la integridad de los datos. |
| ¿Cerrar más tickets implica mejor soporte? | No necesariamente; importan complejidad, calidad y reaperturas. |
| ¿Cuál es el límite de la auto-reparación? | Solo acciones autorizadas, verificadas y acotadas; si falla, escalar. |

## 8. Lista de comprobación para estudiar o sustentar

- Puedo asignar responsabilidades y explicar cuándo escalar.
- Puedo relacionar un activo con los servicios que dependen de él.
- Distingo mantenimiento preventivo, correctivo y predictivo.
- Puedo calcular disponibilidad, FCR y MTTR con unidades y denominadores claros.
- Distingo disponibilidad técnica de rendimiento percibido por el usuario.
- Puedo justificar una alerta con línea base, duración e impacto.
- Puedo diseñar una automatización con errores visibles, permisos y validación.
- Puedo convertir los registros operativos en evidencia para la planificación de la unidad 4.
