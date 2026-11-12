# Unidad 4 — Planificación, presupuesto, indicadores y evolución tecnológica

**Asignatura:** Administración de Centros de Cómputo

**Material base:** las cuatro presentaciones de esta unidad, impartidas por Mgs. José Franco Lamilla, y el caso de crecimiento, presupuesto y KPIs.

**Propósito:** convertir necesidades institucionales y datos técnicos en decisiones de capacidad, proyectos, financiamiento y mejora continua.

La unidad responde a **qué se necesita, cuánto, para cuándo, a qué costo y cómo se comprobará el resultado**. Comprar tecnología no es el objetivo: el objetivo es sostener los servicios del negocio con capacidad, continuidad y costos controlados.

> **Criterio de lectura:** las explicaciones se basan en los materiales locales. Los ejercicios del caso conservan sus supuestos; otros ejemplos se identifican como didácticos. Las propuestas de metas, controles y arquitectura no equivalen a decisiones aprobadas ni a especificaciones confirmadas por un proveedor.

## 1. Materiales y mapa de la unidad

| Bloque | Archivo de la materia | Diapositivas de referencia |
|---|---|---|
| Diagnóstico y crecimiento | [Análisis de Necesidades y Proyección de Crecimiento](<Análisis de Necesidades y Proyección de Crecimiento en el Centro de Cómputo.pptx>) | 6–10: diagnóstico; 12–15: expansión; 17–19: estimación y N+1 |
| POA y presupuesto | [Elaboración de Planes Operativos y Presupuestos de TI](<Elaboración de Planes Operativos y Presupuestos de TI.pptx>) | 4–9: POA; 11–12: presupuesto; 14–15: casos |
| Indicadores | [Indicadores de Gestión (KPIs)](<Indicadores de Gestión (KPIs) Aplicados al Centro de Cómputo.pptx>) | 7–20: indicadores; 22–25: interpretación; 27: PDCA |
| Tendencias | [Tendencias Tecnológicas y su Relevancia](<Tendencias Tecnológicas y su Relevancia para el Centro de Cómputo.pptx>) | 4–17: tecnologías; 19–25: impacto, oportunidades y desafíos |
| Aplicación integradora | [Caso original de crecimiento, presupuesto y KPIs](<../Integradora_tres/Caso_Crecimiento_Presupuesto_KPIs.docx>) | Secciones 1–10: datos, actividades y supuestos |
| Desarrollo del caso | [Guía de la Integradora 3](<../Integradora_tres/readme_integradora3.md>) | Procedimientos, cálculos y limitaciones del caso |

```text
Inventario y monitoreo de la unidad 3
                  ↓
Diagnóstico actual → necesidades del negocio → proyección
                  ↓
Brechas y riesgos → objetivos SMART → proyectos del POA
                  ↓
Presupuesto → aprobación → ejecución controlada
                  ↓
KPIs → interpretación → mejora continua → nuevo diagnóstico
```

La [unidad 3](<../Unidad 3/README.md>) aporta la evidencia operativa; las unidades [1](<../Unidad 1/README.md>) y [2](<../Unidad 2/README.md>) mantienen presentes estructura, normas, seguridad y continuidad.

## 2. Diagnóstico tecnológico y proyección de crecimiento

### 2.1. Conceptos: línea base, diagnóstico y brecha

La **línea base** describe el estado medido en una fecha y periodo definidos. El diagnóstico **As-Is** examina salud, rendimiento y ciclo de vida; no es solo una lista de equipos. Una **brecha** es la diferencia entre lo que se puede ofrecer y lo que requieren los servicios.

| Pilar del diagnóstico | Qué revisar | Riesgo que ayuda a identificar |
|---|---|---|
| Espacio | Unidades U, racks y posibilidad real de instalación | No poder ubicar nuevos equipos |
| Potencia | Capacidad y carga de UPS/PDU, distribución y redundancia | Sobrecarga o pérdida de alimentación |
| Enfriamiento | Carga térmica, CRAC, temperatura y puntos calientes | Sobrecalentamiento y fallas simultáneas |
| Cómputo y almacenamiento | CPU, RAM, IOPS, latencia, espacio y conectividad | Saturación, lentitud y falta de capacidad |
| Ciclo de vida | Garantía, repuestos, versiones y soporte | Obsolescencia y dificultad de recuperación |

