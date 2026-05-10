# 🛠️ ETC System Agents — Los 7 Agentes del Sistema

Configuración de agentes para [OpenCode](https://opencode.ai), el entorno de codificación con IA. Este repo alberga **ETC System Agents**, siete agentes especializados del sistema operativo que reemplazan a `@explore` y `@general`, más skills complementarias de investigación web y scraping.

> _«Mientras los calaveras desarrollan, los system agents preparan el terreno.»_

## 🛠️ Los 7 System Agents

| # | System | Agente | Rol | Frase |
|---|--------|--------|-----|-------|
| 1 | 🧭 | **El Explorador** | Codebase Explorer | _"Leer antes de escribir, entender antes de modificar."_ |
| 2 | 🛠️ | **El Operador** | General Executor | _"Puedo hacerlo, pero quizás no debería."_ |
| 3 | 🔍 | **El Investigador** | Web Researcher | _"Tres fuentes o no es verdad."_ |
| 4 | 📦 | **El Instalador** | Package Installer | _"Primero verifica compatibilidad, luego instala."_ |
| 5 | 🎛️ | **El Configurador** | System Configurator | _"Backup antes de tocar, verifica después de cambiar."_ |
| 6 | 🔗 | **El Integrador** | API Integrator | _"Mínimo privilegio, máxima seguridad."_ |
| 7 | ⚖️ | **El Supervisor** | Agent Router | _"El agente correcto para la tarea correcta."_ |

---

### Permisos de ejecución (bash)

| Agente | Bash | Puede ejecutar |
|--------|:----:|----------------|
| 🧪 **El Maestro** | ✅ Allow | Tests, git commands, scripts de build |
| 🩺 **Bug Doctor** | ✅ Allow | Debuggers, logs, herramientas de diagnóstico |
| 🤓 **El de las Gafas** | ✅ Allow | Exploración del codebase, documentación |
| 🖐️ **Las Manos** | ✅ Allow | Instalación, CI/CD, Docker, comandos de sistema |
| 🎨 **El Pintor** | ✅ Allow | Dev servers, build tools, npm/pip |
| ⚒️ **El Herrero** | ✅ Allow | Migraciones, tests de API, queries de DB |
| ⚖️ **El Árbitro** | ❌ **Deny** | Solo decide y delega. No ejecuta nada. |
| 🧭 **El Explorador** | ✅ Allow | grep, find, git log (solo lectura) |
| 🛠️ **El Operador** | ✅ Allow | Scripts, automatización, tareas generales |
| 🔍 **El Investigador** | ✅ Allow | curl, lynx, html2text, investigación web |
| 📦 **El Instalador** | ✅ Allow | apt, npm, pip, brew, instalación de paquetes |
| 🎛️ **El Configurador** | ✅ Allow | Modificar configs, dotfiles, variables de entorno |
| 🔗 **El Integrador** | ✅ Allow | Configurar APIs, OAuth, webhooks, cuentas |
| ⚖️ **El Supervisor** | ❌ **Deny** | Solo enruta tareas. No ejecuta nada. |

> **Nota:** Los agentes con `bash: deny` (Árbitro, Supervisor) solo pueden leer archivos, cargar skills, invocar a otros agentes y preguntar al usuario. No pueden ejecutar ningún comando ni modificar archivos.

---

### 🧭 El Explorador — Codebase Explorer

Especialista en exploración rápida de codebases. Busca archivos, entiende estructuras de proyectos, encuentra código rápidamente. **Solo lectura** — nunca modifica archivos. Como un bibliotecario que conoce cada rincón de la estantería.

**Principio:** "Lee primero, pregunta después."

**Origen:** Diseñado desde cero para ETC System Agents.

### 🛠️ El Operador — General Executor

Ejecutor general del sistema. Corre scripts, modifica archivos, automatiza tareas, y sabe delegar a los especialistas cuando la tarea no es de su dominio. Su regla de oro: "Si otro agente lo haría mejor, delega."

**Principio:** "Puedo hacerlo, pero quizás no debería."

**Origen:** Diseñado desde cero para ETC System Agents.

### 🔍 El Investigador — Web Researcher

Especialista en búsqueda web, scraping de documentación, y verificación de información técnica. Busca en internet, extrae contenido de páginas, verifica datos contra fuentes oficiales. No se conforma con el primer resultado — cruza fuentes, verifica vigencia, y presenta un panorama completo con nivel de confianza.

Incluye un **canal de búsqueda multicanal:** documentación oficial, GitHub Issues, Stack Overflow, foros y source code.

**Principio:** "Tres fuentes o no es verdad."

**Origen:** Diseñado desde cero para ETC System Agents, integrando skills `firecrawl-scraper`, `github-research`, `stackoverflow-research`, `docs-verifier`.

### 📦 El Instalador — Package Installer

Experto en instalación de paquetes y herramientas del sistema. Sabe qué instalar, cómo, y con qué configuración según el SO y las particularidades del entorno. Detecta el sistema operativo, elige el mejor método de instalación (apt, dnf, pacman, brew, npm, pip, cargo, go, curl|bash, Docker), verifica compatibilidad, y confirma con `--version`.

**Principio:** "Primero verifica compatibilidad, luego instala."

**Origen:** Diseñado desde cero para ETC System Agents.

### 🎛️ El Configurador — System Configurator

Especialista en configuraciones del sistema. Sabe dónde van los archivos de configuración en cada SO (Linux, macOS), cómo hacer backups con timestamp, y cómo no romper nada cuando ajusta un setting. Gestiona dotfiles, variables de entorno, archivos de config de aplicaciones, y settings del SO. Cada cambio es seguro, reversible, y documentado con `diff`.

**Principio:** "Backup antes de tocar, verifica después de cambiar."

**Origen:** Diseñado desde cero para ETC System Agents.

### 🔗 El Integrador — API Integrator

Experto en conectar sistemas con servicios externos. Sabe configurar OAuth 2.0, API keys, webhooks, cuentas de servicio (Supabase, Google Cloud, Stripe, GitHub, AWS, n8n, OpenRouter) con seguridad y precisión. Sigue el principio de mínimo privilegio: nunca da más permisos de los necesarios.

Incluye un **flujo de 6 fases:** diagnóstico inicial, investigación del mejor método de autenticación, backup de credenciales previas, ejecución con permisos mínimos, almacenamiento seguro en `.env` con `chmod 600`, y verificación con prueba de conectividad real.

**Principio:** "Mínimo privilegio, máxima seguridad."

**Origen:** Diseñado desde cero para ETC System Agents.

### ⚖️ El Supervisor — Agent Router

Agente que decide. Cuando los demás no saben quién debe actuar, él decide. Cuando dos agentes discrepan, él resuelve. No ejecuta — dirige. Aplica el mapa de decisiones (exploración → Explorador, ejecución → Operador, investigación → Investigador, instalación → Instalador, configuración → Configurador, integración → Integrador) y la regla del 80% para tareas mixtas.

**Principio:** "El agente correcto para la tarea correcta."

**Origen:** Diseñado desde cero para ETC System Agents.

---

## 🤝 Colaboración entre Agentes

Los 7 System Agents no trabajan en aislamiento — se invocan entre sí automáticamente según el contexto. Hay **24 hooks de colaboración** (S1–S18, C54–C61) documentados en sus instrucciones.

Además, los 7 agentes incorporan un **Protocolo de Handoff con Auditoría**: cuando reciben una tarea fuera de su especialidad, la delegan al agente correcto con todo el contexto, auditan el resultado contra lo que pidió el usuario, y son responsables de la entrega final.

> _«El Explorador lee, el Operador ejecuta, el Investigador busca, el Instalador prepara, el Configurador ajusta, el Integrador conecta. El Supervisor decide quién hace qué. El que no delega cuando debe, entrega peor.»_

### El patrón: Explorar → Ejecutar → Investigar → Instalar → Configurar → Integrar

Cada agente tiene un rol primario claro, y cuando detecta que está fuera de su especialidad, deriva al colega adecuado:

| Agente | Rol primario | Deriva a... |
|--------|-------------|-------------|
| 🧭 **Explorador** | Explorar codebases (solo lectura) | 🛠️ Operador (modificar), 🔍 Investigador (tecnología) |
| 🛠️ **Operador** | Ejecución general | 🧭 Explorador (explorar), 🔍 Investigador (web), 📦 Instalador (paquetes), 🎛️ Configurador (config), 🔗 Integrador (APIs), ⚖️ Supervisor (ruta) |
| 🔍 **Investigador** | Búsqueda web y verificación | 📦 Instalador (instalar tools), 🛠️ Operador (implementar hallazgos) |
| 📦 **Instalador** | Instalación de paquetes | 🔍 Investigador (métodos alternativos), 🎛️ Configurador (post-instalación) |
| 🎛️ **Configurador** | Configuración del sistema | 🛠️ Operador (reiniciar servicios), 📦 Instalador (validadores) |
| 🔗 **Integrador** | Integración de APIs externas | 📦 Instalador (CLIs), 🎛️ Configurador (credenciales), 🔍 Investigador (docs API), 🛠️ Operador (cambios en código) |
| ⚖️ **Supervisor** | Decidir ruta, resolver conflictos | Usuario (tarea irresoluble) |

### Los 24 hooks de colaboración (S1–S18, C54–C61)

#### Hooks S1–S2: El Explorador deriva

| # | Inicia | Gatillo | Invoca a | Resultado |
|---|--------|---------|----------|-----------|
| S1 | 🧭 Explorador | Encuentra código que necesita ser modificado | 🛠️ Operador | Código modificado con ruta exacta y contexto |
| S2 | 🧭 Explorador | Encuentra tecnología desconocida en el codebase | 🔍 Investigador | Tecnología investigada y documentada |

#### Hooks S3–S8: El Operador deriva

| # | Inicia | Gatillo | Invoca a | Resultado |
|---|--------|---------|----------|-----------|
| S3 | 🛠️ Operador | Tarea requiere entender estructura de código primero | 🧭 Explorador | Codebase explorado antes de modificar |
| S4 | 🛠️ Operador | Necesita información actualizada de internet | 🔍 Investigador | Información investigada con fuentes verificadas |
| S5 | 🛠️ Operador | Necesita instalar paquetes/herramientas | 📦 Instalador | Paquete instalado y verificado |
| S6 | 🛠️ Operador | Necesita modificar configuraciones del sistema | 🎛️ Configurador | Configuración ajustada con backup y verificación |
| S7 | 🛠️ Operador | Necesita conectar APIs o servicios externos | 🔗 Integrador | API integrada con mínimo privilegio |
| S8 | 🛠️ Operador | No sabe qué agente debe actuar o hay ambigüedad | ⚖️ Supervisor | Ruta de ejecución determinada |

#### Hooks S9–S10: El Investigador deriva

| # | Inicia | Gatillo | Invoca a | Resultado |
|---|--------|---------|----------|-----------|
| S9 | 🔍 Investigador | Investigación revela herramienta que debe instalarse | 📦 Instalador | Herramienta instalada para continuar investigación |
| S10 | 🔍 Investigador | Hallazgo de investigación listo para implementar | 🛠️ Operador | Hallazgo implementado en el sistema |

#### Hooks S11–S12: El Instalador deriva

| # | Inicia | Gatillo | Invoca a | Resultado |
|---|--------|---------|----------|-----------|
| S11 | 📦 Instalador | Método de instalación no es obvio, necesita investigación | 🔍 Investigador | Método de instalación investigado y documentado |
| S12 | 📦 Instalador | Post-instalación requiere cambios de configuración | 🎛️ Configurador | Configuración ajustada post-instalación |

#### Hooks S13–S14: El Configurador deriva

| # | Inicia | Gatillo | Invoca a | Resultado |
|---|--------|---------|----------|-----------|
| S13 | 🎛️ Configurador | Cambio de configuración requiere reiniciar un servicio | 🛠️ Operador | Servicio reiniciado y verificado |
| S14 | 🎛️ Configurador | Necesita una herramienta para validar la configuración | 📦 Instalador | Validador instalado y ejecutado |

#### Hooks S15–S18: El Integrador deriva

| # | Inicia | Gatillo | Invoca a | Resultado |
|---|--------|---------|----------|-----------|
| S15 | 🔗 Integrador | Necesita un CLI tool para interactuar con el servicio | 📦 Instalador | CLI instalado y verificado |
| S16 | 🔗 Integrador | Credenciales deben guardarse en archivo de configuración | 🎛️ Configurador | Credenciales almacenadas de forma segura |
| S17 | 🔗 Integrador | Necesita documentación actualizada de la API | 🔍 Investigador | Documentación de API obtenida y verificada |
| S18 | 🔗 Integrador | Integración requiere cambios en el código del proyecto | 🛠️ Operador | Código modificado para soportar la integración |

#### Hooks compartidos con ETC (C54–C61)

| # | Inicia | Gatillo | Invoca a | Resultado |
|---|--------|---------|----------|-----------|
| C54 | Cualquier agente | Necesita buscar información actualizada en internet | 🔍 Investigador | Investigación multicanal con resultados comparados y nivel de confianza |
| C55 | 🔍 Investigador | Investigación revela información relevante para el equipo | ✍️ Investigador | Mini-ADR o nota documentada en el proyecto |
| C56 | Cualquiera | Agente delegó tarea y especialista reportó resultado | Agente que delegó | Auditoría: ¿cumple lo que pidió el usuario? Si no → ajustes o arbitraje |
| C60 | Cualquier agente | ≥ 3 iteraciones sin progreso, o > 30 min sin output verificable | 🩺 Bug Doctor (ETC) | Diagnóstico de atasco: ¿bug, mal enfoque, o bloqueo externo? |
| C61 | Cualquier agente | ≥ 3 errores distintos en la misma sesión | 🩺 Bug Doctor (ETC) | Diagnóstico de causa raíz antes de seguir parcheando |

### Reglas de Delegación Obligatoria

Cada agente tiene reglas duras de delegación — no sugerencias, sino checkpoints obligatorios:

| Agente | Regla | Disparador |
|--------|-------|------------|
| 🧭 Explorador | → Operador | Encuentra código que necesita modificación |
| 🧭 Explorador | → Investigador | Tecnología desconocida en el codebase |
| 🛠️ Operador | → Explorador | Necesita entender estructura antes de modificar |
| 🛠️ Operador | → Investigador | Tarea requiere búsqueda web |
| 🛠️ Operador | → Instalador | Tarea requiere instalar paquetes |
| 🛠️ Operador | → Configurador | Tarea requiere modificar configuraciones |
| 🛠️ Operador | → Integrador | Tarea requiere conectar APIs externas |
| 🛠️ Operador | → Supervisor | Tarea ambigua o fuera de alcance |
| 🔍 Investigador | → Instalador | Investigación requiere instalar herramienta |
| 🔍 Investigador | → Operador | Hallazgo listo para implementar |
| 📦 Instalador | → Investigador | Método de instalación no obvio |
| 📦 Instalador | → Configurador | Post-instalación requiere configuración |
| 🎛️ Configurador | → Operador | Cambio requiere reiniciar servicio |
| 🎛️ Configurador | → Instalador | Necesita validador/herramienta |
| 🔗 Integrador | → Instalador | Necesita CLI tool |
| 🔗 Integrador | → Configurador | Credenciales en archivo de configuración |
| 🔗 Integrador | → Investigador | Documentación de API necesaria |
| 🔗 Integrador | → Operador | Integración requiere cambios en código |
| 🔗 Integrador | → Supervisor | Conflicto de permisos o alcance |
| ⚖️ Supervisor | → Usuario | Tarea irresoluble o fuera del alcance de todos los agentes |
| 🧭🛠️🔍📦🎛️🔗 **Todos** | **Responsabilidad del handoff** | **Al delegar, auditas y respondes por el resultado final** |

### Ciclos compuestos — cuando los hooks se encadenan

#### 🧭🛠️ "Explorar → Modificar" (S1→S3)

```
S1: Explorador → Operador ("encontré código que necesita cambios en src/config.js:42")
 ↓
S3: Operador → Explorador ("antes de modificar, necesito entender la estructura completa")
 ↓
Explorador reporta el contexto completo
 ↓
Operador ejecuta la modificación y verifica
```

#### 🔍📦🛠️ "Investigar → Instalar → Implementar" (S4→S9→S10→S5)

```
S4: Operador → Investigador ("necesito la última versión de Node.js y cómo instalarla")
 ↓
S9: Investigador → Instalador ("encontré que necesitamos nvm. Instálalo primero")
 ↓
Instalador instala nvm y Node.js 20 y verifica con `node --version`
 ↓
S10: Investigador → Operador ("Node.js 20 listo. Aquí la guía de migración")
 ↓
Operador implementa los cambios necesarios
```

#### 🔗📦🎛️ "Integrar API externa" (S7→S15→S16→S17→S18)

```
S7: Operador → Integrador ("necesito conectar Stripe para pagos")
 ↓
S15: Integrador → Instalador ("necesito stripe CLI para pruebas locales")
 ↓
S17: Integrador → Investigador ("necesito la última documentación de Stripe Checkout")
 ↓
S16: Integrador → Configurador ("guarda las API keys en .env con chmod 600")
 ↓
S18: Integrador → Operador ("la integración requiere crear webhook handler en api/stripe.ts")
```

#### ⚖️🛠️ "Supervisor resuelve ambigüedad" (S8→ejecución)

```
S8: Operador → Supervisor ("el usuario pidió 'prepara el entorno', no sé si es instalar,
                              configurar o integrar algo")
 ↓
Supervisor analiza: "El usuario necesita Node.js 20 + variables de entorno + Stripe"
 ↓
Fase 1: 📦 Instalador (Node.js + dependencias)
Fase 2: 🎛️ Configurador (.env con variables)
Fase 3: 🔗 Integrador (Stripe API keys)
```

---

## 📁 Estructura de Archivos

```
tu-proyecto/
├── .opencode/
│   ├── agents/                     # 7 agentes del sistema
│   │   ├── el-explorador.md        # 🧭 Codebase Explorer
│   │   ├── el-operador.md          # 🛠️ General Executor
│   │   ├── el-investigador.md      # 🔍 Web Researcher
│   │   ├── el-instalador.md        # 📦 Package Installer
│   │   ├── el-configurador.md      # 🎛️ System Configurator
│   │   ├── el-integrador.md        # 🔗 API Integrator
│   │   └── el-supervisor.md        # ⚖️ Agent Router
│   └── skills/                     # Skills complementarias
│       ├── firecrawl-scraper/SKILL.md
│       ├── github-research/SKILL.md
│       ├── stackoverflow-research/SKILL.md
│       └── docs-verifier/SKILL.md
├── docs/
│   └── conflict-resolution.md      # Protocolo de resolución de conflictos
├── tests/
│   └── hooks.md                    # Tests de validación de hooks
├── prompts/
│   ├── global-instructions.md      # Instrucciones globales (14 agentes)
│   └── orchestrator.md             # Orquestador unificado
├── CHANGELOG.md                    # Historial de versiones
├── opencode.json                   # Configuración de OpenCode
└── README.md                       # Este archivo
```

---

## 🎯 Cómo se Usan

| Método | Sintaxis | Aplica a | Ejemplo |
|--------|----------|----------|---------|
| **@mención** | `@el-investigador` | Agents | `@el-investigador busca documentación de la API de Stripe` |
| **/comando** | `/github-research` | Skills | `/firecrawl-scraper https://docs.example.com` |
| **Lenguaje natural** | Describir la tarea | Cualquiera | "Necesito instalar Node.js 20" → El Supervisor enruta al Instalador |

---

## 📦 Cómo Replicar Esto en Tu Proyecto

```bash
# Clonar este repo
git clone <this-repo> /tmp/etc-system

# Copiar agents y prompts a tu proyecto
cp /tmp/etc-system/.opencode/agents/* tu-proyecto/.opencode/agents/
cp /tmp/etc-system/prompts/* tu-proyecto/prompts/
cp /tmp/etc-system/opencode.json tu-proyecto/

# (Opcional) Copiar skills
cp -r /tmp/etc-system/.opencode/skills/* tu-proyecto/.opencode/skills/

# (Opcional) Copiar documentación
cp -r /tmp/etc-system/docs/* tu-proyecto/docs/
cp -r /tmp/etc-system/tests/* tu-proyecto/tests/
```

### Disponibilidad Global

Para tener los System Agents disponibles en TODOS tus proyectos de OpenCode:

```bash
# Copiar agents a la configuración global
cp .opencode/agents/*.md ~/.config/opencode/agents/

# Copiar prompts globales
cp prompts/global-instructions.md ~/.config/opencode/prompts/

# Copiar skills
cp -r .opencode/skills/* ~/.config/opencode/skills/
```

### Configuración necesaria en opencode.json

El archivo `opencode.json` de este proyecto ya incluye toda la configuración necesaria:

```json
{
  "instructions": ["prompts/global-instructions.md"],
  "agent": {
    "explore": { "disable": true },
    "general": { "disable": true },
    "build": {
      "prompt": "{file:./prompts/orchestrator.md}",
      "permission": {
        "edit": "deny", "bash": "deny",
        "task": "allow",
        "skill": "allow"
      }
    },
    "plan": {
      "prompt": "{file:./prompts/orchestrator.md}",
      "permission": {
        "edit": "deny", "bash": "deny",
        "task": "allow",
        "skill": "allow"
      }
    }
  }
}
```

**Qué hace cada cosa:**
- `instructions`: Aplica las reglas globales a todos los agentes (14 agentes, clarificación de requisitos, delegación con auditoría)
- `explore { disable: true }`: Desactiva el agente explorador nativo de OpenCode. Lo reemplazamos con `@el-explorador`
- `general { disable: true }`: Desactiva el agente general nativo. Lo reemplazamos con `@el-operador` y el resto del septeto
- `build` y `plan` con `edit: deny, bash: deny`: Actúan como orquestadores. No ejecutan nada directamente — solo analizan y delegan a los agentes del sistema mediante Task tool

> **Importante**: Si solo copias los agentes sin esta configuración, `@explore` y `@general` seguirán apareciendo y Build/Plan intentarán ejecutar ellos mismos las tareas. La configuración del `opencode.json` es TAN importante como los agentes.

### Herramientas de investigación

@el-investigador usa herramientas nativas del sistema para investigar en internet:

| Herramienta | Instalación | Coste |
|-------------|-------------|-------|
| `lynx` | `sudo apt install lynx` | ✅ Gratis |
| `html2text` | `pip install html2text` | ✅ Gratis |
| `curl` | Viene con el SO | ✅ Gratis |
| `jq` | `sudo apt install jq` | ✅ Gratis |

Sin API keys, sin cuentas, sin configuraciones.
Si necesitas firecrawl (opcional, con API key), se puede instalar con `npm install -g firecrawl`.

---

## 🤝 Colaboración con ETC — El Septeto Calavera

Los **7 System Agents** + **7 ETC** = **14 agentes** que cubren cualquier tarea que puedas pedirle a OpenCode.

```
System Agents (sistema/ops)          ETC Septeto (desarrollo)
─────────────────────────────        ─────────────────────────
🧭 Explorador    → solo lectura      🧪 Maestro         → TDD
🛠️ Operador      → ejecutor general   🩺 Bug Doctor      → debugging
🔍 Investigador  → búsqueda web       🤓 El de las Gafas → dominio + investigación
📦 Instalador    → paquetes           🖐️ Las Manos        → infraestructura
🎛️ Configurador  → configs            🎨 El Pintor       → frontend
🔗 Integrador    → APIs externas      ⚒️ El Herrero       → backend
⚖️ Supervisor    → router + conflictos ⚖️ El Árbitro      → conflictos ETC
```

**Cómo colaboran entre sistemas:**

| System Agent | Colabora con ETC | Escenario |
|--------------|-----------------|-----------|
| 🧭 **Explorador** | 🧪 **Maestro** | Explorar codebase antes de que el Maestro inicie un ciclo TDD |
| 🛠️ **Operador** | 🧪 **Maestro**, 🩺 **Bug Doctor** | Ejecutar scripts de setup, migraciones, o automatización que el Maestro necesita |
| 🔍 **Investigador** | 🤓 **Gafas**, ⚒️ **Herrero** | Investigar documentación de APIs, librerías, o tecnologías para el desarrollo |
| 📦 **Instalador** | 🖐️ **Manos**, 🎨 **Pintor**, ⚒️ **Herrero** | Instalar dependencias del proyecto que los agentes de ETC necesitan |
| 🎛️ **Configurador** | 🖐️ **Manos** | Configurar variables de entorno, dotfiles, y settings para el entorno de desarrollo |
| 🔗 **Integrador** | ⚒️ **Herrero**, 🖐️ **Manos** | Configurar APIs externas (Stripe, Supabase, GitHub OAuth) que el backend necesita |
| ⚖️ **Supervisor** | ⚖️ **Árbitro** | Escalar conflictos complejos entre los 14 agentes |

Cuando tengas los 14 agentes instalados, puedes hacer:

```
# Pedidos de sistema
@el-explorador explora la estructura del proyecto
@el-investigador busca la última versión de React
@el-instalador instala las dependencias del proyecto

# Pedidos de desarrollo
@el-maestro implementa el login con TDD
@bug-doctor diagnostica el error 500
@el-herrero diseña el schema de la base de datos

# El flujo completo
"Quiero añadir pagos con Stripe al proyecto"
→ El Supervisor (System) lo divide:
   🔗 Integrador configura Stripe
   ⚒️ Herrero diseña el endpoint de pagos
   🧪 Maestro implementa con TDD
   🖐️ Manos despliega a producción
```

---

## 🧩 Proyecto Hermano

[**ETC — El Septeto Calavera**](https://github.com/felixmoto44-spec/ETC-El-Septeto-Calavera) — los 7 agentes de desarrollo (TDD, debugging, dominio, infra, frontend, backend, arbitraje) que completan el ecosistema de 14 agentes.

Mientras **ETC System Agents** se enfoca en tareas del sistema operativo (exploración, operación, investigación web, instalación, configuración, integración, supervisión), **ETC — El Septeto Calavera** se enfoca en desarrollo de software (TDD, debugging, dominio, infraestructura, frontend, backend, arbitraje).

**Juntos forman 14 agentes** que cubren cualquier tarea que puedas pedirle a OpenCode. Instala ambos proyectos en `~/.config/opencode/agents/` para tener el ecosistema completo.

---

## 📋 Changelog

### v1.0.0 — Los 7 System Agents (2026-05-09)

- 7 agentes del sistema creados: 🧭 Explorador, 🛠️ Operador, 🔍 Investigador, 📦 Instalador, 🎛️ Configurador, 🔗 Integrador, ⚖️ Supervisor
- 24 hooks de colaboración (S1–S18, C54–C61)
- 18 reglas de delegación obligatoria entre system agents
- Protocolo de Handoff con Auditoría (C56)
- Hooks C54–C55 compartidos con ETC para investigación web y documentación
- `docs/conflict-resolution.md` con tabla de soberanía y 4 conflictos pre-cocinados
- `tests/hooks.md` con 20 escenarios de validación
- `prompts/global-instructions.md` con los 14 agentes (system + ETC)
- `prompts/orchestrator.md` con mapa de delegación unificado
- `opencode.json` con allowlist de skills y `"*": "deny"`
- README completo con 7 agentes, colaboración y guía de instalación

### v0.1.0 — Pre-release (2026-05-08)

- Versión inicial con los 7 agentes del sistema funcionales
- `@explore` y `@general` deshabilitados en favor de los system agents
- Integración básica con ETC — El Septeto Calavera

---

## Licencia

MIT — Inspirado en [morodomi/tdd-skills](https://github.com/morodomi/tdd-skills), [mattpocock/skills](https://github.com/mattpocock/skills), y [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills).
