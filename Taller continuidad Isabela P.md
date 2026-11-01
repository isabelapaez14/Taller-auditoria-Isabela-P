# Taller: Del riesgo a la auditoría (programa de trabajo)

**Auditoría de Sistemas (ET0114)**
**Docente:** Juan Duque
**Integrante:** Isabela Páez Lopez
**Caso:** Prointimo S.A.S.
**Matriz de riesgos vigente (anexo):** [matriz_riesgos_prointimo.md](matriz_riesgos_prointimo.md)

---

## 1. Identificación del equipo y del caso

| Dato | Detalle |
|------|---------|
| Integrante | Isabela Páez Lopez (única integrante) |
| Organización | Prointimo S.A.S., empresa textil y de confección |
| Sistemas del caso | Dos ERP y las aplicaciones internas APK y Planning |
| Marcos elegidos en el primer taller | ISO/IEC 27001 (principal), COBIT e ITIL |
| Riesgo elegido para esta auditoría | **R1: Pérdida de datos por respaldos poco frecuentes y no probados** |

## 2. Contexto y riesgo seleccionado

**Contexto.** Prointimo S.A.S. usa dos ERP y las aplicaciones APK y Planning para sus procesos administrativos, productivos y de planeación. El área de TI maneja los servidores y hace copias de seguridad, pero no con la frecuencia recomendable, y se han presentado errores en algunos sistemas. La preocupación central es que una falla pueda causar pérdida de información o detener la operación.

**Riesgo seleccionado (tomado de la matriz, riesgo R1):**

| Elemento | Detalle |
|----------|---------|
| Activo o proceso afectado | Base de datos y servidores de los ERP, y el proceso de copias de seguridad y recuperación |
| Amenaza | Falla de disco o servidor (o corrupción de la base de datos) |
| Vulnerabilidad | Los respaldos no se hacen con frecuencia suficiente, no se prueban y se guardan en el mismo sitio que los servidores |
| Consecuencia posible | Si el servidor del ERP falla, se perderían las transacciones registradas desde el último respaldo, y la recuperación podría tardar días o fallar. Se detendrían facturación, compras y producción |
| Probabilidad | 4 – Probable. Hay fallas en los sistemas y los respaldos son poco frecuentes |
| Impacto | 5 – Muy alto. Afecta datos críticos de toda la operación |
| Nivel de riesgo | 4 × 5 = **20 (Crítico)** |
| Control actual | Existen copias de seguridad, pero con frecuencia insuficiente. No hay evidencia de pruebas de restauración ni de copia externa (supuestos de la matriz) |
| Control propuesto | Respaldo completo semanal y diario incremental automatizado con alertas, copia semanal fuera de la sede, prueba de restauración trimestral documentada y definir RPO y RTO aprobados por la gerencia |

**Por qué vale la pena auditarlo.** No basta con decir que es el riesgo de mayor puntaje. Hay cuatro razones:

1. **El proceso es muy importante.** Los ERP concentran la información de toda la empresa. Si no se puede recuperar, no importa qué tan bien funcionen los demás controles.
2. **Es la preocupación principal del caso.** Desde el primer taller se identificó que los respaldos son poco frecuentes.
3. **Es posible revisar el control.** Los respaldos dejan evidencia concreta: bitácoras de ejecución, configuración de las tareas programadas, ubicación de las copias y actas de restauración. Se puede comparar lo que debería pasar con lo que realmente pasó.
4. **Corregirlo es viable y trae ganancias en cadena.** Mejorar los respaldos también reduce el impacto del riesgo de ransomware (R3), que usa la misma copia aislada como control.

## 3. Justificación y objetivo de auditoría

**Objetivo principal:**

> Determinar si las copias de seguridad de las bases de datos de los ERP de Prointimo se ejecutan con la frecuencia definida por la empresa, se guardan de forma separada y protegida, y se comprueban mediante pruebas de restauración documentadas durante el periodo auditado.

Este objetivo se puede verificar porque plantea condiciones que se pueden comparar con evidencia: frecuencia definida contra ejecuciones reales, ubicación de copias y existencia de pruebas de restauración.

**Objetivos específicos:**

1. Verificar si existe una política o procedimiento de respaldo vigente, con frecuencia, responsable y tiempo de conservación definidos.
2. Comprobar si las ejecuciones de respaldo del periodo corresponden a lo programado y si los fallos se detectan y corrigen.
3. Evaluar si las copias se guardan fuera del servidor de producción y con acceso restringido.
4. Determinar si se hacen pruebas de restauración y si sus resultados se documentan.

## 4. Alcance funcional y exclusiones

