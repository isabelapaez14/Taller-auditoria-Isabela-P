# Taller: Matriz inicial de riesgos de sistemas

**Auditoría de Sistemas (ET0114) · Sesión 7 · Matriz de análisis de riesgos**
**Docente:** Juan Duque

**Integrante:** Isabela Páez Lopez

**Caso:** Prointimo S.A.S. (mismo caso del primer taller; no hubo cambio de caso).

---

## 1. Contexto actualizado

Prointimo S.A.S. es una empresa textil y de confección que opera con dos sistemas ERP y las aplicaciones internas APK y Planning, alojados en servidores administrados por el área de TI. Esta entrega se enfoca en la **disponibilidad e integridad de la información de los ERP, APK y Planning**, y en los procesos que la sostienen: copias de seguridad, gestión de accesos y control de cambios. La preocupación principal es que los respaldos no se ejecutan con la frecuencia recomendable y que se presentan errores recurrentes en los sistemas. Del primer taller se retoman ISO/IEC 27001 (prioridad), COBIT e ITIL.

## 2. Supuestos

No se tuvo acceso a información real de la empresa, por lo que lo siguiente son **supuestos razonables, no hechos comprobados**. Deben validarse con las evidencias solicitadas en el primer taller.

1. Los respaldos de servidores y bases de datos se hacen de forma manual o semanal, y no se han hecho pruebas formales de restauración.
2. Las copias de seguridad se almacenan en la misma red o sede que los servidores, sin copia externa.
3. No existe un proceso automático que desactive las cuentas de usuarios retirados; la baja depende de que alguien avise a TI.
4. Los cambios en APK y Planning se aplican directamente en producción, sin ambiente de pruebas ni aprobación documentada.
5. Los errores se reportan por canales informales (llamada, WhatsApp) y no hay un registro histórico de incidentes.
6. El conocimiento técnico de los sistemas está concentrado en pocas personas del área de TI.

## 3. Activos y procesos analizados

| ID | Activo / proceso | Tipo | Por qué es importante |
|----|------------------|------|-----------------------|
| A1 | Base de datos y servidores de los ERP | Información / infraestructura | Contienen la información administrativa y productiva de la empresa. |
| A2 | Proceso de copias de seguridad y recuperación | Proceso | De él depende recuperar la operación tras una falla. |
| A3 | Aplicación Planning | Aplicación | Soporta la planeación de la producción. |
| A4 | Aplicación APK | Aplicación | Apoya procesos internos de la operación. |
| A5 | Proceso de altas, bajas y permisos de usuarios | Proceso | Controla quién accede a ERP, APK y Planning. |
| A6 | Proceso de gestión de cambios y mantenimientos | Proceso | Define cómo se modifican los sistemas en producción. |
| A7 | Proceso de atención de incidentes de TI | Proceso | Determina qué tan rápido se restablece el servicio. |

## 4. Escala utilizada

Se usa la escala sugerida por el docente, de 1 a 5 tanto para probabilidad como para impacto. **Nivel de riesgo = probabilidad × impacto** (valor mínimo 1, máximo 25).

| Valor | Probabilidad | Impacto |
|-------|--------------|---------|
| 1 | Raro | Consecuencia menor y fácil de corregir |
| 2 | Poco probable | Afecta una operación limitada |
| 3 | Posible | Afecta un proceso relevante o varios usuarios |
| 4 | Probable | Interrumpe un servicio importante o expone información sensible |
| 5 | Muy probable | Puede afectar gravemente la operación, datos críticos o cumplimiento |

Para clasificar el resultado del producto se usan estos rangos:

| Rango | Clasificación |
|-------|---------------|
| 15 – 25 | Crítico |
| 10 – 14 | Alto |
| 5 – 9 | Medio |
| 1 – 4 | Bajo |

## 5. Matriz de riesgos

Se usa una tabla por riesgo para que sea legible. Los riesgos están ordenados de mayor a menor nivel.

### R1 · Pérdida de datos por respaldos poco frecuentes y no probados — **Nivel 20 (Crítico)**

