# Informe de auditoría y plan de acción: respaldos de los ERP de Prointimo S.A.S.

**Asignatura:** ET0114 · Auditoría de Sistemas
**Docente:** Juan Duque
**Integrante:** Isabela Páez Lopez (única integrante)

---

## 1. Identificación y resumen ejecutivo

| Dato | Detalle |
|---|---|
| Organización | Prointimo S.A.S., empresa textil y de confección |
| Sistemas del caso | Dos ERP y las aplicaciones internas APK y Planning |
| Riesgo auditado | **R1:** Pérdida de datos por respaldos poco frecuentes y no probados (probabilidad 4 × impacto 5 = **20, Crítico**) |
| Procedimiento ejecutado | **P2:** Verificar la ejecución de los respaldos (criterio C2) |
| Naturaleza del ejercicio | Simulado, con datos ficticios |

**Resumen.** El riesgo R1 fue el de mayor nivel en la matriz de riesgos y la preocupación principal del caso. Del programa de trabajo se ejecutó el procedimiento P2, que compara las ejecuciones de respaldo que debían ocurrir con las registradas en una bitácora **simulada**. En una muestra ficticia de 10 ejecuciones, **9 se realizaron conforme a la política ficticia y 1 presentó una excepción** (respaldo incremental fallido el 17 de septiembre, sin evidencia simulada de alerta ni de nueva ejecución). La causa queda **pendiente de confirmar**. Los procedimientos P1, P3 y P4 **no se ejecutaron** y permanecen como trabajo pendiente.

---

## 2. Objetivo y alcance

**Objetivo general de la auditoría (del programa de trabajo).** Determinar si las copias de seguridad de las bases de datos de los ERP de Prointimo se ejecutan con la frecuencia definida por la empresa, se guardan de forma separada y protegida, y se comprueban mediante pruebas de restauración documentadas.

**Objetivo de esta prueba.** Comprobar, con datos simulados, si los respaldos programados de las bases de datos de los ERP se ejecutan con la frecuencia definida y si los fallos se detectan y corrigen (objetivo específico 2 del programa).

| Aspecto | Definición |
|---|---|
| Proceso | Ejecución programada y monitoreo de los respaldos de las bases de datos de los ERP |
| Sistema | Bases de datos de los dos ERP y la tarea programada que genera los respaldos |
| Periodo de la prueba | 1 al 30 de septiembre de 2026 (**periodo simulado**). El programa original proponía seis meses; se redujo para este ejercicio |
| Población | 30 ejecuciones programadas (una por día) según la bitácora **ficticia** |
| Responsable del control | Administrador de servidores y bases de datos (TI) |
| Exclusiones | APK y Planning (riesgos R2 y R5); control de acceso a servidores y antivirus (R3 y R4); respaldos de equipos de usuario; procedimientos P1, P3 y P4 del programa (no ejecutados) |

**Límite de las exclusiones.** El resultado no permite afirmar que toda la continuidad de TI esté controlada, ni que APK y Planning estén protegidos, ni que las pruebas de restauración o la ubicación de las copias sean adecuadas.

---

## 3. Criterios y metodología

### 3.1 Criterio

Prointimo no entregó su política real, por lo que se define una **regla ficticia** para poder realizar la prueba. Corresponde al criterio **C2** del programa de trabajo.

> **Política de respaldo (FICTICIA):**
> - Respaldo completo todos los domingos.
> - Respaldo incremental de lunes a sábado.
> - Todo respaldo fallido debe generar una alerta y volver a ejecutarse dentro de las 24 horas siguientes, con evidencia.

Esta regla coincide con el control propuesto en la matriz de riesgos, pero **no es un requisito verificado de Prointimo, de ISO/IEC 27001 ni de COBIT**. En una auditoría real habría que sustituirla por la política vigente de la empresa (criterio C1, por confirmar).

### 3.2 Selección de la muestra

