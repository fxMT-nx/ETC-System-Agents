# ETC-System-Agents

Sistema de 7 agentes especializados para tareas del sistema operativo, configuración, y mantenimiento. Cada agente es un subagente autónomo con un dominio específico.

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

## Instalación

Los agentes se instalan en `~/.config/opencode/agents/`:

```bash
cp .opencode/agents/*.md ~/.config/opencode/agents/
```

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

## Licencia

MIT