**EoL** señala fin de vida según la política del fabricante; **EoS**, fin de soporte. Las fechas deben verificarse: una garantía vencida no demuestra automáticamente que el producto esté sin soporte.

### 2.2. Parte técnica: capacidad instalada, utilizable y resiliente

No confundir:

- **Instalada:** recursos nominales adquiridos.
- **Utilizable:** recursos realmente disponibles después de reservas, protección y limitaciones.
- **Demanda:** carga medida o proyectada, incluyendo picos.
- **Capacidad tras una falla:** recursos que siguen disponibles bajo el escenario evaluado.
- **Margen o headroom:** reserva para crecimiento, variaciones y operación segura.

**N+1** significa disponer de un elemento adicional a los N necesarios. No basta con contar equipos: deben existir configuración, distribución y capacidad para sostener el servicio después de una falla.

Para elementos homogéneos que pueden sustituirse y compartir la carga:

```text
Capacidad restante = (número de elementos − 1) × capacidad por elemento
Utilización tras falla = demanda / capacidad restante × 100
Capacidad requerida con margen = demanda / fracción máxima de uso
```

La presentación propone operación normal al **70–80% de la capacidad total** como orientación. El **caso integrador exige ≤75% de la capacidad que queda después de una falla**. Son criterios distintos; especificar siempre el denominador.

No aplicar la fórmula mecánicamente a un SAN: hacen falta datos de discos, controladoras, protección y réplicas. Tampoco sumar UPS sin verificar su arquitectura eléctrica ni suponer que un rack adicional vuelve redundante cualquier distribución de equipos.

### 2.3. Proyección por tendencia y por necesidades del negocio

**Tendencia lineal:**

`Demanda futura = uso actual + crecimiento por periodo × número de periodos`

**Modelo por negocio:**

`Demanda adicional = nuevas unidades de negocio × consumo por unidad`

La estimación puede combinar ambos métodos, pero se debe comprobar que no contabilicen dos veces la misma demanda. Mantener unidades consistentes y aclarar si un crecimiento de CPU representa **puntos porcentuales** o un incremento relativo.

**Ejemplo didáctico:** pasar de 58% a 76% implica **18 puntos porcentuales**, no un aumento relativo del 18%. El incremento relativo es `18/58 × 100 = 31,03%`.

### 2.4. Escalamiento y hoja de ruta

| Alternativa | Cómo crece | Condición o limitación |
|---|---|---|
| Vertical, scale-up | Añadir CPU, RAM o discos a un equipo | Límite físico, costo y posible punto único de falla |
| Horizontal, scale-out | Añadir nodos y distribuir carga | Aplicación compatible, coordinación y red suficiente |
| HCI | Integrar cómputo y almacenamiento en nodos | Verificar capacidad efectiva, licencias y tolerancia a fallas |
| Red 10/25 GbE | Aumentar capacidad de conectividad | Revisar puertos, transceptores, cableado y extremos |
| All-Flash | Usar almacenamiento SSD para mejorar E/S | Dimensionar capacidad, latencia, endurance y costo |

La hoja de ruta o **roadmap** establece prioridades, dependencias, hitos y renovación por etapas. La compra debe aprobarse **antes** del agotamiento del margen, considerando contratación, entrega, instalación, migración y pruebas.

### 2.5. Interpretación lógica

**Situación:** sobra espacio de rack, pero una falla de refrigeración deja capacidad térmica insuficiente.

**Razonamiento:** espacio libre no significa capacidad para instalar servidores. Cada equipo también requiere potencia, refrigeración, conectividad y soporte.

**Decisión:** resolver primero la restricción que compromete la continuidad y diseñar una expansión equilibrada. Comprar cómputo sin revisar energía y enfriamiento puede agravar el riesgo.

## 3. Plan operativo anual y presupuesto de TI

### 3.1. Conceptos: PETI, POA y objetivos SMART

El **PETI** es el Plan Estratégico de TI, con horizonte de varios años. El **POA** traduce su primer año en objetivos, iniciativas, responsables, recursos, fechas e indicadores.

La metodología de las diapositivas sigue esta secuencia:

