# Integradora 3 — Guía completa para analizar y resolver el caso

**Asignatura:** Administración de Centros de Cómputo  
**Caso:** *Crecimiento, presupuesto e indicadores (KPIs)* — Universidad Regional Andina (URA)  
**Horizonte:** diagnóstico al 30 de junio de 2026; plan operativo y presupuesto 2027  
**Entregables:** informe ejecutivo editable con anexos de cálculo; el caso solicita una versión final PDF.

Esta guía explica el propósito de cada parte, el procedimiento recomendado, los cálculos reproducibles, los criterios técnicos y los puntos que deben verificarse antes de presentar la solución. El documento editable resuelto que acompaña a esta guía se llama `Informe_Caso_Crecimiento_Presupuesto_KPIs.docx`.

> **Criterio de lectura:** las cifras se calculan con los datos y supuestos fijos del caso. Cuando falta un dato —por ejemplo, la topología interna del SAN— se marca la limitación en vez de presentar una hipótesis como un hecho. Las cotizaciones son preliminares y no sustituyen el diseño detallado ni la aprobación institucional.

## 1. Qué pide el caso y cómo organizar el trabajo

El caso entrega una institución con 14.000 estudiantes y 1.100 funcionarios, servicios centrales críticos, una infraestructura con poco margen, incidentes crecientes y un límite presupuestario de USD 520.000. El informe debe convertir esa evidencia en una decisión ejecutiva, no limitarse a completar tablas. El trabajo está dividido en seis partes:

| Parte | Pregunta que responde | Producto principal |
|---|---|---|
| A. Diagnóstico de capacidad | ¿Qué puede soportar la infraestructura hoy y qué falla bajo N+1? | Tabla de capacidad, hallazgos de cinco pilares y decisión sobre los servidores legacy |
| B. Proyección | ¿Qué capacidad hará falta para el crecimiento conocido y cuándo? | Línea base, demanda de negocio, dimensionamiento y fecha de aprobación |
| C. POA 2027 | ¿Qué se hará, quién lo hará y cuándo? | Tres objetivos SMART y al menos cinco iniciativas con dependencias |
| D. Presupuesto | ¿Cuánto cuesta y cómo se controla? | Clasificación CAPEX/OPEX, total, ZBB, forecast y control de cambios |
| E. KPIs | ¿Cómo se medirá la mejora? | Cálculos mensuales/semestrales, umbrales, tendencias y ciclo PDCA |
| F. Decisión ejecutiva | ¿Qué debe aprobar el Consejo? | Resumen, tablero de cinco indicadores, supuestos, fuentes y preguntas anticipadas |

### Secuencia de resolución recomendada

1. **Fijar la línea base:** usar exclusivamente el estado al 30/06/2026 y distinguir capacidad instalada, capacidad utilizable, consumo promedio y pico.
2. **Calcular riesgos actuales:** aplicar N+1 (se pierde un elemento), y después comparar la carga normal con el 75% de la capacidad que queda.
3. **Proyectar por dos vías:** tendencia histórica (almacenamiento) y demanda del negocio (estudiantes, procesos financieros, SLA).
4. **Traducir brechas a proyectos:** formular objetivos SMART, responsables por rol, hitos y dependencias.
5. **Costear las soluciones:** clasificar cada partida una sola vez; explicitar costos recurrentes y supuestos.
6. **Medir resultados:** calcular los KPIs con denominadores consistentes y separar medición observada de estimaciones.
7. **Cerrar con una decisión:** monto solicitado, riesgos de no actuar, beneficios y condiciones para liberar la inversión.

## 2. Base técnica de las unidades 1 a 4

El caso requiere combinar contenidos de toda la materia. No se debe tratar como un ejercicio aislado de Excel.

### Unidad 1 — Estructura, normas y modelos de centro de cómputo

- **Centro de cómputo como ecosistema:** hardware, software, datos, procesos y personal; por eso la decisión cubre capacidad, continuidad, servicio y responsabilidades.
- **Roles y gobierno:** el director alinea tecnología con el plan institucional; administradores de sistemas, redes, bases de datos, seguridad, soporte y facilities ejecutan partes diferentes del plan.
- **Estándares y prácticas:** ITIL sirve como marco de buenas prácticas de gestión de servicios; ISO/IEC 20000 trata el sistema de gestión de servicios; ISO/IEC 27001, la gestión de seguridad de información; ANSI/TIA-942 orienta el diseño de infraestructura de telecomunicaciones. No son equivalentes.
- **Operación del recinto:** separación de pasillos fríos/calientes, medición ambiental, mantenimiento preventivo, UPS, etiquetado y monitoreo tipo DCIM fundamentan las acciones de energía, refrigeración y gestión de cambios.
- **On-premise, nube e híbrido:** la URA puede mantener cargas críticas en su centro y evaluar nube para respaldo geográfico, archivo o picos no permanentes. No debe prometerse *cloud bursting* sin verificar integración, conectividad, seguridad, costos y licencias.
- **Aplicaciones y bases de datos:** dos bases nuevas requieren análisis de CPU, I/O, respaldo, latencia, seguridad y ambientes de prueba; las aplicaciones financieras y académicas requieren alta disponibilidad y un plan de recuperación.