| Aspecto | Definición |
|---------|------------|
| **Proceso o función** | Copias de seguridad y recuperación de las bases de datos de los ERP: programación, ejecución, almacenamiento y pruebas de restauración |
| **Sistema o componente** | Servidores y bases de datos de los dos ERP, la herramienta o tarea programada que genera los respaldos y el lugar donde se almacenan las copias |
| **Población** | Ejecuciones programadas de respaldo del periodo (según bitácoras), alertas de fallo, copias almacenadas y registros de pruebas de restauración |
| **Periodo** | Los seis meses anteriores al inicio de la auditoría (propuesto). Es un tiempo suficiente para ver patrones, fallos y cierres de mes, sin hacer la revisión demasiado larga. Se ajustaría si las bitácoras no conservan ese historial |
| **Áreas o responsables** | Área de TI (responsable de servidores y bases de datos, y jefe de TI); gerencia, que aprobaría la política y los tiempos de recuperación |
| **Inclusiones** | Respaldos de las bases de datos de los dos ERP, su ubicación y protección, la política que los rige y las pruebas de restauración |
| **Exclusiones** | (a) APK y Planning, que se trataron en otros riesgos de la matriz (R2 y R5); (b) el control de acceso a los servidores y el antivirus (R3 y R4); (c) respaldos de equipos de usuarios |

**Razón y límite de las exclusiones.** Se excluyen para no abarcar «todos los sistemas y todos los controles». Esto limita la conclusión: el resultado solo servirá para decir si **los respaldos de los ERP** son confiables. No permitirá afirmar que toda la continuidad de TI de Prointimo esté controlada ni que APK y Planning estén protegidos.

## 5. Criterios de evaluación

No se conocen las políticas internas de Prointimo, así que cuando falta ese dato se escribe «criterio por confirmar mediante solicitud de la política vigente». Citar un marco solo como «cumplir ISO/IEC 27001» no es un criterio que se pueda comprobar, por eso se convierte en condiciones concretas.

| ID | Condición esperada | Fuente | Por qué aplica al caso |
|----|--------------------|--------|------------------------|
| C1 | Existe una política o procedimiento de respaldo aprobado y vigente, con frecuencia, alcance, tiempo de conservación y responsable | Política interna de TI (**por confirmar mediante solicitud de la política vigente**). Referencia general: ISO/IEC 27001, que pide respaldos como parte de la seguridad de la información | Sin una regla definida no se puede decir si los respaldos son suficientes |
| C2 | Los respaldos se ejecutan con la frecuencia definida en la política, y los fallos se detectan y corrigen | Política de respaldo (**frecuencia por confirmar**) | Es la vulnerabilidad principal del riesgo: la frecuencia insuficiente |
| C3 | Hay al menos una copia en un lugar separado del servidor de producción, con acceso restringido | Política interna (**por confirmar**) y buena práctica de ISO/IEC 27001 | Si la copia está en el mismo sitio, una falla del servidor la destruye también |
| C4 | Se prueban restauraciones de forma periódica y se documentan sus resultados | Política interna (**por confirmar**); referencia general de ISO/IEC 27001 | Un respaldo que no se ha probado no garantiza que se pueda recuperar |
| C5 | Hay tiempos máximos de pérdida de datos (RPO) y de recuperación (RTO) definidos y aprobados por la gerencia | Política interna (**por confirmar**); COBIT, en su enfoque de gestión de la continuidad | Permite decidir qué tan buena es la frecuencia de respaldo |

**Nota sobre la matriz.** Los valores que aparecen como controles propuestos en la matriz (por ejemplo RPO ≤ 24 horas) son una propuesta de mejora, **no** un criterio verificado de la empresa. En la auditoría solo se compararía contra los valores que Prointimo tenga realmente definidos. No se atribuyen a ISO/IEC 27001 ni a COBIT plazos, porcentajes ni requisitos específicos que no se hayan verificado.

## 6. Programa de trabajo

Cada procedimiento indica qué se obtendría, qué se compararía, sobre qué población o muestra y qué evidencia se guardaría.

### P1. Comprender y verificar el diseño del control

| Elemento | Detalle |
|----------|---------|
| **Control** | Política y configuración de los respaldos de los ERP; TI (administrador de servidores y bases de datos) los define y opera |
| **Criterio** | C1, C3 y C5 |
| **Procedimiento** | 1) Solicitar la política o procedimiento de respaldo y recuperación. 2) Entrevistar al responsable de TI para entender cómo funciona el proceso: qué se respalda, cada cuánto, dónde se guarda y quién lo revisa. 3) Solicitar capturas de la configuración de las tareas programadas de cada ERP y de la ubicación de las copias. 4) Comparar la configuración con lo que dice la política y con lo que contó la persona entrevistada |
| **Población o muestra** | Las bases de datos de los dos ERP (población pequeña, se revisan todas) |
| **Evidencia esperada** | Política vigente con fecha y aprobación, capturas de configuración, lista de ubicaciones de almacenamiento, nombre del responsable |
| **Posibles excepciones** | No existe política o está sin aprobar; la frecuencia configurada no coincide con la política; las copias solo están en el mismo servidor; no hay RPO ni RTO definidos |