- **Población:** 30 ejecuciones programadas de septiembre de 2026 (4 completas los domingos 6, 13, 20 y 27, y 26 incrementales).
- **Muestra:** 10 ejecuciones (33 % de la población). Se incluyeron de forma dirigida las 4 completas y el cierre de mes (30 de septiembre), y se sortearon 5 días adicionales: 2, 11, 17, 23 y 25 de septiembre (**sorteo simulado**).
- La muestra no permite proyectar resultados a toda la población.

### 3.3 Procedimiento (P2 del programa de trabajo)

1. Obtener la bitácora de la herramienta de respaldo del periodo (**simulada**).
2. Construir la lista de ejecuciones esperadas según la política ficticia.
3. Comparar fecha, tipo y estado de cada ejecución de la muestra.
4. Para cada ejecución fallida, buscar evidencia de alerta y de nueva ejecución dentro de 24 horas.
5. **Condición de excepción:** ejecución ausente, fallida sin nueva ejecución en 24 horas o sin evidencia de alerta.

### 3.4 Evidencia examinada

Bitácora **ficticia** de respaldos de septiembre de 2026. Anexo: [papel_trabajo_P2.md](./papel_trabajo_P2.md).

---

## 4. Resultados y hallazgos

### 4.1 Resultado de la prueba (datos ficticios)

| # | Fecha (2026) | Tipo esperado | Estado en bitácora (ficticia) | Alerta y reejecución en 24 h | Resultado |
|---|---|---|---|---|---|
| 1 | 2 de septiembre | Incremental | Exitoso | No aplica | Conforme |
| 2 | 6 de septiembre | Completo | Exitoso | No aplica | Conforme |
| 3 | 11 de septiembre | Incremental | Exitoso | No aplica | Conforme |
| 4 | 13 de septiembre | Completo | Exitoso | No aplica | Conforme |
| 5 | 17 de septiembre | Incremental | **Fallido** | **Sin evidencia** | **Excepción** |
| 6 | 20 de septiembre | Completo | Exitoso | No aplica | Conforme |
| 7 | 23 de septiembre | Incremental | Exitoso | No aplica | Conforme |
| 8 | 25 de septiembre | Incremental | Exitoso | No aplica | Conforme |
| 9 | 27 de septiembre | Completo | Exitoso | No aplica | Conforme |
| 10 | 30 de septiembre (cierre de mes) | Incremental | Exitoso | No aplica | Conforme |

**Resumen:** 10 ejecuciones revisadas, 9 conformes y 1 excepción.

### 4.2 Hallazgo H-01 (simulado): respaldo fallido sin alerta ni nueva ejecución

| Componente | Descripción |
|---|---|
| **Criterio** | Todo respaldo fallido debe generar alerta y volver a ejecutarse dentro de 24 horas (política **ficticia**, criterio C2) |
| **Condición** | En 1 de las 10 ejecuciones revisadas de la bitácora simulada (17 de septiembre), el respaldo incremental figura como fallido y no hay evidencia de alerta ni de nueva ejecución en las 24 horas siguientes |
| **Causa** | **Pendiente de confirmar.** La prueba no la establece. Podría deberse a la configuración de alertas, al seguimiento de la bitácora o a otra razón, pero no hay evidencia que lo sustente |
| **Efecto o riesgo** | Pudo quedar un periodo sin cobertura de respaldo de las bases de datos de los ERP. De haber fallado el servidor en ese lapso, la recuperación podría haber perdido las transacciones posteriores a la última copia válida (materialización del riesgo R1). El alcance real del intervalo sin cobertura **no se determinó** |
| **Recomendación** | Revisar cómo se detectan y atienden los respaldos fallidos, activar alertas con confirmación de lectura y registrar la corrección de cada fallo |

### 4.3 Qué no se afirma

- No se afirma que el fallo se repita en otros días ni que exista un porcentaje de falla en toda la población: solo se revisaron 10 de 30 ejecuciones.
- No se afirma que los datos se hayan perdido ni que alguien haya sufrido consecuencias.
- No se afirma nada sobre las ejecuciones no incluidas en la muestra.
- Los resultados corresponden a datos simulados y no describen a Prointimo.

---

## 5. Conclusión y limitaciones