### Unidad 2 — Seguridad y continuidad

- Evaluar confidencialidad, integridad y disponibilidad (CID), acceso físico y lógico, autenticación/autorización, parches, privilegios y segmentación.
- Respaldos completos, incrementales o diferenciales deben probarse; una copia no restaurada no demuestra recuperabilidad.
- Definir BCP/DRP con análisis de impacto, responsables, comunicaciones, RTO/RPO acordados con las áreas y pruebas periódicas. El caso no proporciona RTO/RPO, por tanto deben proponerse como tarea de aprobación, no inventarse.
- Tratar IoT (sensores, cámaras, PDU) como parte de la superficie de seguridad: inventario, cambio de credenciales, firmware, VLAN aislada y acceso restringido.
- Para la matrícula, planificar mantenimiento fuera del periodo de inscripción, controlar cambios, proteger respaldos y realizar pruebas de recuperación.

### Unidad 3 — Personal, inventario, monitoreo y automatización

- Mantener inventario/CMDB con ubicación, responsable, garantía, licencias, firmware y ciclo de vida; priorizar los nueve servidores fuera de garantía.
- Monitorear servicios y recursos (CPU, almacenamiento, red, temperatura, UPS, CRAC) y establecer umbrales accionables con escalamiento y tickets.
- Aplicar mantenimiento preventivo, registrar causa raíz y cambios, y gestionar incidentes conforme a roles y niveles de escalamiento.
- Utilizar automatización de forma controlada (parches por oleadas, aprovisionamiento repetible, alertas, respaldos y reportes); cada automatización debe tener aprobación, bitácora y reversa.
- Capacitar y cruzar conocimiento entre el personal para no depender de una sola persona ni de un proveedor para operar el nuevo entorno.

### Unidad 4 — Planeación, presupuesto, KPIs y tendencias

- Proyectar capacidad con historial, consultas al negocio y escenarios; dimensionar para N+1 y reserva, no para el promedio aislado.
- Alinear el POA con objetivos institucionales y convertirlos en metas SMART, iniciativas, recursos, responsables, fechas e indicadores.
- Diferenciar CAPEX (activos de vida útil) de OPEX (licencias recurrentes, servicios, capacitación y energía); confirmar con Finanzas cualquier tratamiento contable dudoso.
- Usar ZBB para volver a justificar contratos y servicios heredados; medir variaciones mensualmente, actualizar el forecast y controlar cambios.
- Leer tendencias y correlacionar indicadores. Aplicar PDCA: planificar una acción, ejecutarla, verificar el KPI y estandarizar o corregir.
- Las tendencias (HCI, virtualización, almacenamiento flash, automatización, nube híbrida, Green IT) solo son útiles si resuelven una brecha probada y caben en las capacidades y presupuesto.

## 3. Datos de partida que no deben confundirse

- **Cómputo:** 3 hosts de 64 núcleos; uso promedio 58% y pico 84% del clúster actual. Las 140 VM describen inventario, no una capacidad adicional.
- **Almacenamiento:** 40 TB utilizables y 31 TB ocupados. El caso no especifica discos, controladoras, arreglos independientes ni capacidad de failover del SAN.
- **Energía:** 2 UPS de 120 kW; carga TI de 85 kW.
- **Refrigeración:** 2 unidades CRAC de 50 kW; carga térmica de 85 kW.
- **Racks:** 6 × 42 U = 252 U; 210 U ocupadas.
- **Red:** núcleo de 1 GbE; el tráfico pico de almacenamiento es 720 Mbps (72% del enlace nominal, antes de considerar otros flujos y overhead).
- **Legacy:** 9 servidores sin garantía; mantenimiento USD 48.000/año.
- **Matrícula:** SLA vigente 99,9%; meta de Admisiones para 2027: 99,95%.
- **Presupuesto 2026:** USD 480.000 (CAPEX 200.000 y OPEX 280.000); ejecutado a junio USD 270.000.

## 4. Parte A — Diagnóstico de capacidad

### A1. Regla de cálculo

Para cada recurso, retirar un elemento de capacidad y calcular:

`Utilización N+1 = carga actual / capacidad que permanece con un elemento fuera de servicio × 100`

Después comparar contra el límite del caso: carga normal ≤ 75% de esa capacidad N+1. No basta con tener redundancia nominal si, al perderla, el recurso supera el umbral.

| Recurso | Capacidad N+1 que queda | Uso | Uso sobre N+1 | Resultado |
|---|---:|---:|---:|---|
| SAN | No determinable a nivel de arreglo completo; 40 TB solo si el SAN aporta tolerancia interna a falla y no se pierde el arreglo completo | 31 TB | 77,5% bajo esa hipótesis | Supera 75%; verificar arquitectura, réplica y capacidad efectiva |
| UPS | 1 × 120 = 120 kW | 85 kW | 70,83% | Cumple por 5 kW de margen respecto al límite de 90 kW |
| CRAC | 1 × 50 = 50 kW | 85 kW térmicos | 170% | No cumple ni la capacidad N+1 ni el margen |
| Cómputo | 2 hosts × 64 núcleos = 128 núcleos equivalentes | 58% × 3 = 1,74 hosts equivalentes | 1,74/2 = 87% | Sobrevive carga media, pero incumple 75% |
| Racks | 5 × 42 = 210 U tras perder un rack | 210 U | 100% | Sin espacio de reserva N+1 |

**Limitación del SAN:** no hay datos para calcular la capacidad que quedaría si falla un arreglo, una controladora o un conjunto de discos. La tabla usa 40 TB como capacidad efectiva N+1 únicamente si el fabricante confirma tolerancia interna y capacidad reconstruida. Si el requisito incluye la pérdida del arreglo completo, debe existir un segundo destino/servicio y su capacidad no está indicada.

### A2. ¿Sobrevive el clúster al pico actual si pierde un host?

`Pico actual = 84% × 3 hosts = 2,52 hosts equivalentes`  
`Capacidad tras perder un host = 2 hosts`  
`2,52 / 2 = 126%`

**No sobrevive sin degradación:** el pico supera en 0,52 host equivalente la capacidad remanente. Se debe reducir el riesgo antes de aumentar cargas.

### A3. Cinco pilares del diagnóstico

1. **Espacio:** 83,33% de las U ocupadas; al perder un rack, la ocupación de los cinco restantes sería 100%.
2. **Potencia:** 85/120 = 70,83% después de la pérdida de una UPS; pasa el umbral actual con margen estrecho.
3. **Enfriamiento:** 85/50 = 170% si falla una unidad; es el riesgo inmediato para hardware y disponibilidad.
4. **Cómputo y almacenamiento:** cómputo al 87% de dos hosts tras falla; almacenamiento al 77,5% de 40 TB y crecimiento acelerado.
5. **Ciclo de vida:** nueve equipos sin garantía, con gasto de USD 48.000/año y riesgo de seguridad, repuestos y soporte.

La refrigeración es más urgente que el espacio porque la carga térmica excede incluso la capacidad restante tras la falla, con posible impacto rápido y simultáneo en todos los equipos. El espacio también falla el criterio de reserva; la expansión debe incluir distribución física/racks o una decisión explícita de no depender del rack que se considere indisponible.

### A4. Decisión sobre servidores legacy

Inventariar las cargas y dependencias de los nueve servidores; clasificar criticidad, parcheabilidad, garantía, licencias y plan de respaldo; migrar primero los servicios de mayor riesgo y probar datos, rendimiento y recuperación; retirar cada servidor solo tras aceptación del dueño de servicio y respaldo restaurable. Mantener el contrato mientras existan cargas necesarias en esos equipos. Bajo ZBB, eliminar o renegociar el contrato cuando se complete y valide la migración, con ahorro de USD 48.000 por año a partir del periodo efectivamente cancelable. No se recomienda dar de baja los servidores de forma inmediata.

## 5. Parte B — Proyección y hoja de ruta

### B1. Almacenamiento

El horizonte tiene 18 meses desde 30/06/2026 hasta 31/12/2027.

`Crecimiento base = 2 TB/mes × 18 meses = 36 TB`  
`Uso base proyectado = 31 + 36 = 67 TB`  
`Capacidad total para uso ≤ 75% = 67 / 0,75 = 89,33 TB`  
`Capacidad utilizable adicional sobre los 40 TB actuales = 89,33 − 40 = 49,33 TB`

La carga actual ya es `31/40 = 77,5%`; por tanto, el margen del 75% ya se supera en la línea base al 30/06/2026 (durante junio, si la tendencia lineal se prolonga hacia atrás). El SAN llegaría a 40 TB en aproximadamente `(40−31)/2 = 4,5 meses`, alrededor de mediados de noviembre de 2026, sin considerar nuevas demandas.