| Campo | Detalle |
|-------|---------|
| Activo o proceso | A1 y A2: base de datos de los ERP y proceso de respaldos |
| Amenaza | Falla de disco o servidor (o corrupción de la base de datos). |
| Vulnerabilidad | Los respaldos no se hacen con frecuencia suficiente, no se prueban y se guardan en el mismo sitio que los servidores. |
| Riesgo | Si el servidor del ERP falla, se perderían las transacciones registradas desde el último respaldo y la recuperación podría tardar días o fallar, deteniendo facturación, compras y producción. |
| Probabilidad | **4 – Probable** (hay fallas en los sistemas y los respaldos son poco frecuentes). |
| Impacto | **5 – Muy alto** (afecta datos críticos de toda la operación). |
| Nivel | **4 × 5 = 20** |
| Control actual | Existen copias de seguridad, pero con frecuencia insuficiente. No hay evidencia de pruebas de restauración ni de copia externa (supuestos 1 y 2). |
| Control propuesto | (a) Respaldo completo semanal y diario incremental, automatizado y con alerta por correo si falla. (b) Una copia semanal fuera de la sede o en la nube. (c) Prueba de restauración documentada cada trimestre, con tiempo medido. (d) Definir RPO ≤ 24 horas y RTO ≤ 8 horas, aprobados por la gerencia. |
| Justificación de prioridad | Es el riesgo con mayor nivel: la pérdida afecta todos los procesos, y la preocupación principal del caso ya apunta a esta debilidad. |

### R2 · Interrupción de la operación por errores recurrentes en los sistemas — **Nivel 16 (Crítico)**

| Campo | Detalle |
|-------|---------|
| Activo o proceso | A3, A4 y A7: Planning, APK y atención de incidentes |
| Amenaza | Errores de software o configuración en los sistemas. |
| Vulnerabilidad | Los incidentes no se registran ni se analizan, por lo que las causas raíz no se corrigen y los errores se repiten. |
| Riesgo | Un error repetido en Planning o APK puede dejar a los usuarios sin el sistema por horas, retrasando la programación de producción y generando reprocesos. |
| Probabilidad | **4 – Probable** (el caso ya reporta errores en diferentes sistemas). |
| Impacto | **4 – Alto** (interrumpe un servicio importante para varias áreas). |
| Nivel | **4 × 4 = 16** |
| Control actual | TI atiende los errores cuando se reportan, sin registro formal ni análisis de recurrencia (supuesto 5). |
| Control propuesto | (a) Registrar todo incidente en una herramienta de mesa de ayuda (puede ser una hoja compartida al inicio) con fecha, sistema, causa y tiempo de solución. (b) Revisión mensual de los 5 incidentes más repetidos con un plan de corrección. (c) Meta: reducir 30% los incidentes repetidos en seis meses. |
| Justificación de prioridad | Ya ocurre con frecuencia y afecta directamente la continuidad; es de bajo costo empezar a medirlo. |

### R3 · Infección por malware o ransomware en los servidores — **Nivel 15 (Crítico)**

| Campo | Detalle |
|-------|---------|
| Activo o proceso | A1 y A2: servidores y respaldos |
| Amenaza | Malware o ransomware que ingresa por correo, USB o equipos de usuario. |
| Vulnerabilidad | Posible falta de actualización del antivirus y de segmentación de red, y respaldos accesibles desde la misma red (supuesto 2). |
| Riesgo | Un ransomware podría cifrar los servidores y también los respaldos, dejando a la empresa sin datos y sin forma de recuperarlos. |
| Probabilidad | **3 – Posible** (amenaza común en empresas de este tamaño). |
| Impacto | **5 – Muy alto** (podría afectar gravemente la operación y los datos críticos). |
| Nivel | **3 × 5 = 15** |
| Control actual | Se asume que hay antivirus (a confirmar con evidencia). No hay evidencia de respaldos aislados. |
| Control propuesto | (a) Verificar mensualmente que el antivirus esté actualizado en servidores y equipos, con reporte de la consola. (b) Mantener una copia de respaldo desconectada o inmutable. (c) Separar la red de servidores de la red de usuarios. (d) Capacitación anual breve sobre correos sospechosos, con registro de asistencia. |
| Justificación de prioridad | Menos probable que R1 y R2, pero su impacto es máximo y el control (copia aislada) coincide con el de R1. |

### R4 · Acceso indebido con cuentas de personal retirado o permisos excesivos — **Nivel 12 (Alto)**

| Campo | Detalle |
|-------|---------|
| Activo o proceso | A5: gestión de usuarios y permisos en ERP, APK y Planning |
| Amenaza | Excolaborador (o empleado actual) que intenta acceder o modificar información sin autorización. |
| Vulnerabilidad | Las cuentas siguen activas después del retiro y no se revisan los permisos de forma periódica (supuesto 3). |
| Riesgo | Un excolaborador podría ingresar al ERP y consultar o alterar información comercial o de producción, sin que la empresa lo detecte. |
| Probabilidad | **3 – Posible** (los retiros de personal son frecuentes y la baja no está automatizada). |
| Impacto | **4 – Alto** (podría exponer información sensible o alterar datos). |
| Nivel | **3 × 4 = 12** |
| Control actual | Las bajas dependen de un aviso a TI; no hay evidencia de revisiones periódicas. |
| Control propuesto | (a) Procedimiento de retiro: Talento Humano notifica a TI el mismo día y TI desactiva las cuentas en máximo 24 horas, con registro. (b) Cada mes, comparar la lista de usuarios activos contra la nómina vigente y documentar las diferencias. (c) Revisión semestral de permisos por parte de cada jefe de área. |
| Justificación de prioridad | Es una falla de gestión de bajo costo de corregir, con impacto relevante sobre la confidencialidad. |

