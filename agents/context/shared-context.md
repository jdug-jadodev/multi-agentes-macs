# Contexto Compartido — Estado Actual del Proyecto

> Este archivo es la **memoria persistente** del sistema multi-agente. Todos los agentes lo leen al iniciar una tarea y lo actualizan al terminar.
> **Categoría:** 🟡/🔴 Mixto — el snapshot se mantiene siempre; la bitácora se archiva periódicamente. Política completa en [`context/lifecycle.md`](lifecycle.md).

## Reglas

1. **Append-only en bitácora**: cada agente SOLO agrega líneas/bloques nuevos. NO borra ni modifica lo que otro agente escribió.
2. **Marca de tiempo**: cada entrada tiene fecha, agente y acción.
3. **Contexto histórico**: este archivo conserva el rastro completo de la sesión/proyecto. Para detalles profundos, ver `agents/<rol>/outputs/`.
4. **Rotación**: cuando la bitácora supere ~200 entradas, se archiva el bloque antiguo a `context/archive/bitacora/YYYY-MM-DD-bitacora.md`.

---

## Snapshot del Proyecto

| Campo | Valor |
|-------|-------|
| **Nombre** | Plataforma Interactiva de Algoritmos |
| **Stack principal** | TypeScript + Astro 4.16.18 + Vanilla JS/CSS |
| **Versión actual** | 0.0.1 |
| **Última actualización** | 2026-06-16 12:00 |
| **Estado** | desarrollo (FASE 1 en curso) |

---

## Bitácora de Eventos (append-only)

> Formato: `[YYYY-MM-DD HH:MM] [agente] — acción breve`

<!-- Los agentes agregan sus entradas aquí, nunca borran las anteriores -->

- [2026-06-16 12:00] [orchestrator] — Sistema MACS activado. Leí AGENTS.md, project-brief.md, shared-context.md, active-plan.md, decisions-log.md, architecture.md y lessons-learned.md. Listo para recibir tareas.