### B2. Demanda adicional del negocio

Para 6.000 estudiantes adicionales:

- CPU adicional: `6 × 3% = 18 puntos porcentuales` de la capacidad del clúster actual.
- Almacenamiento LMS: `6 × 80 GB = 480 GB = 0,48 TB` (convención decimal, consistente con TB del caso).
- Carga TI: `6 × 1,5 kW = 9 kW`.

Finanzas requiere 4 TB más. Entonces:

`Uso total de almacenamiento al cierre = 67 + 0,48 + 4 = 71,48 TB`  
`Capacidad total para ≤75% = 71,48/0,75 = 95,31 TB`  
`Capacidad adicional mínima sobre los 40 TB actuales = 55,31 TB`

Conviene especificar al menos **100 TB utilizables efectivos** (después de RAID/reserva y espacio del sistema) para mantener el uso proyectado por debajo de 75%; confirmar que la cotización HCI realmente entrega esa capacidad.

CPU:

- Promedio proyectado sobre el clúster actual: `58% + 18 pp = 76%`.
- Pico proyectado: `84% + 18 pp = 102%`, equivalente a `3 × 1,02 = 3,06 hosts`.
- Supervivencia estricta del pico N+1: se necesitan 4 hosts disponibles después de una falla, por tanto **5 hosts totales**, o **2 adicionales** a los 3 actuales.
- Para conservar también el margen de 25% en el pico proyectado: `3,06/0,75 = 4,08`; se requieren 5 hosts disponibles tras falla, es decir, **6 hosts totales o 3 adicionales**. Se recomienda este dimensionamiento, sujeto a validar compatibilidad, licencias, memoria y capacidad real de cada nodo. No asumir que una cotización de HCI de tres nodos se integra automáticamente al clúster VMware existente.

### B3. Energía y refrigeración después del crecimiento

`Carga TI proyectada = 85 + 9 = 94 kW`

- UPS actuales bajo N+1: `94/120 = 78,33%` — supera el margen de 75%.
- Con tercera UPS de 120 kW: tras la falla de una quedan `2 × 120 = 240 kW`; `94/240 = 39,17%`.
- CRAC existentes bajo N+1: quedan 50 kW — insuficiente.
- Con dos CRAC adicionales (cuatro en total): tras la falla de una quedan 150 kW; `94/150 = 62,67%`.

Las capacidades efectivas deben verificarse ante el fabricante: operación en paralelo, redundancia eléctrica A/B, límites ambientales, distribución por sala y capacidad de refrigeración bajo condiciones reales.

### B4. Fecha de aprobación y urgencia

La tendencia indica saturación del SAN alrededor de mediados de noviembre de 2026, mientras el margen de 75% ya se ha perdido. La decisión debe ser **inmediata**: autorización de compra/medidas puente antes de ese punto, con almacenamiento temporal por tiering/archivo o capacidad contratada aprobada si la entrega del HCI no llega a tiempo. En el contexto de entrega indicado por el caso, el Consejo debe recibir una solicitud urgente, no esperar a la fecha ordinaria de presupuesto. Confirmar plazos reales de adquisición e instalación antes de comprometer una fecha de producción.

## 6. Parte C — POA 2027

Un objetivo SMART incluye resultado concreto, indicador medible, alcance viable, relevancia institucional y fecha. Redactar un resultado, no una actividad (“comprar switches” es iniciativa; “mantener el SLA…” es objetivo).

| Objetivo SMART sugerido | Iniciativas | Responsable principal | Fecha e indicador |
|---|---|---|---|
| Mantener la disponibilidad mensual del portal de matrícula ≥99,95% durante 2027 y completar dos pruebas de recuperación antes del 31/12/2027, programando mantenimientos fuera de matrícula. | N+1 de CRAC/UPS; control de cambios; monitoreo y escalamiento; respaldo inmutable; ejercicios DRP | Director del centro + SysAdmin + Facilities + Admisiones | Mensual y cierre anual; disponibilidad ≥99,95%; dos pruebas registradas |
| Antes del 30/06/2027, disponer de al menos 100 TB útiles, seis nodos equivalentes y core de 10 GbE; con pérdida de un nodo, mantener el pico proyectado ≤75% de la capacidad superviviente. | HCI dimensionada; expansión validada; actualización de red; migración de cargas; inventario/CMDB | SysAdmin + Redes + DBA + Compras | Hito 30/06/2027; TB útiles, CPU y Mbps bajo escenario N+1 |
| Reducir el PUE promedio de línea base 1,788 a ≤1,70 para 31/12/2027 y elevar el FCR ponderado de 65,27% a ≥75% antes del cierre de 2027. | Contención de pasillo frío; sensores y análisis por temporada; mantenimiento de CRAC; base de conocimiento y capacitación cruzada de soporte | Facilities + Jefe de soporte + Director | Medición mensual; PUE ≤1,70; FCR ≥75% |