**Conclusión.** En la muestra **simulada** de 10 ejecuciones, 9 cumplieron la política ficticia y 1 presentó una excepción (H-01). Esto indica que, **en este escenario**, el control de ejecución y monitoreo de respaldos operó en la mayoría de los casos revisados, pero el manejo de fallos mostró una debilidad. La prueba no permite concluir si el proceso de respaldo de Prointimo es confiable.

**Limitaciones.**

1. Datos, bitácora y política **ficticios**; sin acceso a información real.
2. Muestra de 10 ejecuciones en un mes simulado, no representativa de seis meses.
3. Causa del hallazgo no determinada.
4. **No se ejecutaron** P1 (diseño del control y política vigente), P3 (pruebas de restauración) ni P4 (ubicación y protección de copias). Siguen vigentes los supuestos de la matriz: copias en el mismo sitio que los servidores y sin pruebas formales de restauración. Son supuestos, no hallazgos.
5. Auditoría realizada por una sola persona, sin revisión cruzada de los papeles de trabajo.

**Pendiente.** Ejecutar P1, P3 y P4 con información real y autorizada, o con una simulación documentada, antes de concluir sobre el riesgo R1 completo.

---

## 6. Plan de acción y anexos

### 6.1 Acción para el hallazgo H-01 (propuesta)

| Campo | Detalle |
|---|---|
| Acción propuesta | Revisar el proceso de detección de respaldos fallidos: activar alerta por correo, definir quién la atiende y registrar la nueva ejecución de cada fallo |
| Responsable propuesto | Administrador de servidores y bases de datos (TI), con supervisión del jefe de TI |
| Prioridad | Alta, porque el riesgo R1 tiene nivel crítico (20) y un respaldo fallido sin atender deja datos sin cobertura |
| Plazo propuesto | 30 días, sujeto a acuerdo con la organización |
| Evidencia de cierre | Configuración de alertas, procedimiento actualizado y bitácora posterior que muestre un fallo (real o de prueba) atendido dentro del plazo |

### 6.2 Acciones de seguimiento (propuestas, no derivadas de hallazgos)

Estas acciones **no responden a hallazgos**, porque los procedimientos correspondientes no se ejecutaron. Son propuestas de continuidad del trabajo.

| Acción propuesta | Responsable propuesto | Plazo propuesto | Evidencia de cierre |
|---|---|---|---|
| Ejecutar P1: obtener la política de respaldo vigente y confirmar frecuencia, RPO y RTO | Auditora, con jefe de TI | 2 semanas desde la autorización | Política con fecha y aprobación; papel de trabajo P1 |
| Ejecutar P3: revisar pruebas de restauración | Auditora, con TI | 4 semanas | Actas de prueba y tiempos medidos |
| Ejecutar P4: verificar copia fuera del servidor y accesos | Auditora, con TI | 4 semanas | Capturas de rutas, permisos y lista de usuarios |

### 6.3 Trazabilidad y anexos

| Elemento | Relación con este informe | Enlace |
|---|---|---|
| Taller 1: marcos | Contexto y marcos: ISO/IEC 27001, COBIT, ITIL | [Taller Elige el marco correcto.md](./Taller%20Elige%20el%20marco%20correcto.md) |
| Taller 2: matriz de riesgos | Riesgo R1, nivel 20, control actual y propuesto | [matriz_riesgos_prointimo.md](./matriz_riesgos_prointimo.md) |
| Taller 3: programa de trabajo | Objetivo, alcance, criterio C2 y procedimiento P2 | [Taller continuidad Isabela P.md](./Taller%20continuidad%20Isabela%20P.md) |
| Papel de trabajo P2 (simulado) | Muestra, pasos y resultados de la prueba | [papel_trabajo_P2.md](./papel_trabajo_P2.md) |

**Trazabilidad:** R1 (matriz) → control: ejecución programada de respaldos → criterio C2 (política ficticia) → procedimiento P2 → muestra de 10 ejecuciones → hallazgo H-01 → acción 6.1.

**Protección de datos.** No se utilizó información real ni datos personales. Todos los datos de la prueba son ficticios.
