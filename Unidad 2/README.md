# Unidad 2 — Seguridad y Continuidad de Operaciones

> **Asignatura:** Administración de Centros de Cómputo (ECOTEC)
> **Fuentes:** Ciberseguridad en Redes e Infraestructuras Críticas · Principios de Seguridad Física y Lógica · Políticas de Respaldo y Recuperación ante Desastres · Seguridad en IoT e IA · Caso de Estudio (on-premise/cloud/híbrido)

Esta unidad se enfoca en **proteger** el centro de cómputo y **garantizar que siga operando** ante cualquier incidente: amenazas físicas y lógicas, controles de acceso, estrategias de respaldo, planes de continuidad y recuperación ante desastres, y los nuevos riesgos de IoT e Inteligencia Artificial.

---

## 📌 15 Temas / Conceptos Clave

1. **Objetivo de la ciberseguridad: la tríada CID.** Proteger la **Confidencialidad** (solo personal autorizado accede), la **Integridad** (información precisa y no alterada) y la **Disponibilidad** (accesible cuando se necesita).

2. **Amenazas físicas.** Acceso no autorizado (credenciales falsas, robo de discos), **sabotaje interno** (administradores descontentos, borrado de backups, apagado de climatización) y **fallas ambientales/eléctricas** (sobrecalentamiento, cortes sin UPS ni generador).

3. **Amenazas lógicas.** **Ransomware** dirigido a hipervisores (VMware/Hyper-V) y SAN; **ataques a la cadena de suministro** (actualización comprometida); **DDoS** (saturar ancho de banda); y **vulnerabilidades no parcheadas** (la causa más común de brechas).

4. **Control de acceso: autenticación vs autorización.** La **autenticación** verifica la identidad (contraseña, biometría); la **autorización** determina los recursos a los que el usuario puede acceder una vez autenticado. Existen controles **físicos** (instalaciones) y **lógicos** (datos y recursos electrónicos).

5. **Medidas de seguridad para hardware y software.** Hardware: **cifrado de datos**, blindaje físico, control de acceso a dispositivos. Software: **actualizaciones y parches**, antivirus/antimalware, firewalls y sistemas de detección de intrusos (IDS).

6. **Herramientas de mitigación en el datacenter.** Jaulas (*caging*), control de acceso físico multinivel (biometría, mantraps), **PAM / bóveda digital** (gestión de acceso privilegiado), **microsegmentación y firewalls internos**, y **hardening** de sistemas.

7. **Protección perimetral y Zero Trust.** Perímetro físico (campus, guardias), de red (**NGFW, IPS**), interno (**Zero Trust** y red de gestión aislada *out-of-band*) y humano/procesos (gestión de cambios, DRP, capacitación). **Zero Trust** = "nunca confíes, siempre verifica".

8. **Estrategias de backup.** **Completo** (copia todo, restauración rápida), **incremental** (solo cambios desde el último backup) y **diferencial** (cambios desde el último completo). El incremental y el diferencial necesitan el completo inicial.

9. **Frecuencia y almacenamiento de respaldos.** Frecuencia **diaria** (datos recientes), **semanal** (datos menos críticos) y **mensual** (archivo/auditoría). Almacenamiento **local** (rápido, riesgo físico), **remoto** (seguro ante desastres) y **nube** (flexible, depende de internet).

10. **Plan de Continuidad de Negocio (BCP).** Incluye la **evaluación de riesgos** (identificación de amenazas → análisis de impacto → estrategias de mitigación), el **desarrollo del plan** (comunicación, roles, componentes) y las **pruebas** (simulacros, revisión periódica, ajustes).

11. **Recuperación ante desastres: RTO, RPO, sitios y RAID.** **RTO** = tiempo objetivo de recuperación; **RPO** = punto objetivo de recuperación (datos tolerados a perder). Sitios **Hot/Warm/Cold** según rapidez de activación. **RAID y clustering** aportan redundancia y alta disponibilidad.

12. **Procesos y herramientas de recuperación de datos.** Restauración de sistemas, **validación de datos** y **pruebas de integridad**. Herramientas: software de recuperación, almacenamiento en nube y servicios especializados.