1. Revisar PETI, necesidades de otras áreas, FODA y desempeño anterior.
2. Definir objetivos **SMART**: específicos, medibles, alcanzables, relevantes y con plazo.
3. Identificar proyectos e iniciativas.
4. Asignar personas, tecnología, cronograma, hitos y dependencias.
5. Definir indicadores y presentar el plan para aprobación.

**Ejemplo didáctico propuesto:** “Reducir el MTTR de los incidentes críticos de 3,5 a 2 horas antes del 30 de septiembre de 2027 mediante procedimientos probados, capacitación y escalamiento, manteniendo una tasa de reapertura no superior a la línea base”.

Es específico, medible y tiene fecha. Para llamarlo **alcanzable**, todavía debe comprobarse que existen recursos y que el diagnóstico respalda la reducción. La redacción SMART no sustituye el análisis de viabilidad.

### 3.2. Parte técnica: estructura mínima del POA

| Necesidad | Proyecto o iniciativa | Responsable por rol | Dependencia | Evidencia de aceptación |
|---|---|---|---|---|
| Continuidad térmica | Ampliar y probar refrigeración | Facilities y dirección | Diseño y presupuesto aprobados | Prueba de capacidad ante falla |
| Capacidad futura | Migración y expansión del clúster | SysAdmin | Energía, red y enfriamiento preparados | Carga validada y recuperación probada |
| Mejor soporte | Capacitación y procedimientos | Responsable de soporte | Diagnóstico de competencias | Mejora de FCR sin elevar reaperturas |
| Costos controlados | Revisión de contratos y consumo | Dirección TI y Finanzas | Inventario y contratos completos | Variaciones y ahorros documentados |

Una dependencia debe reflejar una condición real: capacitar y preparar procedimientos puede ejecutarse en paralelo con la compra, pero la migración necesita infraestructura lista y validada.

### 3.3. CAPEX, OPEX y metodologías

| Concepto | Qué representa | Ejemplos |
|---|---|---|
| CAPEX | Inversión en activos con beneficios durante varios periodos | Servidores, switches, UPS y climatización |
| OPEX | Gasto operativo y servicios recurrentes | Energía, soporte, suscripciones y capacitación |
| Incremental | Ajustar el presupuesto previo por un porcentaje | Operación relativamente estable |
| Base cero, ZBB | Justificar cada gasto desde cero | Revisar contratos heredados y prioridades |
| Basado en actividades, ABC | Vincular costos a actividades o servicios | Costear soporte, respaldo o matrícula |

**Pago único no significa automáticamente CAPEX:** la clasificación depende de la naturaleza del gasto y de la política contable. Una suscripción suele ser OPEX; una licencia perpetua o ciertos costos de implantación pueden exigir evaluación de Finanzas.

El presupuesto debe incluir tanto el **POA** como la operación existente: personal, energía, mantenimiento, licencias y servicios. No asumir que una tabla de cotizaciones representa el costo total de operar el centro.

Como complemento de análisis, comparar el **TCO**, costo total de propiedad, durante un horizonte común: compra, operación, soporte, capacitación, migración y salida. La nube traslada parte de la inversión a consumo operativo, pero no garantiza ahorro por sí sola.

### 3.4. Control financiero y razonamiento

```text
Variación monetaria = gasto real − presupuesto comparable
Variación porcentual = variación / presupuesto comparable × 100
Proyección de cierre = ejecutado + estimación del gasto restante
```

Comparar gasto real con presupuesto **del mismo periodo y alcance**. Una proyección lineal es orientativa: las compras grandes, pagos anticipados y estacionalidad pueden alterar el ritmo.

**Ejemplo de las diapositivas:** una factura IaaS de USD 18.000 frente a USD 12.000 previstos implica:

`Variación = 18.000 − 12.000 = USD 6.000; variación porcentual = 50%`

**Interpretación:** revisar recursos ociosos, dimensionamiento, etiquetas, almacenamiento y transferencias. El autoapagado propuesto en clase debe aplicarse a recursos elegibles; no detener producción crítica indiscriminadamente.

**ZBB:** si un contrato deja de aportar valor tras una migración validada, puede eliminarse o renegociarse. El ahorro depende de fechas y condiciones contractuales. No financiar otro proyecto con un ahorro que todavía no puede materializarse.

