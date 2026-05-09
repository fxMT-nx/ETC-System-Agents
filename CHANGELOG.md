# Changelog — ETC System Agents

Todos los cambios notables se documentan en este fichero.

---

## [1.0.0] — 2026-05-09 — Los 7 System Agents

### Agentes
- 🧭 **El Explorador** — Codebase Explorer (solo lectura)
- 🛠️ **El Operador** — General Executor con delegación inteligente
- 🔍 **El Investigador** — Web Researcher multicanal
- 📦 **El Instalador** — Package Installer multiplataforma
- 🎛️ **El Configurador** — System Configurator con backup automático
- 🔗 **El Integrador** — API Integrator con mínimo privilegio
- ⚖️ **El Supervisor** — Agent Router y resolución de conflictos

### Hooks
- **S1–S2:** El Explorador deriva a Operador e Investigador
- **S3–S8:** El Operador deriva a los 5 especialistas + Supervisor
- **S9–S10:** El Investigador deriva a Instalador y Operador
- **S11–S12:** El Instalador deriva a Investigador y Configurador
- **S13–S14:** El Configurador deriva a Operador e Instalador
- **S15–S18:** El Integrador deriva a Instalador, Configurador, Investigador y Operador
- **C54–C56:** Hooks compartidos con ETC (investigación web, documentación, handoff con auditoría)
- **Total: 24 hooks** (S1–S18, C54–C56)

### Reglas de delegación
- 18 reglas obligatorias (DEBES en vez de considera)
- Protocolo de Handoff con Auditoría en los 7 agentes

### Documentación
- `docs/conflict-resolution.md`: tabla de soberanía y 4 conflictos pre-cocinados
- `tests/hooks.md`: 20 escenarios de validación para hooks
- `README.md` completo con 542 líneas, tablas de colaboración y guía de instalación
- `CHANGELOG.md` con historial de versiones

### Infraestructura
- `opencode.json` con allowlist de skills y `"*": "deny"`
- `prompts/global-instructions.md` con los 14 agentes (system + ETC)
- `prompts/orchestrator.md` con mapa de delegación unificado
- `.github/workflows/validate-system-structure.yml`: validación automática de estructura

### Skills complementarias
- `firecrawl-scraper`: scraping web a Markdown
- `github-research`: búsqueda en GitHub Issues/PRs
- `stackoverflow-research`: búsqueda en Stack Overflow
- `docs-verifier`: verificación contra documentación oficial

---

## [0.1.0] — 2026-05-08 — Pre-release

### Agentes
- Versión inicial con los 7 agentes del sistema funcionales
- `@explore` y `@general` deshabilitados en favor de los system agents

### Configuración
- `opencode.json` con agentes configurados y permisos básicos
- `prompts/global-instructions.md` con lista de 14 agentes
- `prompts/orchestrator.md` con mapa de delegación

### Integración
- Integración básica con ETC — El Septeto Calavera
- `README.md` inicial con tabla de agentes y guía de instalación

---

## Origen

- Skills de investigación: [firecrawl-scraper](https://github.com/nicholasgriffintn/skills), [github-research](https://github.com/mattpocock/skills)
- Inspiración para el sistema de agentes: [ETC — El Septeto Calavera](https://github.com/felixmoto44-spec/ETC-El-Septeto-Calavera)
- Todos los agentes: diseñados desde cero para ETC System Agents
