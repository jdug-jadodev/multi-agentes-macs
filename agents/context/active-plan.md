# Plan Activo

> Plan en ejecución. Cuando se cierra, se mueve a `context/archive/plans/YYYY-MM-PLAN-XXX.md` y este archivo se **resetea** a estado de plantilla.
> **Categoría:** 🟡 Vivo — se resetea al cerrar. Política completa en [`context/lifecycle.md`](lifecycle.md).

## Metadata

- **ID del plan:** PLAN-<YYYYMMDD>-<NN>
- **Tarea:** <descripción corta>
- **Orquestador:** <MiniMax M3>
- **Fecha inicio:** <YYYY-MM-DD HH:MM>
- **Estado:** pending | in_progress | blocked | completed | cancelled

## Clasificación

<trivial | media | compleja | investigación>

## Agentes involucrados

1. <agente> — <rol en este plan>
2. ...

## Plan de ejecución

1. [ ] <paso 1> — <agente>
2. [ ] <paso 2> — <agente>
3. [ ] <paso 3> — <agente>
4. ...

## Paralelizaciones

- <paso X> ‖ <paso Y> (sin dependencias)

## Criterios de éxito

- [ ] <criterio 1>
- [ ] <criterio 2>
- [ ] <criterio 3>

## Outputs generados

| Agente | Archivo de output | Link |
|--------|-------------------|------|
| architect | `agents/architect/outputs/...` | ... |
| senior-dev | `agents/senior-dev/outputs/...` | ... |

## Bloqueos activos

- <ninguno | descripción del bloqueo>

## Decisiones tomadas durante el plan

- <decisión>: <justificación>

## Resultado final (al cerrar)

<resumen de qué se entregó>

## Lecciones aprendidas (para `lessons-learned.md`)

- <qué funcionó>
- <qué se puede mejorar>

---

## 🧹 Acciones de cierre (ejecutadas por el Orquestador)

Al pasar este plan a estado `completed`, el Orquestador ejecuta:

- [ ] Mover este archivo a `context/archive/plans/YYYY-MM-PLAN-XXX.md`
- [ ] Agregar encabezado de archivo con fecha y link al plan original
- [ ] Resetear `active-plan.md` a esta plantilla
- [ ] Si hubo decisión arquitectónica → ADR en `decisions-log.md`
- [ ] Si cambió la arquitectura → actualizar `architecture.md` y archivar versión previa
- [ ] Agregar entrada a `shared-context.md` cerrando el plan
- [ ] Si hay lecciones → agregar a `lessons-learned.md`