Los gastos no previstos requieren control de cambios: causa, impacto, alternativa de financiamiento, aprobación y actualización del plan. No ocultar un sobrecosto moviéndolo entre partidas sin autorización.

## 4. KPIs e interpretación de resultados

### 4.1. Conceptos: métrica, KPI y línea base

Una **métrica** es una medición. Un **KPI** es una métrica clave relacionada con un objetivo y una decisión. Medir CPU es útil; convertirla en indicador de capacidad requiere alcance, línea base, umbral y acción.

Cada indicador debe tener definición, fórmula, unidad, fuente, periodo, responsable, meta y criterio de alerta. Una cifra sin esos elementos puede ser ambigua.

### 4.2. Parte técnica: fórmulas y precauciones

| Indicador | Fórmula o medición | Interpretación |
|---|---|---|
| Disponibilidad | `(tiempo total − caída) / tiempo total × 100` | Comparar con el SLA del servicio y periodo |
| MTBF | `tiempo total de operación / número de fallas` | Mayor valor suele indicar mayor confiabilidad |
| MTTR | `tiempo total de reparación / número de reparaciones` | Menor valor suele indicar recuperación más rápida |
| PUE | `energía total de la instalación / energía de TI` | Menor valor indica menor sobrecarga energética |
| CUE | `emisiones atribuibles a la operación / energía de TI` | Expresar, por ejemplo, en kg CO₂e/kWh de TI |
| Utilización | `recurso utilizado / capacidad de referencia × 100` | Interpretar según picos, reservas y arquitectura |
| FCR | `tickets resueltos en primer contacto / tickets elegibles × 100` | Calidad de la atención inicial |
| Cumplimiento SLA | `casos que cumplen / casos evaluados × 100` | Requiere definir qué compromiso y universo se evalúan |
| Latencia | Tiempo de respuesta o RTT, según alcance | Identificar si corresponde a red o aplicación |

**Precauciones importantes:**

- MTBF y MTTR requieren fallas/reparaciones del mismo sistema y criterios consistentes. No sustituir fallas de un componente por todos los incidentes del centro.
- Si no hay fallas, reparaciones o tickets elegibles, reportar que la razón no es calculable en ese periodo; no inventar ceros.
- Disponibilidad de 99,95% y cumplimiento de SLA de 99,95% no son la misma medición.
- PUE es adimensional; 1,8 significa 0,8 unidades de energía de soporte por cada unidad de TI, no “80% de toda la energía desperdiciada”.
- CUE mide emisiones por energía de TI. Un valor cero dentro de un alcance no demuestra neutralidad de todo el ciclo de vida.
- CPU baja puede sugerir sobreaprovisionamiento, pero también reserva de alta disponibilidad. Revisar arquitectura antes de retirar recursos.

Las diapositivas explican PUE mediante energía; el caso lo mide con **potencia de la sala**. Una razón de potencias simultáneas describe un instante o promedio de medición, mientras que una razón de energías integra un periodo.

Para varios periodos:

`PUE agregado = suma de energía total / suma de energía TI`

El promedio aritmético de PUE mensuales no necesariamente equivale al PUE agregado. Lo mismo ocurre con FCR y disponibilidad: sumar numeradores y denominadores, no promediar porcentajes sin considerar sus pesos.

### 4.3. Interpretación lógica: del número a la decisión

| Observación | Hipótesis que investigar | Verificación o acción |
|---|---|---|
| Disponibilidad baja y MTTR sube | Recuperación lenta | Revisar repuestos, procedimientos y escalamiento |
| Disponibilidad baja y fallas aumentan | Menor confiabilidad | Analizar recurrencia, cambios y ciclo de vida |
| Latencia y utilización de red suben | Congestión | Correlacionar flujos, colas y horarios |
| FCR baja y reaperturas suben | Problemas más complejos o diagnóstico insuficiente | Revisar clasificación, conocimiento y capacitación |
| PUE aumenta | Mayor consumo de soporte o menor carga TI | Revisar clima, refrigeración y mediciones de energía |

Una tendencia cuenta más que un dato aislado, pero **correlación no significa causalidad**. Las diapositivas relacionan PUE con estaciones; para afirmar que el calor explica un cambio concreto hacen falta datos ambientales y de carga.