### P2. Verificar la ejecución de los respaldos

| Elemento | Detalle |
|----------|---------|
| **Control** | Ejecución programada y monitoreo de los respaldos; lo realiza TI |
| **Criterio** | C2 |
| **Procedimiento** | 1) Solicitar las bitácoras o reportes de la herramienta de respaldo del periodo. 2) Armar la lista de ejecuciones que debieron ocurrir según la frecuencia definida. 3) Comparar contra las ejecuciones registradas (fechas, estado exitoso o fallido, tamaño). 4) Para cada fallo, pedir evidencia de que se detectó y se volvió a ejecutar |
| **Población o muestra** | Todas las ejecuciones programadas del periodo. Si son demasiadas para revisarlas una a una, se tomaría una muestra aleatoria que incluya siempre las del cierre de cada mes. El tamaño se definiría cuando se conozca la población real (no se inventa una cantidad) |
| **Evidencia esperada** | Bitácoras o reportes exportados, alertas o correos de fallo, tickets de corrección |
| **Posibles excepciones** | Días sin respaldo; respaldos fallidos sin repetir; bitácoras que no cubren todo el periodo; respaldos sin evidencia de revisión |

### P3. Verificar las pruebas de restauración

| Elemento | Detalle |
|----------|---------|
| **Control** | Pruebas periódicas de restauración; TI las ejecuta y la jefatura debería revisarlas |
| **Criterio** | C4 y C5 |
| **Procedimiento** | 1) Solicitar los registros de pruebas de restauración del periodo. 2) Seleccionar algunos respaldos del periodo y comprobar que existen y se pueden leer. 3) Si hay acceso, observar una restauración en un ambiente de prueba y medir el tiempo que tarda. 4) Comparar el tiempo con el RTO definido (si existe) |
| **Población o muestra** | Todas las pruebas registradas en el periodo; para la verificación de lectura, una muestra pequeña de respaldos de distintas fechas (incluido uno de cierre de mes) |
| **Evidencia esperada** | Actas o informes de prueba, capturas de la restauración, tiempos medidos, firma o aprobación de la jefatura |
| **Posibles excepciones** | No hay pruebas registradas; una restauración fallida sin corrección; la prueba no está documentada; el tiempo de recuperación supera lo definido |

### P4. Verificar ubicación y protección de las copias

| Elemento | Detalle |
|----------|---------|
| **Control** | Almacenamiento separado y acceso restringido a las copias; TI los define |
| **Criterio** | C3 |
| **Procedimiento** | 1) Identificar dónde se guardan las copias (servidor, disco externo, nube, otra sede). 2) Comprobar que al menos una copia esté fuera del servidor de producción. 3) Solicitar la lista de usuarios con permiso sobre las copias y revisar que sean solo los necesarios |
| **Población o muestra** | Todas las ubicaciones de almacenamiento y todos los usuarios con acceso a ellas |
| **Evidencia esperada** | Capturas de rutas y permisos, lista de usuarios con acceso, contrato o configuración del almacenamiento externo (si existe) |
| **Posibles excepciones** | Copias solo en el mismo servidor; acceso amplio sin justificación; no existe copia externa |

**Sobre las entrevistas.** La entrevista sirve para entender cómo funciona el proceso, pero **no es la única evidencia** de que el control opera. Cada cosa que diga TI se corroboraría con registros o configuraciones, por ejemplo comparando la frecuencia que cuenta el responsable con las bitácoras de ejecución.

### Fila de trazabilidad

| ID del riesgo | Control a evaluar | Criterio y fuente | Procedimiento | Población o muestra | Evidencia esperada |
|---------------|-------------------|-------------------|---------------|---------------------|--------------------|
| R-01 | Política y configuración de respaldos de los ERP | C1, C3, C5. Política interna (por confirmar), ISO/IEC 27001, COBIT | P1. Revisar política, entrevistar y comparar con la configuración | Bases de datos de los dos ERP (todas) | Política vigente, capturas de configuración, ubicaciones |
| R-01 | Ejecución programada de respaldos | C2. Política de respaldo (frecuencia por confirmar) | P2. Comparar ejecuciones esperadas contra bitácoras | Ejecuciones del periodo (todas o muestra aleatoria con cierres de mes) | Bitácoras, alertas de fallo, tickets |
| R-01 | Pruebas de restauración | C4, C5. Política interna (por confirmar), ISO/IEC 27001 | P3. Revisar registros y observar una restauración de prueba | Pruebas del periodo y una muestra de respaldos | Actas de prueba, tiempos medidos, capturas |
| R-01 | Ubicación y acceso a las copias | C3. Política interna (por confirmar), ISO/IEC 27001 | P4. Verificar ubicaciones y permisos | Ubicaciones y usuarios con acceso (todos) | Capturas de rutas, permisos y lista de usuarios |

