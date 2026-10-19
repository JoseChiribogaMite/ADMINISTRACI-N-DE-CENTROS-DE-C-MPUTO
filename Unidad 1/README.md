# Unidad 1 — Estructura y Normativas del Centro de Cómputo

> **Asignatura:** Administración de Centros de Cómputo (ECOTEC)
> **Fuentes:** Estructura Organizacional y Funciones · Tipos y Modelos de Centros de Cómputo · Normativas y Buenas Prácticas · Relación con el Desarrollo de Software y Bases de Datos

Esta unidad sienta las bases del **qué** y el **cómo** de un centro de cómputo: su concepto, objetivos, roles, estructuras organizacionales, las normativas y estándares internacionales que lo rigen, las buenas prácticas operativas, y los modelos de despliegue (on-premise, cloud e híbrido).

---

## 📌 15 Temas / Conceptos Clave

1. **Concepto de Centro de Cómputo (Data Center).** Es el *espacio físico y lógico* donde se concentran, procesan y distribuyen todos los recursos de TI de una organización. No es "un cuarto lleno de servidores", sino un ecosistema complejo.

2. **Componentes del ecosistema.** Todo centro de cómputo se compone de tres pilares: **Hardware** (servidores, almacenamiento, red, respaldo), **Software** (SO, bases de datos, ERP/CRM, seguridad) y **Personal especializado** (el equipo que lo gestiona).

3. **Objetivos del centro de cómputo.** Dos grandes fines: **optimización de recursos** (uso eficiente de tecnología y personas) y **soporte a la toma de decisiones** (datos precisos y actuales para los directivos).

4. **Beneficios e importancia.** Aumento de la eficiencia, mejora de la comunicación interna, centralización de la información, garantía de disponibilidad (uptime), optimización del rendimiento y protección de los activos digitales.

5. **Roles estratégicos del equipo TI.** Administrador de Sistemas (servidores y SO), Encargado de Redes (switches/routers/firewalls), Especialista en Seguridad Informática (auditorías, ISO 27001), Soporte Técnico (usuarios finales) y el **Rol Gerencial / Jefe de Centro de Cómputo** (políticas, alineación estratégica, innovación).

6. **Funciones del centro moderno.** Habilitador de innovación, soporte para la decisión, garante de la continuidad del negocio, centro de eficiencia y reducción de costos, provisión de servicios, mantenimiento de infraestructura, soporte/asesoría y fomento de la cultura digital.

7. **Estructuras organizacionales.** Tres modelos según el tamaño de la empresa: **Funcional** (PyME, por especialidades), **por Proyectos o Unidades de Negocio** (empresa grande) y **Matricial o Híbrida** (corporaciones globales, con "dos jefes").

8. **Normativas y estándares clave.** **Uptime Institute (Tier Standard)** —certificación de confiabilidad y disponibilidad—, **ANSI/TIA-942** —diseño de infraestructura de telecomunicaciones e instalaciones— y las **normas ISO**.

9. **Niveles Tier I–IV.** Tier I: 99.671% (básico, sin redundancia); Tier II: 99.741% (componentes redundantes); Tier III: 99.982% (mantenimiento concurrente); Tier IV: 99.995% (tolerante a fallos).

10. **Normas ISO.** **ISO/IEC 27001** (SGSI, seguridad de la información y tríada CID), **ISO/IEC 20000** (gestión de servicios, certificable), **ISO 9001** (calidad) y **ISO 50001** (gestión de energía).

11. **ITIL.** Marco de trabajo (*framework*) de buenas prácticas para la Gestión de Servicios de TI (ITSM). No es una norma: enseña el **cómo**. ITIL v3 organiza el ciclo de vida en Estrategia, Diseño, Transición, Operación y Mejora Continua; ITIL 4 lo evoluciona al **Sistema de Valor del Servicio (SVS)**.

12. **Comparativa ITIL vs ISO 20000 vs ISO 27001.** ITIL = guía del "cómo" (certifica personas); ISO 20000 = norma que *demuestra* calidad del servicio (certifica organizaciones); ISO 27001 = norma que *demuestra* robustez en seguridad de la información.