Los umbrales deben responder al SLA y al riesgo. Para métricas de consumo, un valor alto suele ser peor; para disponibilidad o FCR, suele ser peor un valor bajo. Documentar esa dirección y no copiar alertas sin contexto.

### 4.4. Mejora continua: PDCA

**Planificar:** detectar una brecha, investigar causas, fijar meta y diseñar una acción.

**Hacer:** ejecutar el cambio controlado.

**Verificar:** medir con las mismas definiciones y un periodo comparable.

**Actuar:** estandarizar si funciona o ajustar y repetir.

**Ejemplo de las diapositivas:** PUE inicial 2,0; meta 1,7; después de contención de pasillo frío se observa 1,72.

**Interpretación:** hubo mejora, pero no se alcanzó exactamente la meta. Revisar condiciones de comparación y ajustes; no declarar éxito total solo porque el indicador bajó. La referencia de PUE 1,5 de la presentación es parte del ejemplo, no un promedio universal verificado para cualquier centro.

## 5. Tendencias tecnológicas y criterio de adopción

### 5.1. Qué aportan y qué requieren

| Tendencia | Concepto y aplicación | Exigencia o riesgo |
|---|---|---|
| IA / AIOps | Analizar telemetría, detectar anomalías y apoyar mantenimiento predictivo | Calidad de datos, supervisión, falsos positivos y seguridad |
| DCIM | Gestionar infraestructura física: energía, espacio, refrigeración y conexiones | Inventario y sensores fiables, integración y procedimientos |
| Big Data | Procesar grandes volúmenes y diversidad de datos | Ingesta, capacidad, gobernanza y protección escalables |
| SDS / objetos | Gestionar almacenamiento por software y escalar datos no estructurados | Rendimiento, consistencia, costos y compatibilidad |
| ILM | Mover o conservar datos según su ciclo de vida | Retención, privacidad, recuperación y frecuencia de acceso |
| Virtualización | Ejecutar VM con sistemas operativos invitados sobre un hipervisor | Capacidad del host, licencias y continuidad |
| Contenedores / Kubernetes | Empaquetar aplicaciones y orquestar ejecución | Seguridad, redes, persistencia y conocimiento especializado |
| SDDC / SDN | Gestionar cómputo, almacenamiento y red mediante software y políticas | Complejidad de integración y control de cambios |
| IoT / edge | Capturar datos y procesarlos cerca de su origen | Seguridad física/lógica, conectividad y operación remota |
| Green IT / alta densidad | Mejorar eficiencia y adaptar potencia/refrigeración | Inversión, medición y diseño especializado |

Como complemento técnico, VM y contenedor no son equivalentes: una VM tiene su propio sistema operativo invitado; los contenedores normalmente comparten el kernel del entorno donde se ejecutan, que puede ser una VM.

“Datos calientes” son los de acceso frecuente; “fríos”, los poco consultados. Pasarlos a almacenamiento barato puede reducir costos, pero recuperar un archivo debe seguir cumpliendo el tiempo requerido por el servicio.

### 5.2. Interpretación lógica y límites

**Consolidar servidores reduce cantidad de equipos, pero puede elevar kW por rack.** Menos espacio ocupado no implica menos calor local. Una arquitectura de alta densidad exige revisar distribución eléctrica, flujo de aire y, si corresponde, refrigeración especializada.

**AIOps no elimina supervisión:** las predicciones pueden equivocarse y sus acciones deben respetar límites, permisos y reversa. La automatización “lights-out” es una aspiración para tareas rutinarias, no ausencia de responsabilidad o mantenimiento humano.

**Big Data no invalida todos los respaldos tradicionales:** obliga a comprobar que capacidad, ventana de copia y restauración satisfacen RPO/RTO. La tecnología se elige por esa necesidad, no por una etiqueta.

**La eficiencia no reemplaza la disponibilidad:** aunque la presentación destaca PUE, agilidad y predicción, el cumplimiento del servicio continúa siendo obligatorio.

Antes de adoptar una tendencia, responder: **qué brecha resuelve, qué evidencia lo demuestra, qué costo total implica, quién la operará, cómo se protege y con qué KPI se validará**.

## 6. Prácticas resueltas con archivos de la materia

