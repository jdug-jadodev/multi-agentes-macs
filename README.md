# 🤖 MACS — Multi-Agent Collaboration System

> Sistema multi-agente **transversal** basado en los principios del artículo *"Building a multi-agent research system"* de Anthropic, **optimizado para MiniMax M3**.

---

## ¿Qué es esto?

MACS es un **sistema de 6 agentes** que colaboran para abordar tareas de desarrollo de software de forma estructurada, trazable y de alta calidad.

```
┌────────────┐  ┌────────────┐  ┌────────────┐
│ Orquestador│  │ Líder      │  │ Arquitecto │
│            │  │ Técnico    │  │            │
└────────────┘  └────────────┘  └────────────┘
┌────────────┐  ┌────────────┐
│ Senior Dev │  │ QA & Sec   │
│            │  │            │
└────────────┘  └────────────┘
┌────────────┐
│ Process Mgr│
│            │
└────────────┘
```

Todos comparten un **contexto global** (`context/`) que funciona como su memoria colectiva, de modo que cada agente sabe qué han hecho los otros.

---

## 🚀 Inicio Rápido

### 1. Instalar MACS en tu proyecto

Copia la carpeta `agents/` a la raíz de tu proyecto:

```bash
# Desde la raíz de tu proyecto
cp -r /path/to/agents ./agents
```

### 2. Personalizar el contexto

Edita [context/project-brief.md](context/project-brief.md) con la información de tu proyecto. Es lo primero que leerá el Orquestador.

### 3. Activar el sistema

Abre tu proyecto con MiniMax M3 (Claude Code, API, SDK) y di:

> *"Activa el sistema MACS para el proyecto X"*

El Orquestador responderá con un resumen de lo que leyó y quedará listo.

### 4. Dar una tarea

> *"Necesito agregar autenticación con OAuth2 al proyecto"*

El Orquestador clasificará la tarea, la planificará y delegará a los agentes necesarios.

---

## 📁 Estructura

```
agents/
├── AGENTS.md                      ← Registro global (LEE PRIMERO)
├── orchestrator.md                ← Definición del Orquestador
├── README.md                      ← Este archivo
│
├── agents/                        ← Definición de cada agente
│   ├── tech-lead.md
│   ├── architect.md
│   ├── senior-dev.md
│   ├── qa-security.md
│   └── process-manager.md
│
├── context/                       ← Memoria compartida (append-only)
│   ├── shared-context.md          ← Bitácora de eventos
│   ├── active-plan.md             ← Plan en ejecución
│   ├── project-brief.md           ← Brief del proyecto
│   ├── architecture.md            ← Arquitectura actual
│   ├── decisions-log.md           ← ADRs (Architecture Decision Records)
│   └── lessons-learned.md         ← Memoria institucional
│
├── workflows/                     ← Flujos de trabajo
│   ├── standard-task.md           ← Features de 2-5 archivos
│   ├── complex-task.md            ← Features/refactors grandes
│   └── research-task.md           ← Investigación / descubrimiento
│
└── templates/                     ← Plantillas
    ├── agent-delegation.md
    ├── agent-output.md
    └── context-update.md
```

---

## 🧠 Los 6 Agentes

| # | Agente | Rol | Cuándo actúa |
|---|--------|-----|--------------|
| 1 | **Orquestador** | Coordina, planifica, sintetiza | **Siempre** (punto de entrada) |
| 2 | **Líder Técnico** | Estrategia técnica, trade-offs | Decisiones críticas, validación |
| 3 | **Arquitecto** | Estructura, stack, patrones | Proyectos nuevos, refactors, módulos |
| 4 | **Senior Dev** | Implementación de código | Toda tarea de código |
| 5 | **QA y Seguridad** | Tests + auditoría | Después de implementar |
| 6 | **Gestor de Procesos** | Flujo, dependencias, tracking | Tareas complejas, multi-fase |

> Los agentes no son procesos separados en runtime. Son **roles que MiniMax M3 adopta** siguiendo los prompts y formatos definidos en `agents/`.

---

## 🔄 Flujo Típico

```
Usuario: "Necesito agregar X feature"
    ↓
Orquestador: Clasifica, planifica, escribe active-plan.md
    ↓
Arquitecto: Diseña approach (5-10 min)
Líder Técnico: Valida approach (3-5 min)
    ↓
Senior Dev: Implementa + tests (15-45 min)
    ↓
QA y Seguridad: Valida funcional y seguridad (5-15 min)
    ↓
Orquestador: Sintetiza y entrega al usuario
    ↓
Gestor de Procesos: Cierra plan en decisions-log.md
```

---

## 📚 Cómo Usar

### Para tareas simples

> *"Arregla el typo en línea 42 de `src/foo.ts`"*

→ El Orquestador delega directo al Senior Dev. Sin orquestación completa.

### Para tareas medias

> *"Agrega un endpoint `GET /users/:id` con paginación"*

→ Activar [`workflows/standard-task.md`](workflows/standard-task.md).

### Para tareas complejas

> *"Migra el proyecto de CRA a Next.js App Router"*

→ Activar [`workflows/complex-task.md`](workflows/complex-task.md).

### Para investigación

> *"Investiga si，我们应该 usar Zustand o Redux Toolkit"*

→ Activar [`workflows/research-task.md`](workflows/research-task.md).

---

## 🌐 Integración con Skills, MCPs e Instrucciones externas

MACS es **agnóstico al proyecto**. Funciona con:

- ✅ **Skills** del sistema (Claude Code)
- ✅ **MCPs** configurados (Supabase, GitHub, etc.)
- ✅ **CLAUDE.md** del proyecto (se lee al inicio)
- ✅ **Copilot instructions** (.github/copilot-instructions.md)
- ✅ **Reportes de código** (lint, coverage, audit)
- ✅ **Documentación del proyecto** (README, docs/)

Todo esto se declara en [context/project-brief.md](context/project-brief.md) y el Orquestador lo respeta.

---

## 🎯 Principios (de Anthropic, adaptados a M3)

1. **Pensar como el agente** — simula antes de delegar.
2. **Delegación con contexto completo** — sin ambigüedad.
3. **Esfuerzo proporcional** — no usar 6 agentes para un typo.
4. **Herramientas importan** — verifica que existan y estén bien descritas.
5. **Mejora continua** — lessons-learned.md se actualiza siempre.
6. **Amplio → narrow** — primero panorama, luego detalle.
7. **Extended thinking** — explícate el "por qué" antes del "cómo".
8. **Paralelización agresiva** — 3-5 sub-agentes en paralelo cuando se pueda.

---

## 🔧 Personalización

Para adaptar MACS a tu proyecto:

1. Edita [context/project-brief.md](context/project-brief.md) con la info de tu proyecto.
2. Personaliza los workflows en `workflows/` si tu proceso es diferente.
3. Agrega skills específicas a `context/project-brief.md` sección 9.
4. Si agregas un nuevo rol, créalo en `agents/<nuevo-rol>.md` y regístralo en [AGENTS.md](AGENTS.md).

---

## 📜 Licencia

Uso personal / interno.

---

## 🙏 Créditos

- **Diseño base:** Anthropic — [Building a multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system)
- **Modelo host:** MiniMax M3 (Fable 5 / Opus 4.8 / Sonnet 4.6 / Haiku 4.5)
