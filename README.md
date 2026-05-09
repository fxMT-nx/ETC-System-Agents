# 🛠️ ETC System Agents

7 agentes del sistema para [OpenCode](https://opencode.ai) que reemplazan a `@explore` y `@general`. Cada agente tiene un dominio estricto: exploración, operación, investigación web, instalación, configuración, integración y supervisión.

> **14 agentes en total**: estos 7 System Agents + los 7 [ETC — El Septeto Calavera](https://github.com/felixmoto44-spec/ETC-El-Septeto-Calavera) (Maestro, Bug Doctor, El de las Gafas, Las Manos, El Pintor, El Herrero, El Árbitro) forman el ecosistema completo ETC.

## Los 7 Agentes del Sistema

| # | Agente | Archivo | Rol | Cuándo usarlo |
|---|--------|---------|-----|---------------|
| 1 | 🧭 **El Explorador** | `el-explorador.md` | Exploración rápida de codebases (solo lectura) | Necesitas entender un proyecto, buscar archivos, o explorar código sin modificarlo |
| 2 | 🛠️ **El Operador** | `el-operador.md` | Ejecutor general con delegación inteligente | Tarea general que no encaja en los otros agentes; sabe delegar a especialistas |
| 3 | 🔍 **El Investigador** | `el-investigador.md` | Búsqueda web y verificación de información | Necesitas info actualizada de internet, documentación, o resolver dudas técnicas |
| 4 | 📦 **El Instalador** | `el-instalador.md` | Instalación de paquetes y herramientas | Necesitas instalar algo en el sistema: paquetes, CLIs, dependencias |
| 5 | 🎛️ **El Configurador** | `el-configurador.md` | Configuración del sistema y dotfiles | Necesitas modificar configs, variables de entorno, o ajustar settings |
| 6 | 🔗 **El Integrador** | `el-integrador.md` | Integración de APIs y servicios externos | Necesitas conectar APIs, OAuth, webhooks, o gestionar credenciales |
| 7 | ⚖️ **El Supervisor** | `el-supervisor.md` | Router de tareas y resolución de conflictos | No sabes qué agente invocar o dos agentes están en conflicto |

## Principios del Sistema

- **Cada agente sabe lo que sabe**: dominios estrictos, nada de "yo también puedo"
- **Delegación obligatoria**: si la tarea no es de tu dominio, DEBES delegar
- **Auditoría**: el que delega es responsable del resultado final
- **Formato unificado**: `frontmatter` con `description` y `mode: subagent` + markdown completo

## Cómo se Usan

| Método | Sintaxis | Ejemplo |
|--------|----------|---------|
| **@mención** | `@el-investigador` | `@el-investigador busca documentación de la API de Stripe` |
| **Lenguaje natural** | Describir la tarea | `Necesito instalar Node.js 20` → El Supervisor enruta al Instalador |

Los agentes se invocan por `@` en OpenCode. Si no sabes cuál usar, invoca a **El Supervisor** (`@el-supervisor`) que analizará la tarea y la derivará al agente correcto.

### Cómo se Integran con ETC — El Septeto Calavera

Los **7 System Agents** se enfocan en tareas del sistema operativo, investigación web, instalación y configuración. Los **7 ETC** se enfocan en desarrollo de software: TDD, debugging, dominio, infraestructura, frontend, backend y arbitraje.

```
System Agents (sistema/ops)          ETC Septeto (desarrollo)
─────────────────────────────        ─────────────────────────
🧭 Explorador    → solo lectura      🧪 Maestro         → TDD
🛠️ Operador      → ejecutor general   🩺 Bug Doctor      → debugging
🔍 Investigador  → búsqueda web       🤓 El de las Gafas → dominio
📦 Instalador    → paquetes           🖐️ Las Manos        → infraestructura
🎛️ Configurador  → configs            🎨 El Pintor       → frontend
🔗 Integrador    → APIs externas      ⚒️ El Herrero       → backend
⚖️ Supervisor    → router + conflictos ⚖️ El Árbitro      → conflictos ETC
```

## Instalación

Los agentes se instalan en `~/.config/opencode/agents/`:

```bash
cp .opencode/agents/*.md ~/.config/opencode/agents/
```

Si también usas [ETC — El Septeto Calavera](https://github.com/felixmoto44-spec/ETC-El-Septeto-Calavera), tendrás 14 agentes disponibles en tu OpenCode.

## Estructura

```
.opencode/
├── agents/
│   ├── el-explorador.md      # 🧭 Codebase Explorer
│   ├── el-operador.md         # 🛠️ General Executor
│   ├── el-investigador.md     # 🔍 Web Researcher
│   ├── el-instalador.md       # 📦 Package Installer
│   ├── el-configurador.md     # 🎛️ System Configurator
│   ├── el-integrador.md       # 🔗 API Integrator
│   └── el-supervisor.md       # ⚖️ Agent Router
prompts/
├── global-instructions.md
└── orchestrator.md
opencode.json
```

## Proyecto Hermano

[**ETC — El Septeto Calavera**](https://github.com/felixmoto44-spec/ETC-El-Septeto-Calavera) — los 7 agentes de desarrollo (TDD, debugging, dominio, infra, frontend, backend, arbitraje) que completan el ecosistema de 14 agentes.

## Licencia

MIT