13. **Riesgos del IoT en el datacenter.** Vectores de **ataque físico-digital** (sensor comprometido), **contraseñas por defecto** (admin/admin en PDU y cámaras IP), **punto ciego en parches** (firmware desactualizado) y **pivotes para movimiento lateral**.

14. **Vulnerabilidades de la IA en el datacenter.** **Ataques de evasión** contra SIEM, **envenenamiento de datos** en mantenimiento predictivo (AIOps) y **manipulación de la optimización de cargas** de trabajo.

15. **Controles y auditorías para IoT e IA.** Para IoT: **segmentación extrema** (VLAN aislada), **hardening** (cambio de contraseñas, firmware, servicios) e inventario/ciclo de vida. Para IA: auditoría de **caja negra** (black-box), auditoría de la **cadena de suministro de datos** (hashes) y monitoreo del **drift** del modelo.

---

## ❓ 20 Preguntas Clave

1. ¿Cuál es el objetivo principal de la ciberseguridad en un centro de cómputo?
2. ¿Cuál de las siguientes es una amenaza FÍSICA para un centro de cómputo?
3. ¿A qué apuntan directamente los ataques modernos de ransomware en un datacenter?
4. ¿Qué es un ataque a la cadena de suministro?
5. ¿Qué busca un ataque DDoS?
6. ¿Cuál es la diferencia entre autenticación y autorización?
7. ¿Qué medida de seguridad de HARDWARE convierte la información en un formato ilegible sin la clave?
8. ¿Qué medida de SOFTWARE es esencial para corregir vulnerabilidades?
9. ¿Qué herramienta centraliza y protege las cuentas de administrador (bóveda digital)?
10. ¿Qué técnica divide la red para prevenir movimientos laterales de atacantes?
11. ¿Qué principio afirma "nunca confíes, siempre verifica"?
12. ¿Qué tipo de backup copia solo los cambios desde el último backup?
13. ¿Qué tipo de backup guarda todos los cambios desde el último backup completo?
14. ¿Qué característica describe el almacenamiento de respaldos en la nube?
15. ¿Cuáles son los pasos de la evaluación de riesgos en un BCP?
16. ¿Qué significa RTO en un plan de recuperación ante desastres?
17. ¿Cuál es la diferencia entre los sitios Hot, Warm y Cold?
18. ¿Para qué se usan RAID y clustering en la continuidad?
19. ¿Por qué las contraseñas por defecto (admin/admin) en PDUs y cámaras IP son un riesgo crítico?
20. ¿Qué vulnerabilidad de IA permite inyectar logs falsos para engañar al mantenimiento predictivo?

---

## ✅ Respuestas

1. **Garantizar la confidencialidad, integridad y disponibilidad** de la información (tríada CID).
2. **El sabotaje interno** (borrado de backups, apagado de climatización) y el acceso no autorizado.
3. **A los hipervisores (VMware, Hyper-V) y cabinas de almacenamiento (SAN).**
4. **Comprometer una actualización de un software de confianza** para instalar una puerta trasera.
5. **Saturar el ancho de banda y los firewalls** hasta que los servicios legítimos sean inaccesibles.
6. **La autenticación verifica la identidad; la autorización determina los recursos accesibles.**
7. **Cifrado de datos.**
8. **Actualizaciones y parches.**
9. **PAM (Gestión de Acceso Privilegiado) / bóveda digital.**
10. **Microsegmentación y firewalls internos.**
11. **Confianza Cero (Zero Trust).**
12. **Backup incremental.**
13. **Backup diferencial.**
14. **Flexible y escalable, accesible desde cualquier lugar, pero depende de una buena conexión.**
15. **Identificación de amenazas → análisis de impacto → estrategias de mitigación.**
16. **El tiempo objetivo para recuperar la operación tras una interrupción** (Recovery Time Objective).
17. **Hot = activo en minutos; Warm = requiere aprovisionamiento parcial; Cold = solo instalaciones, tarda más.**
18. **Para proporcionar redundancia y alta disponibilidad** de datos y servicios.
19. **Porque un atacante puede cortar remotamente la energía o controlar infraestructura crítica.**
20. **Envenenamiento de datos.**