## 7. Responsables, cronograma, supuestos y limitaciones

### Responsables

| Rol | Persona o área | Función |
|-----|----------------|---------|
| Auditora | Isabela Páez Lopez | Planea, solicita información, revisa la evidencia y redacta las conclusiones |
| Responsable de TI | Administrador de servidores y bases de datos | Explica el proceso y entrega bitácoras, configuraciones y capturas |
| Jefe de TI | Jefatura del área | Entrega la política, aprueba el acceso a la información y recibe los resultados |
| Gerencia | Dirección de la empresa | Aprueba tiempos de recuperación y recibe el informe |

### Cronograma propuesto (4 semanas)

| Semana | Fase | Actividades | Producto |
|--------|------|-------------|----------|
| 1 | Preparación | Presentar el objetivo y el alcance a TI, confirmar el periodo, preparar formatos de papeles de trabajo | Plan aprobado y lista de información a solicitar |
| 2 | Solicitud de información | Pedir política, configuraciones, bitácoras, registros de pruebas y lista de accesos | Evidencia recibida y registrada |
| 3 | Revisión | Ejecutar P1 a P4, comparar contra criterios y registrar excepciones | Papeles de trabajo con hallazgos preliminares |
| 4 | Cierre | Confirmar hallazgos con TI, redactar conclusiones y recomendaciones, presentar el resultado | Informe final |

### Dependencias y recursos

- Que TI entregue a tiempo las bitácoras y la política, y que las bitácoras conserven el historial del periodo.
- Acceso de solo lectura a la herramienta de respaldo y, si es posible, un ambiente de pruebas para observar una restauración.
- Una hoja de cálculo para comparar ejecuciones esperadas contra reales y un formato de papeles de trabajo.
- Disponibilidad del responsable de TI para entrevistas y aclaraciones.

### Qué se puede hacer realmente y qué queda como planificación

| Parte | Estado |
|-------|--------|
| Identificar el riesgo, definir el objetivo, el alcance, los criterios y el programa de trabajo | **Se realiza en este trabajo** |
| Solicitar documentos, revisar bitácoras, observar la restauración y concluir | **Queda como planificación**, porque no se tiene acceso a la información real de Prointimo |

### Supuestos

Los siguientes son supuestos, **no hechos comprobados**. Vienen de la matriz de riesgos y deben confirmarse con evidencia:

1. Los respaldos se hacen de forma manual o semanal y no se han hecho pruebas formales de restauración.
2. Las copias se guardan en la misma red o sede que los servidores, sin copia externa.
3. No se conoce la política interna de respaldo, por eso los criterios figuran como «por confirmar».
4. El área de TI está dispuesta a entregar bitácoras y configuraciones durante la auditoría.

### Limitaciones

- La conclusión se limita a los respaldos de las bases de datos de los ERP y al periodo definido (ver exclusiones).
- Si las bitácoras no conservan el historial del periodo, la revisión de ejecuciones sería parcial y habría que dejarlo indicado.
- Como se trabaja con una sola auditora, no hay revisión cruzada de los papeles de trabajo.
- Sin acceso a información real, los valores de probabilidad e impacto y los hallazgos son estimaciones y deben contrastarse con la evidencia.

## 8. Fuentes y referencia a la matriz

- Matriz de riesgos de Prointimo S.A.S. (anexo): [matriz_riesgos_prointimo.md](matriz_riesgos_prointimo.md). El riesgo analizado es **R1**.
- Taller anterior: «Elige el marco correcto para tu auditoría» (Prointimo S.A.S., marcos ISO/IEC 27001, COBIT e ITIL y evidencias a solicitar).
- ISO/IEC 27001, norma de sistemas de gestión de la seguridad de la información (consultada solo como referencia general, sin citar requisitos específicos).
- COBIT, marco de gobierno y gestión de TI de ISACA (consultado solo como referencia general, sin citar requisitos específicos).
- Enunciado y rúbrica del taller (Auditoría de Sistemas ET0114, docente Juan Duque).