**Iniciativas mínimas que deben aparecer (cinco o más):**

1. Adquirir/instalar tres nodos HCI y almacenamiento con mínimo de 100 TB utilizables; requiere proveedor y validación de arquitectura/licencias.
2. Ampliar refrigeración con dos CRAC y comprobar balance térmico; requiere contratista especializado.
3. Instalar tercera UPS en paralelo y certificar pruebas A/B; requiere proveedor y ventana de mantenimiento.
4. Migrar core de 1 a 10 GbE; requiere proveedor, plan de cambio y pruebas de rendimiento.
5. Migrar nueve servidores legacy por olas, restaurar desde backup y retirar soporte solo tras aceptación; requiere consultoría temporal y equipo interno.
6. Implementar telemetría y runbooks (CPU, SAN, red, PUE, temperatura, UPS, SLA); SysAdmin/Redes/Facilities y capacitación.
7. Formalizar BCP/DRP, RTO/RPO con cada dueño del servicio y dos simulacros; requiere participación de Admisiones, Finanzas y Vicerrectorado.
8. Capacitar personal en HCI/virtualización, recuperación, operación de CRAC/UPS y prácticas ITIL; partida de capacitación.

### Dependencias de cronograma

Primero aprobar fondos y diseño; luego validar compatibilidad y capacidad, emitir órdenes y preparar el sitio. Instalar redundancia física y red antes de mover cargas. Migrar por grupos después de respaldos probados, pruebas de aceptación y reversa. Retirar legacy al final. Para la inscripción, congelar cambios no esenciales y reservar ventanas acordadas con Admisiones. Medir mensualmente y cerrar cada trimestre con revisión PDCA.

## 7. Parte D — Presupuesto y control

### D1. Clasificación y total

| Partida | Tipo | USD | Tratamiento |
|---|---|---:|---|
| HCI de 3 nodos + All-Flash | CAPEX | 165.000,00 | Activo; confirmar capacidad y compatibilidad |
| Core 10 GbE (2 switches) | CAPEX | 38.000,00 | Activo |
| Dos CRAC adicionales | CAPEX | 84.000,00 | Activo de infraestructura |
| Tercera UPS de 120 kW | CAPEX | 45.000,00 | Activo |
| Renovación de licencias | OPEX | 60.000,00 | Renovación recurrente según cotización |
| Consultoría de migración (pago único) | OPEX* | 30.000,00 | Servicio; confirmar política contable institucional |
| Capacitación | OPEX | 9.000,00 | Servicio de formación |
| Mantenimiento legacy | OPEX | 48.000,00 | Contrato anual; sujeto a salida de legacy |
| Energía incremental | OPEX | 15.610,32 | Costo anual calculado |
| **Total CAPEX** |  | **332.000,00** |  |
| **Total OPEX** |  | **162.610,32** |  |
| **Total 2027** |  | **494.610,32** | Bajo el tope de USD 520.000 |

`Energía anual = 9 kW × 8.760 h × 1,80 × USD 0,11/kWh = USD 15.610,32`

El saldo nominal del tope es `520.000 − 494.610,32 = USD 25.389,68`. Es un margen pequeño para costos no cotizados (rack, cableado, instalación, impuestos, licencias adicionales o contingencias); exigir cotización completa antes de emitir la orden. No sumar CAPEX/OPEX dos veces ni excluir energía.

### D2. ZBB para mantenimiento legacy

El ZBB exige justificar el gasto desde cero. El contrato solo se mantiene mientras proteja equipos que aún prestan servicios necesarios. Con la migración terminada, probada y aceptada, el gasto deja de tener justificación: se cancela/no renueva y libera **USD 48.000 anuales** desde el periodo contractual aplicable. Presupuestarlo en 2027 es una postura conservadora si las fechas de migración/cancelación no están aseguradas; actualizar forecast y reconocer ahorro cuando exista evidencia contractual. No cancelar antes de retirar las dependencias.

### D3. Metodología recomendada

Usar **presupuesto base cero** para revisar contratos (especialmente mantenimiento legacy y licencias) y **presupuesto basado en actividades** para enlazar cada costo a SLA, capacidad y proyectos. Si el formato exige una única metodología, escoger ZBB: hay activos obsoletos, restricción estricta de USD 520.000 y cada partida debe demostrar que reduce un riesgo o habilita una necesidad institucional. Evitar el incrementalismo automático.