### R5 · Errores por cambios aplicados sin pruebas ni autorización — **Nivel 12 (Alto)**

| Campo | Detalle |
|-------|---------|
| Activo o proceso | A6, A3 y A4: gestión de cambios en Planning y APK |
| Amenaza | Error humano durante una modificación o actualización. |
| Vulnerabilidad | Los cambios se aplican directamente en producción, sin pruebas previas ni aprobación documentada (supuesto 4). |
| Riesgo | Una modificación mal probada en Planning podría dejar el sistema fuera de servicio o generar datos incorrectos de planeación, sin posibilidad de volver rápido a la versión anterior. |
| Probabilidad | **3 – Posible** (los cambios son habituales y no hay controles previos). |
| Impacto | **4 – Alto** (puede interrumpir un servicio importante y dañar datos). |
| Nivel | **3 × 4 = 12** |
| Control actual | No hay evidencia de un procedimiento formal de cambios. |
| Control propuesto | (a) Formato de solicitud de cambio con descripción, responsable, aprobador y plan de reversa. (b) Ambiente de pruebas (aunque sea una copia del sistema) antes de pasar a producción. (c) Ventanas de cambio fuera de horario productivo. (d) Respaldo obligatorio antes de cada cambio, con evidencia. |
| Justificación de prioridad | Relacionado con R2 (muchos errores nacen de cambios) y con costo de implementación bajo. |

### R6 · Dependencia de personas clave y falta de documentación — **Nivel 9 (Medio)**

| Campo | Detalle |
|-------|---------|
| Activo o proceso | A1, A3 y A4: servidores y aplicaciones |
| Amenaza | Salida o ausencia prolongada del personal de TI que conoce los sistemas. |
| Vulnerabilidad | El conocimiento técnico no está documentado y no hay inventario ni responsables definidos por sistema (supuesto 6). |
| Riesgo | Si se retira la persona que administra los ERP, la empresa podría tardar semanas en resolver fallas o restaurar un servidor por falta de manuales y claves. |
| Probabilidad | **3 – Posible** (la rotación de personal es posible). |
| Impacto | **3 – Moderado** (afecta un proceso relevante al retrasar la recuperación, sin afectar directamente los datos). |
| Nivel | **3 × 3 = 9** |
| Control actual | No hay evidencia de inventario actualizado ni de manuales de operación. |
| Control propuesto | (a) Inventario de servidores, aplicaciones y bases de datos con un responsable asignado a cada uno. (b) Manual de operación y restauración por sistema, revisado cada seis meses. (c) Claves administrativas custodiadas en un gestor de contraseñas con acceso de respaldo para dos personas. |
| Justificación de prioridad | Importante para la continuidad a mediano plazo, pero menos urgente que los riesgos sobre los datos. |

## 6. Resumen y priorización

| Prioridad | Riesgo | Nivel | Clasificación |
|-----------|--------|-------|---------------|
| 1 | R1 · Pérdida de datos por respaldos deficientes | 20 | Crítico |
| 2 | R2 · Errores recurrentes en los sistemas | 16 | Crítico |
| 3 | R3 · Malware o ransomware | 15 | Crítico |
| 4 | R4 · Cuentas de personal retirado | 12 | Alto |
| 4 | R5 · Cambios sin pruebas ni autorización | 12 | Alto |
| 6 | R6 · Dependencia de personas clave | 9 | Medio |

**Conclusión:** los tres riesgos críticos tienen que ver con disponibilidad e integridad de la información, lo que coincide con la preocupación principal planteada en el primer taller y con el orden de marcos elegido (ISO/IEC 27001, COBIT e ITIL). Una acción de bajo costo, como automatizar los respaldos y mantener una copia aislada, reduce a la vez R1 y R3.

## 7. Relación con el primer taller

| Riesgo | Marco de referencia | Evidencia del primer taller que ayudaría a validarlo |
|--------|---------------------|-------------------------------------------------------|
| R1, R3 | ISO/IEC 27001 | Registros de copias de seguridad, política de backups, evidencias de antivirus. |
| R4 | ISO/IEC 27001 | Listado de usuarios y permisos de ERP, APK y Planning. |
| R5, R6 | COBIT | Procedimientos de cambios, inventario de recursos, funciones y responsabilidades. |
| R2 | ITIL | Registro de incidentes, tiempos de respuesta, historial de cambios. |
