# Papel de trabajo P2: verificación de la ejecución de los respaldos

**Auditoría:** Prointimo S.A.S. · **Riesgo:** R1 · **Criterio:** C2 · **Auditora:** Isabela Páez Lopez
**Datos ficticios:** bitácora y política simuladas para este ejercicio.

## 1. Control revisado

Ejecución programada y monitoreo de los respaldos de las bases de datos de los ERP. Responsable del control: administrador de servidores y bases de datos (TI).

## 2. Criterio (política ficticia)

- Respaldo completo los domingos.
- Respaldo incremental de lunes a sábado.
- Todo respaldo fallido debe generar alerta y volver a ejecutarse dentro de las 24 horas siguientes, con evidencia.

## 3. Población, periodo y muestra

- **Periodo:** 1 al 30 de septiembre de 2026 (simulado).
- **Población:** 30 ejecuciones programadas (4 completas: 6, 13, 20 y 27; 26 incrementales).
- **Muestra:** 10 ejecuciones. Selección dirigida: las 4 completas y el cierre de mes (30 de septiembre). Selección por sorteo simulado: 2, 11, 17, 23 y 25 de septiembre.

## 4. Pasos

1. Obtener la bitácora simulada del periodo.
2. Listar las ejecuciones esperadas según la política.
3. Comparar fecha, tipo y estado de cada ejecución de la muestra.
4. Para cada fallo, buscar alerta y nueva ejecución dentro de 24 horas.
5. Registrar como excepción toda ejecución ausente, o fallida sin alerta o sin nueva ejecución en 24 horas.

## 5. Datos comparados y resultados

| # | Fecha (2026) | Día | Tipo esperado | Registro en bitácora (ficticia) | Estado | Alerta y reejecución en 24 h | Resultado |
|---|---|---|---|---|---|---|---|
| 1 | 2 sep | miércoles | Incremental | Existe | Exitoso | No aplica | Conforme |
| 2 | 6 sep | domingo | Completo | Existe | Exitoso | No aplica | Conforme |
| 3 | 11 sep | viernes | Incremental | Existe | Exitoso | No aplica | Conforme |
| 4 | 13 sep | domingo | Completo | Existe | Exitoso | No aplica | Conforme |
| 5 | 17 sep | jueves | Incremental | Existe | Fallido | Sin evidencia | **Excepción** |
| 6 | 20 sep | domingo | Completo | Existe | Exitoso | No aplica | Conforme |
| 7 | 23 sep | miércoles | Incremental | Existe | Exitoso | No aplica | Conforme |
| 8 | 25 sep | viernes | Incremental | Existe | Exitoso | No aplica | Conforme |
| 9 | 27 sep | domingo | Completo | Existe | Exitoso | No aplica | Conforme |
| 10 | 30 sep | miércoles | Incremental | Existe | Exitoso | No aplica | Conforme |

**Resumen:** 10 revisadas, 9 conformes, 1 excepción (hallazgo H-01 del informe).

## 6. Limitaciones

- Datos ficticios; no describen a Prointimo.
- Muestra de 10 de 30 ejecuciones: no permite proyectar resultados a toda la población.
- La causa de la excepción no se determinó.
- No se verificó si existió otra ejecución que cubriera el intervalo afectado.

## 7. Conclusión sobre lo examinado

En la muestra simulada, 9 de 10 ejecuciones cumplieron el criterio y 1 presentó una excepción por respaldo fallido sin alerta ni nueva ejecución. La prueba no demuestra que el mismo problema exista en toda la población ni que haya habido pérdida de datos.