### D4. Forecast 2026

`Ejecución semestral / presupuesto anual = 270.000/480.000 = 56,25%`  
`Forecast lineal = 270.000 × 2 = USD 540.000`  
`Variación proyectada = 540.000 − 480.000 = +USD 60.000 = +12,5% del presupuesto`

Al cierre de junio, el gasto supera en USD 30.000 el ritmo lineal permitido para medio año (USD 240.000). Una causa posible es adelanto de compras/mantenimiento o gasto no planificado; es una hipótesis a validar con órdenes, facturas, centros de costo y devengos. Controlar mediante forecast mensual, revisión de variaciones, responsable por partida y aprobación formal de cambios; no congelar gastos críticos sin evaluación de riesgo.

### D5. Escenario ajustado

La suma de las nueve partidas cotizadas **no supera** el tope: no corresponde recortar arbitrariamente un proyecto crítico. Se presenta la base completa de USD 494.610,32. Si los costos de expansión física/racks u otros elementos no cotizados consumen más de los USD 25.389,68 disponibles, volver a priorizar con cotizaciones y análisis de riesgo; proteger primero enfriamiento, energía, almacenamiento y cómputo N+1. La partida de mantenimiento solo se elimina cuando la migración esté validada.

## 8. Parte E — KPIs, umbrales y mejora

### E1. Disponibilidad

Fórmula: `(minutos del periodo − minutos caídos) / minutos del periodo × 100`.

| Mes | Caída (min) | Disponibilidad |
|---|---:|---:|
| Enero | 35 | 99,9190% |
| Febrero | 20 | 99,9537% |
| Marzo | 95 | 99,7801% |
| Abril | 180 | 99,5833% |
| Mayo | 310 | 99,2824% |
| Junio | 150 | 99,6528% |

`Caída semestral = 790 min`; `disponibilidad semestral = (259.200−790)/259.200 = 99,6952%`.  
Con SLA 99,9%, el máximo de caída semestral es `259.200 × 0,001 = 259,2 min`; el exceso observado es **530,8 min**. Para una meta de 99,95%, el límite equivale a 21,6 min por mes de 30 días (129,6 min en un semestre de 180 días). Solo enero y febrero cumplieron el 99,9% mensual de 2026; marzo-junio no.

### E2. FCR

`FCR = tickets resueltos en primer contacto / tickets totales × 100`

| Mes | FCR |
|---|---:|
| Enero | 70,34% |
| Febrero | 71,56% |
| Marzo | 63,71% |
| Abril | 62,81% |
| Mayo | 61,54% |
| Junio | 62,61% |

FCR semestral ponderado: `4.680/7.170 = 65,27%`. La tendencia mejora levemente en febrero, cae con fuerza en marzo y continúa hasta mayo, con recuperación marginal en junio. Una hipótesis es el aumento de volumen/complexidad de incidentes y la presión sobre soporte; validar con categorías de tickets, reaperturas, turnos y habilidades antes de atribuir causa.

### E3. PUE

`PUE promedio = (1,78+1,76+1,74+1,80+1,82+1,83)/6 = 1,7883 ≈ 1,79`.

La secuencia puede ser coherente con mayor demanda de refrigeración en meses cálidos, mezcla de aire o carga/condiciones distintas; los datos no incluyen temperatura exterior ni energía de enfriamiento por separado, así que es una hipótesis. Instalar contención de pasillos frío/caliente, revisar sensores y consignas CRAC, limpiar filtros y medir energía por subsistema. Verificar el efecto con la misma metodología de medición mensual.

### E4. Umbrales de gestión sugeridos

Los umbrales son disparadores internos de respuesta, no sustituyen el SLA ni una especificación del fabricante.

| KPI | Amarillo (advertencia) | Rojo (crítico) | Base que justifica el umbral |
|---|---|---|---|
| Disponibilidad mensual | <99,97% | <99,95% o incumplimiento del SLA vigente | 2026 tuvo meses bajo 99,9%; meta 2027 es 99,95% |
| FCR | <70% | <65% | Base semestral 65,27%, con caída mensual hasta 61,54% |
| PUE | >1,75 | >1,80 | Promedio 1,788; abril-junio ya estuvo en 1,80–1,83 |
| CPU clúster | >70% sostenido | >75% normal o pico que no sobreviva a una falla N+1 | Promedio 58%, pico 84%; la previsión llega a 76% promedio/102% pico sobre capacidad actual |