Los siguientes datos proceden del **caso ficticio URA**. Su línea base es 30/06/2026; utiliza meses de 30 días, un semestre de 180 días y proyección de almacenamiento de 18 meses hasta 31/12/2027.

### Práctica 1 — Diagnóstico N+1

| Recurso | Cálculo tras una falla | Uso resultante | Lectura |
|---|---|---|---|
| Cómputo medio | `58% × 3 = 1,74 hosts; 1,74/2 × 100` | 87% | Supera el margen del 75% |
| Cómputo pico | `84% × 3 = 2,52 hosts; 2,52/2 × 100` | 126% | No sostiene el pico sin degradación |
| UPS | `85/120 × 100` | 70,83% | Cumple margen actual bajo la configuración asumida por el caso |
| Refrigeración | `85/50 × 100` | 170% | Capacidad insuficiente tras perder una unidad |
| SAN utilizable actual | `31/40 × 100` | 77,5% | Sin margen del 75%; N+1 no demostrable sin arquitectura |
| Espacio instalado | `210/252 × 100` | 83,33% | Supera el 75% incluso sin retirar un rack |

**Ambigüedad del espacio:** la tabla del caso muestra 252 U, pero su instrucción general pide retirar un elemento. Si se interpreta que se pierde un rack completo, quedarían `5 × 42 = 210 U`, con ocupación del 100%. Esto cuantifica espacio remanente, no demuestra que los servicios de ese rack sobrevivan. Explicitar la interpretación.

**Trabajo:** redactar un hallazgo por pilar y priorizar acciones. **Respuesta esperada:** refrigeración es urgente porque una falla deja solo 50 kW para 85 kW térmicos; el espacio también incumple, pero no resuelve esa restricción.

### Práctica 2 — Proyectar almacenamiento y cómputo

Convención decimal para este ejercicio: `1 TB = 1.000 GB`.

```text
Crecimiento base = 2 TB/mes × 18 meses = 36 TB
Uso futuro base = 31 + 36 = 67 TB
LMS adicional = 6 × 80 GB = 480 GB = 0,48 TB
Finanzas adicional = 4 TB
Demanda futura total = 67 + 0,48 + 4 = 71,48 TB
Capacidad utilizable requerida = 71,48/0,75 = 95,31 TB
Capacidad adicional sobre 40 TB = 95,31 − 40 = 55,31 TB
```

Los 95,31 TB no son capacidad bruta ni prueba de N+1 del SAN. El fabricante debe confirmar capacidad efectiva después de protección y comportamiento ante falla.

```text
CPU adicional = 6 × 3 = 18 puntos porcentuales del clúster actual
Promedio proyectado = 58% + 18 pp = 76%
Pico proyectado = 84% + 18 pp = 102% del clúster actual
Demanda pico equivalente = 3 × 1,02 = 3,06 hosts actuales
```

Con hosts equivalentes y distribución viable, sostener estrictamente ese pico tras una falla requiere **5 hosts totales**: quedan cuatro; con cuatro totales quedarían tres, insuficientes. Si además se exige uso pico ≤75% después de la falla:

`3,06/(H − 1) ≤ 0,75 → H ≥ 5,08 → 6 hosts totales`

Para carga normal proyectada, cinco totales dejan `2,28/4 × 100 = 57%`. Diferenciar supervivencia del pico, margen normal y margen del pico; no trasladar estas cuentas a nodos HCI de especificaciones desconocidas.

```text
Carga TI adicional = 6 × 1,5 = 9 kW
Carga TI futura = 85 + 9 = 94 kW
Uso de una UPS restante = 94/120 × 100 = 78,33%
```

**Interpretación:** la UPS cumple hoy pero deja de cumplir el margen del caso tras el crecimiento. Además, el almacenamiento ya supera 75% en la línea base; sin expansión se llena en `(40−31)/2 = 4,5 meses`, aproximadamente a mediados de noviembre de 2026. La compra no puede esperar al cierre de 2027.

**Entregable:** cálculos, supuestos de equivalencia, fecha de aprobación propuesta y tiempos de implementación que deben verificarse.

### Práctica 3 — Presupuesto, energía y control

Clasificación didáctica de las cotizaciones del caso:

| Grupo | Partidas | Total USD |
|---|---|---:|
| CAPEX | HCI 165.000 + red 38.000 + CRAC 84.000 + UPS 45.000 | 332.000 |
| OPEX antes de energía | Renovación 60.000 + consultoría 30.000 + capacitación 9.000 + legacy 48.000 | 147.000 |
| Subtotal | Las ocho partidas | 479.000 |

La consultoría se trata aquí como OPEX de servicio y la renovación como gasto operativo; confirmar cualquier tratamiento diferente con Finanzas.

El caso fija 9 kW adicionales, 8.760 horas/año, PUE 1,80 y tarifa USD 0,11/kWh:

```text
Energía adicional = 9 × 8.760 × 1,80 = 141.912 kWh/año
Costo adicional = 141.912 × 0,11 = USD 15.610,32/año
Total de partidas = 479.000 + 15.610,32 = USD 494.610,32
Margen frente al tope = 520.000 − 494.610,32 = USD 25.389,68
```

Si el contrato legacy puede eliminarse durante todo el año después de una migración aceptada, el ahorro máximo es USD 48.000/año y el escenario baja a **USD 446.610,32**. No dar por garantizada esa cancelación ni olvidar gastos de operación no incluidos en las cotizaciones.

Para el presupuesto 2026, el caso aporta USD 270.000 ejecutados en seis meses frente a USD 480.000 anuales:

```text
Ejecución = 270.000/480.000 × 100 = 56,25%
Forecast lineal = 270.000 × 12/6 = USD 540.000
Variación prevista = 540.000 − 480.000 = USD 60.000 = 12,5%
```

**Trabajo:** proponer una causa posible y una acción formal. **Comprobación:** el sobrecosto es una proyección, no un gasto confirmado; investigar calendario de compras y compromisos antes de recortar iniciativas críticas.

### Práctica 4 — Tablero con datos del semestre

Aplicar las fórmulas a los valores del caso:

| Mes | Caída, min | Disponibilidad | FCR | PUE informado |
|---|---:|---:|---:|---:|
| Enero | 35 | 99,9190% | 70,34% | 1,78 |
| Febrero | 20 | 99,9537% | 71,56% | 1,76 |
| Marzo | 95 | 99,7801% | 63,71% | 1,74 |
| Abril | 180 | 99,5833% | 62,81% | 1,80 |
| Mayo | 310 | 99,2824% | 61,54% | 1,82 |
| Junio | 150 | 99,6528% | 62,61% | 1,83 |

```text
Caída semestral = 35 + 20 + 95 + 180 + 310 + 150 = 790 minutos
Disponibilidad = (259.200 − 790)/259.200 × 100 = 99,6952%
Caída permitida al 99,9% = 259.200 × 0,001 = 259,2 minutos
Exceso de caída = 790 − 259,2 = 530,8 minutos
FCR semestral = 4.680/7.170 × 100 = 65,27%
PUE promedio aritmético = 10,73/6 = 1,7883
```

Enero y febrero cumplen el SLA 99,9%; el resto no. El semestre tampoco cumple. FCR cae después de febrero, con una recuperación leve en junio; PUE baja hasta marzo y aumenta después. El caso no proporciona datos de clima suficientes para demostrar una causa térmica.

Para MTTR agregado, si las cantidades de incidentes corresponden a las reparaciones usadas para medirlo:

`MTTR semestral ≈ suma(MTTR mensual × incidentes) / suma(incidentes) = 110,2/34 = 3,2412 h`

La aproximación usa promedios mensuales redondeados; si las poblaciones no coinciden, se necesitan los registros de reparación. No calcular MTBF del portal con todos los incidentes sin confirmar que representan fallas de ese servicio.

**Trabajo:** diseñar un tablero con cinco KPIs, fuente, responsable, línea base, meta y acción. Para la meta 2027 de disponibilidad 99,95%, un mes convencional de 30 días permite `43.200 × 0,0005 = 21,6 minutos` de caída.

### Práctica 5 — Umbrales y ciclo de mejora

**Propuesta didáctica para discutir, no política aprobada:**

