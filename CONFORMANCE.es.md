> Traducción comunitaria (borrador) — Política P2-002 de NTARI, Difusión Multilingüe Global. Fuente: CONFORMANCE.md (original en inglés, instantánea del 2026-10-05). Borrador comunitario asistido por máquina, pendiente de revisión por mantenedores regionales conforme a P2-002 §3.1. Las especificaciones técnicas centrales permanecen en inglés conforme a §2.2.
>
> ¿Encontraste un error en esta traducción? Tu corrección es una contribución
> bienvenida y valorada: haz un fork del repositorio y abre un pull request en
> https://github.com/NTARI-RAND/childcare-trust-network.

> **El original en inglés es normativo.** Esta traducción se ofrece para lectura, no para interpretación: donde difiera de `CONFORMANCE.md`, rige el inglés. Las palabras clave normativas (MUST, MUST NOT, SHOULD, SHOULD NOT, MAY), los nombres de campos, las etiquetas y los identificadores se mantienen en inglés porque constituyen el contrato de conformidad.

# CTN — Autodescripción de conformidad

*Autodeclarada hasta que una suite de pruebas cite estos ID (registro: `JFA/jfa-conformance-suite.py`). CTN está en etapa de propuesta; "cumplido por diseño" significa que la especificación (`CLAUDE.md`) enuncia la regla y el criterio de aceptación — el código todavía debe hacerla vinculante.*

**Forma:** la economía del cuidado de alto riesgo de la Parte VI de la arquitectura — distribución completa de las evaluaciones, una capa de seguridad centrada en la prevención que prevalece sobre todas las demás reglas.

| ID | Invariante | Estado |
|---|---|---|
| COV-1 | Sin promedios; distribución completa | **Cumplido por diseño** — sección "Do not average", criterio de aceptación con grep; delegar a CI en la compilación |
| COV-2 | La calificación más baja es el incumplimiento | **Cumplido por diseño** — `-1` es daño, `harm_flagged`, comentario obligatorio |
| COV-3 | Simétrico; toda afirmación admite respuesta | **Parcial** — calificación multidireccional, sí; disputa/derecho de réplica, abierto (OQ-6) |
| COV-4 | Decide si, nunca cuánto | **Cumplido por diseño** — tres señales honestas (verificación, distribución, antigüedad), nunca fusionadas |
| REC-1 | De solo adición | **Cumplido por diseño** — eventos de calificación inmutables; atestiguamiento abierto (OQ-7) |
| REC-2 | Perdonar, nunca ocultar | **Cumplido por diseño** — las disputas marcan y contextualizan, nunca borran |
| REC-3 | Nada de PII en el bien común | **Cumplido por diseño** — los datos de menores nunca entran en el almacén de eventos ni en ninguna salida de reputación |
| REC-9 | Tipos de relación | **Abierto** (OQ-8) |
| ECO-4/5 | Depósito de garantía primero; ganado, nunca comprado, si alguna vez entra el crédito | **Valor por defecto comprometido** (OQ-5) |
| GOV-9 | Documento vivo de preguntas abiertas | **Cumplido** — `OPEN-QUESTIONS.md` se distribuye con esta semilla |
| GOV-10 | Bien común copyleft | **Cumplido** — AGPL-3.0, declarado en la especificación |

**Precedencia nombrada:** la vía de seguridad infantil prevalece sobre el pacto donde entren en conflicto — el precedente de alto riesgo de la Parte VI, adoptado deliberadamente, con el debido proceso rigiendo la durabilidad de las consecuencias y no la protección inmediata.

**Línea de honestidad:** CTN no tiene registro atestiguado; toda afirmación de conducta que hace hoy es autodeclarada (problema abierto 2 de la arquitectura).