Cada alerta requiere dueño, ventana de evaluación, umbral sostenido, ticket y acción. Para CPU, diferenciar promedio, pico y capacidad disponible tras falla; no comparar una métrica de clúster con un host aislado.

### Tablero ejecutivo de cinco KPIs

| Indicador | Línea base | Meta 2027 | Tendencia / acción |
|---|---|---|---|
| Disponibilidad de matrícula | 99,6952% semestral (790 min caídos) | ≥99,95% mensual | Degradación mar–jun; redundancia, ventanas controladas y pruebas DR |
| FCR | 65,27% ponderado | ≥75% | Caída hasta mayo; capacitación, runbooks y análisis de tickets |
| PUE | 1,7883 promedio | ≤1,70 al 31/12/2027 | Sube abr–jun; contención de aire y eficiencia CRAC |
| CPU | 58% promedio / 84% pico | Pico ≤75% de capacidad N+1 proyectada | Añadir 3 nodos equivalentes; recalcular con telemetría real |
| Almacenamiento | 31/40 TB = 77,5% | ≥100 TB útiles y utilización ≤75% al cierre de 2027 | Umbral ya superado; comprar/activar expansión con urgencia |

**MTTR complementario:** el caso ya reporta promedio mensual. Su media simple es 2,92 h; ponderando por incidentes (si cada incidente equivale a una reparación) es 3,24 h. La equivalencia de incidentes y reparaciones debe confirmarse antes de reportar el ponderado como MTTR oficial. Para MTBF, los “incidentes” no están definidos como fallas del portal ni del mismo componente; no publicar un MTBF causal sin clasificar eventos y exposición por servicio.

### PDCA aplicado a la URA

- **Planificar:** revisar disponibilidad, FCR, PUE, CPU y almacenamiento; elegir la causa prioritaria, definir la meta y ventana.
- **Hacer:** desplegar redundancia, ajuste de refrigeración, capacitación o runbook mediante cambios aprobados.
- **Verificar:** comparar la métrica con la línea base, el periodo y la definición idéntica; verificar también que no se trasladó el problema a otra capa.
- **Actuar:** estandarizar si funcionó; si no, analizar causa raíz, ajustar umbral o solución y volver a medir.

## 9. Parte F — decisión para el Consejo

### Mensaje ejecutivo sugerido

Solicitar aprobar un presupuesto de **USD 494.610,32** para 2027 (USD 332.000 CAPEX y USD 162.610,32 OPEX) y autorizar medidas urgentes de continuidad/almacenamiento. La decisión está motivada por la falla N+1 de refrigeración, el pico de CPU que no sobrevive la pérdida de un host, el SAN por encima del umbral de 75%, el tráfico de red cercano al límite y el incumplimiento del SLA semestral. La inversión moderniza capacidad, reduce interrupciones, permite crecer el LMS y digitalizar procesos. La falta de inversión expone matrícula, sistemas académico y financiero a indisponibilidad, pérdida de datos y costos de emergencia.

### Preguntas que conviene anticipar

1. **¿Por qué invertir si el total está dentro del tope?** Porque el gasto responde a brechas cuantificadas; el margen libre es solo USD 25.389,68 y todavía hay costos de expansión física/instalación sin cotizar.
2. **¿Por qué no migrar todo a nube?** No hay TCO, requisitos regulatorios, conectividad, RTO/RPO ni precio de nube en el caso. Se recomienda arquitectura híbrida controlada como opción a evaluar; primero asegurar capacidad y continuidad local.
3. **¿Se puede cancelar ya el contrato legacy?** No. Debe mantenerse hasta completar, probar y aceptar la migración; luego puede liberar USD 48.000/año según la fecha de renovación/cancelación.
4. **¿Se garantiza 99,95% con estas compras?** No por sí solas. Se necesita operación controlada, redundancia efectiva, monitoreo, gestión de cambios y pruebas de recuperación. El objetivo debe medirse y revisarse con Admisiones.

## 10. Supuestos, límites y control de calidad