| KPI | Verde | Amarillo | Rojo | Criterio |
|---|---|---|---|---|
| Disponibilidad mensual 2027 | ≥99,95% | ≥99,9% y <99,95% | <99,9% | Amarillo ya incumple la meta nueva; requiere acción |
| FCR | ≥70% | ≥65% y <70% | <65% | Referencia al comienzo del semestre y deterioro posterior |
| PUE | ≤1,78 | >1,78 y ≤1,82 | >1,82 | Referencia provisional; ajustar por clima y carga |
| CPU normal sobre capacidad tras falla | ≤70% | >70% y ≤75% | >75% | Aviso antes de incumplir el margen del caso |

Los KPIs mensuales son para seguimiento; las alertas operativas necesitan ventanas más cortas. Acordar además cuándo actuar antes de consumir el presupuesto de caída permitido.

**Trabajo:** elegir una brecha y escribir un PDCA con responsable, fecha y medición comparable. Por ejemplo, mejorar FCR con capacitación y una base de conocimiento, comprobando también reaperturas para evitar cierres superficiales.

### Práctica 6 — Evaluar una tendencia sin comprar por moda

Comparar dos opciones para una brecha del caso: ampliar infraestructura local o adoptar un servicio híbrido.

**Entregable:** matriz con capacidad, continuidad, seguridad, costo a tres años, integración, capacitación, migración, dependencia del proveedor y salida. Cuando falten datos, indicar qué cotización, medición o prueba hace falta.

**Comprobación:** recomendar la opción que satisface requisitos verificables. No asumir que tres nodos HCI cotizados aportan 100 TB utilizables o que la nube cumple automáticamente el SLA institucional.

## 7. Preguntas de comprensión con respuestas

| Pregunta | Respuesta razonada |
|---|---|
| ¿En qué se diferencia diagnóstico de inventario? | Añade salud, rendimiento, soporte, riesgos y prioridades. |
| ¿Qué significa N+1? | Un elemento adicional a los necesarios, capaz de sostener el servicio ante la falla evaluada. |
| ¿Por qué no dimensionar solo con promedio? | Puede ocultar picos y carga redistribuida tras una falla. |
| ¿75% de capacidad total equivale a 75% de capacidad tras falla? | No; cambian el denominador y la reserva efectiva. |
| ¿Qué une al PETI con el trabajo anual? | El POA con objetivos, iniciativas, responsables, presupuesto e indicadores. |
| ¿Un objetivo SMART está automáticamente garantizado? | No; debe demostrarse su viabilidad técnica y financiera. |
| ¿Una compra de pago único siempre es CAPEX? | No; depende del gasto y del tratamiento contable. |
| ¿Qué aporta ZBB frente al incremental? | Obliga a justificar el valor de cada gasto, incluso los heredados. |
| ¿PUE menor demuestra menor consumo absoluto? | No; también se necesitan energías totales y carga comparable. |
| ¿FCR alto basta para demostrar buen soporte? | No; revisar reaperturas, calidad y complejidad. |
| ¿Promediar porcentajes mensuales siempre es correcto? | No; agregar numeradores y denominadores o ponderar adecuadamente. |
| ¿Una correlación demuestra causa? | No; hay que verificar hipótesis con más evidencia. |
| ¿Qué cambia con edge computing? | Se distribuye procesamiento y también responsabilidad operativa y de seguridad. |
| ¿Cuándo termina PDCA? | La mejora se revisa continuamente; se estandariza o se ajusta y se repite. |

## 8. Lista de comprobación para sustentar una decisión

- Diagnóstico fechado con los cinco pilares y servicios afectados.
- Fórmulas reproducibles, unidades consistentes y datos separados de supuestos.
- Proyección con tendencia, negocio, picos, margen y escenario de falla.
- Objetivos SMART ligados al PETI y a necesidades institucionales.
- Iniciativas con responsables, dependencias, capacitación y aceptación.
- Presupuesto con CAPEX/OPEX, operación existente, energía y contratos.
- Control de variaciones, forecast y aprobación de cambios.
- KPIs con población, periodo, fuente, meta, umbral e interpretación.
- Acción PDCA cuya mejora pueda verificarse.
- Recomendación tecnológica basada en brechas y costos, no en promesas.

**Criterio final:** una buena sustentación conecta evidencia → riesgo → alternativa → costo → resultado esperado. Si falta información, identifica la validación necesaria en lugar de convertir una suposición en un hecho.