13. **Buenas prácticas operativas.** Climatización (HVAC) con **pasillos fríos/calientes** y temperatura de 18–27 °C; seguridad física (control de acceso multinivel, CCTV, VESDA/Novec/FM-200); gestión de energía (**UPS**, generadores, redundancia A/B); **DCIM**, mantenimiento preventivo, documentación y etiquetado.

14. **Modelos de despliegue.** **On-premise** ("la fortaleza propia": control total, CapEx alto), **Cloud** ("el hotel de lujo": elasticidad, pago por uso, vendor lock-in) e **Híbrido** ("lo mejor de dos mundos": integración, portabilidad de cargas, *cloud bursting*). Servicios cloud: **IaaS, PaaS, SaaS**.

15. **Relación con desarrollo de software y bases de datos.** El centro provee infraestructura para el **SDLC** (capacity planning, ambientes dev/test/staging, alta disponibilidad, monitoreo), administra bases de datos (respaldo, DRP, rendimiento SSD/SAN, seguridad) e integra servicios vía **APIs, middleware, microservicios, Docker/Kubernetes** y ambientes híbridos/multinube.

---

## ❓ 20 Preguntas Clave

1. ¿Qué es un Centro de Cómputo (Data Center)?
2. ¿Cuáles son los tres componentes principales del ecosistema de un centro de cómputo?
3. ¿Cuáles son los dos grandes objetivos de un centro de cómputo?
4. ¿Qué rol es responsable de la instalación, configuración y mantenimiento de servidores y sistemas operativos?
5. ¿Quién administra la conectividad, switches, routers y firewalls?
6. ¿Qué estructura organizacional es la más común en PyMEs y se organiza por especialidades?
7. ¿Qué estructura combina la organización funcional con la de proyectos, generando "dos jefes"?
8. ¿Qué organización creó el estándar Tier para certificar confiabilidad y disponibilidad?
9. ¿Qué nivel Tier es tolerante a fallos y ofrece 99.995% de disponibilidad?
10. ¿Qué disponibilidad corresponde al Tier I (básico, sin redundancia)?
11. ¿Qué norma internacional establece los requisitos de un SGSI y protege la tríada CID?
12. ¿Qué norma es auditable y certifica el Sistema de Gestión de Servicios (SGS)?
13. ¿Qué es ITIL?
14. ¿Qué tecnologías de contenedores y orquestación son fundamentales para la integración moderna?
15. ¿Qué cubre el estándar ANSI/TIA-942?
16. ¿Qué buena práctica alinea los racks para que el aire frío y caliente no se mezclen?
17. ¿Qué sistema proporciona energía instantánea con baterías ante un corte eléctrico?
18. ¿Cuál es una característica clave del modelo on-premise?
19. ¿En qué modelo cloud el proveedor entrega una aplicación completa lista para usar?
20. ¿Qué modelo combina infraestructura local con nube pública y permite "cloud bursting"?

---

## ✅ Respuestas

1. **El espacio físico y lógico** donde se concentran, procesan y distribuyen todos los recursos de TI de una organización.
2. **Hardware, Software y Personal especializado.**
3. **Optimización de recursos** y **soporte a la toma de decisiones.**
4. **Administrador de Sistemas.**
5. **Encargado de Redes.**
6. **Estructura Funcional.**
7. **Estructura Matricial o Híbrida.**
8. **Uptime Institute.**
9. **Tier IV** (99.995%).
10. **99.671%.**
11. **ISO/IEC 27001.**
12. **ISO/IEC 20000.**
13. **Un marco de buenas prácticas (framework) para la Gestión de Servicios de TI (ITSM).**
14. **Docker y Kubernetes.**
15. **El diseño de la infraestructura de telecomunicaciones e instalaciones del centro de datos.**
16. **Pasillos fríos y calientes.**
17. **UPS (Sistema de Alimentación Ininterrumpida).**
18. **La empresa posee y controla todo el hardware, con alta inversión inicial (CapEx).**
19. **SaaS (Software como Servicio).**
20. **El modelo Híbrido.**