1. Se usa el mes de 43.200 minutos y semestre de 259.200 minutos indicado en el caso.
2. Los 80 GB por 1.000 usuarios se convierten como 0,08 TB; por tanto 480 GB = 0,48 TB. Confirmar convención decimal/binaria antes de comprar.
3. La carga térmica futura aumenta en 9 kW igual que la carga TI; la relación real depende de eficiencia y configuración de la sala.
4. La carga proyectada asume el crecimiento LMS simultáneo, el crecimiento de almacenamiento continúa linealmente y Finanzas agrega 4 TB una sola vez.
5. Los porcentajes de CPU adicional se interpretan como puntos porcentuales de la capacidad total actual del clúster, conforme a la redacción del caso.
6. El SAN no incluye datos para demostrar redundancia de arreglo; no se presupone que RAID proteja frente a pérdida total del SAN.
7. El cálculo de N+1 considera capacidad nominal, sin derating ambiental, licencias, memoria, IOPS o límites de carga por rack; el diseño debe validarlos.
8. Consultoría y capacitación se clasifican OPEX para fines del caso; la política contable de la URA puede definir otro tratamiento para costos capitalizables.
9. Los USD 15.610,32 de energía son un costo anualizado de los 9 kW adicionales usando PUE 1,80 y tarifa USD 0,11/kWh.
10. Los costos del caso son cotizaciones preliminares en dólares de 2026. No se añaden impuestos, escalamiento de precio ni costos no listados.
11. Los datos no explican la causa del aumento de caídas, FCR o PUE; las causas sugeridas son hipótesis para validar, no conclusiones causales.
12. La media ponderada de MTTR supone que el número de incidentes es el número de reparaciones; confirmar esta relación antes de oficializarla.
13. No se calcula MTBF oficial porque el caso no define qué incidentes cuentan como fallas ni su periodo operativo por componente.
14. Los resultados deben revisarse con Finanzas, Admisiones, Vicerrectorado, Facilities, Compras, Seguridad y dueños de los servicios antes de solicitar aprobación.

### Checklist de entrega

- [ ] Resumen ejecutivo de una página con decisión/monto/riesgos/beneficios.
- [ ] Respuestas A1–A5 y B1–B4 con fórmulas visibles.
- [ ] Objetivos SMART e iniciativas con dueño, fecha, KPI y dependencia.
- [ ] Todas las partidas CAPEX/OPEX, cálculo de energía, ZBB y forecast 2026.
- [ ] Disponibilidad de cada mes y semestre; SLA; FCR mensual y ponderado; PUE; umbrales.
- [ ] Tablero de cinco KPIs con línea base, meta y tendencia.
- [ ] Supuestos, fuentes, limitaciones y declaración de uso/verificación de IA.
- [ ] Informe final de 8–10 páginas y anexos; entregar el PDF requerido por el caso además del editable Word.
- [ ] Citas consistentes y referencias según la guía APA 7 entregada en el repositorio.

## 11. Fuentes del curso utilizadas

Fuentes internas entregadas con la asignatura. Las citas en el informe deben señalar la unidad o el material pertinente y no atribuir a los documentos conclusiones que son cálculos del caso.

- Caso *Crecimiento, presupuesto e indicadores (KPIs)*. `Integradora_tres/Caso_Crecimiento_Presupuesto_KPIs.docx`.
- Unidad 1: `Estructura Organizacional y Funciones del Centro de Cómputo.pptx`; `Normativas y Buenas Prácticas en el Centro de Cómputo.pptx`; `Relación con el Desarrollo de Software y Bases de Datos.pptx`; `Tipos y Modelos de Centros de Cómputo.pptx`; `Administracion_Centro_Computo.pdf`.
- Unidad 2: `Ciberseguridad en Redes e Infraestructuras Críticas (Enfoque en Centros de Cómputo).pptx`; `Políticas de Respaldo y Recuperación ante Desastres.pptx`; `Principios de Seguridad Física y Lógica en la Protección de Sistemas.pptx`; `Seguridad en IoT e IA para Administradores de Centros de Cómputo.pptx`.
- Unidad 3: `Automatización de Procesos Administrativos en TI.pptx`; `Gestión del Recurso Humano Técnico en el Centro de Cómputo.pptx`; `Inventario, Control y Mantenimiento de Hardware y Software en la Administración de Centros de Cómputo.pptx`; `Monitoreo y Administración de Redes y Servicios en el Centro de Cómputo.pptx`.
- Unidad 4: `Análisis de Necesidades y Proyección de Crecimiento en el Centro de Cómputo.pptx`; `Elaboración de Planes Operativos y Presupuestos de TI.pptx`; `Indicadores de Gestión (KPIs) Aplicados al Centro de Cómputo.pptx`; `Tendencias Tecnológicas y su Relevancia para el Centro de Cómputo.pptx`.
- `Guía práctica Normas apa 7ma edición.pdf`.

Para las diapositivas atribuidas al docente, puede emplearse una referencia institucional del tipo: **Franco Lamilla, J. (s. f.). *[Título de la presentación]* [Diapositivas de clase, Unidad X]. Administración de Centros de Cómputo, ECOTEC.** Ajustar autor/fecha si el docente o el aula virtual proporcionan datos bibliográficos más precisos. Para el caso, citar el documento de instrucciones como material de clase sin inventar autor o fecha de publicación.
