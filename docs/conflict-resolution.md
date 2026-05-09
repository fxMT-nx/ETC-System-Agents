# Protocolo de resolución de conflictos entre System Agents

> **Implementado por ⚖️ El Supervisor**, el séptimo agente del sistema. Ante cualquier conflicto, los agentes invocan a El Supervisor quien aplica este protocolo para resolver disputas con decisión vinculante.

## Principio fundamental

Cada agente tiene soberanía en su dominio. Los conflictos ocurren cuando dos dominios se solapan. Este documento define quién tiene la última palabra en cada tipo de conflicto.

## Tabla de soberanía por dominio

| Dominio | Agente soberano | Razón |
|---------|----------------|-------|
| Exploración de codebases (solo lectura) | 🧭 El Explorador | Especialista en búsqueda y comprensión de código |
| Ejecución general, scripts, automatización | 🛠️ El Operador | Ejecutor general del sistema |
| Investigación web, verificación de información | 🔍 El Investigador | Metodología multicanal |
| Instalación de paquetes y herramientas | 📦 El Instalador | Experto en gestores de paquetes y SO |
| Configuración del sistema y dotfiles | 🎛️ El Configurador | Backup, sintaxis, y reversibilidad |
| Integración de APIs y servicios externos | 🔗 El Integrador | Mínimo privilegio, máxima seguridad |
| Decisión de ruta y asignación de tareas | ⚖️ El Supervisor | Árbitro del sistema |

## Conflictos conocidos y su resolución

### Conflicto 1: ¿Quién instala y quién configura?

**Situación:** El Instalador descarga Node.js 20 pero la instalación requiere configurar `~/.npmrc` y variables de entorno.

**Resolución:** El Instalador instala el paquete (soberanía de instalación). Luego deriva al Configurador (hook S12) para los cambios post-instalación. El Instalador verifica que el binario funciona (`node --version`) antes de pasar la posta. El Configurador hace backup del `.npmrc` actual antes de modificarlo.

**Regla general:** Instalación ≠ Configuración. El Instalador pone el binario en el sistema. El Configurador ajusta los archivos de configuración. Ambos verifican.

---

### Conflicto 2: ¿El Integrador o el Operador modifica el código?

**Situación:** El Integrador necesita crear un archivo `api/stripe.ts` para el webhook handler de Stripe. El Operador considera que modificar código es su dominio.

**Resolución:** El Integrador diseña la integración (qué debe hacer el webhook, qué credenciales necesita, qué endpoints llamar). Luego deriva al Operador (hook S18) para que implemente los cambios en el código. El Integrador audita que el código implementado coincida con la integración diseñada.

**Regla general:** El Integrador decide qué se necesita conectar. El Operador ejecuta los cambios en el código. El Integrador verifica que la conexión funcione.

---

### Conflicto 3: ¿El Investigador o el Instalador cuando hay que investigar un método de instalación?

**Situación:** El Instalador no conoce el mejor método para instalar una herramienta poco común.

**Resolución:** El Instalador invoca al Investigador (hook S11) para que investigue el método de instalación óptimo. El Investigador busca en 2-3 fuentes (documentación oficial, GitHub, Stack Overflow) y reporta el método recomendado. El Instalador ejecuta la instalación siguiendo las recomendaciones.

**Regla general:** El Investigador investiga, el Instalador ejecuta. El Instalador no adivina métodos de instalación.

---

### Conflicto 4: ¿Qué pasa si el Supervisor y el Explorador discrepan sobre qué agente debe actuar?

**Situación:** El Explorador, explorando el codebase, encuentra código que necesita modificarse y cree que debería hacerlo él mismo (tentador porque "ya está ahí").

**Resolución:** El Explorador tiene prohibido modificar archivos (es solo lectura). El Supervisor decide quién modifica: normalmente el Operador, o si el cambio es muy específico de un dominio (ej. schema de DB → Integrador), el Supervisor asigna al especialista correspondiente.

**Regla general:** El Supervisor tiene la última palabra en asignación de tareas. Ningún agente puede auto-asignarse una tarea que no sea de su dominio.

---

## Protocolo de escalación

Si un conflicto no encaja en los casos anteriores, **El Supervisor** aplica su protocolo de arbitraje:

1. **Recibir el conflicto** — Parte A, Parte B, contexto
2. **Clasificar**: Solapamiento de dominio, Desacuerdo técnico, Ambigüedad de responsabilidad, o Conflicto de prioridades
3. **Resolver**: Aplicar tabla de soberanía si está cubierto; aplicar criterio si no; escalar al usuario solo si es irresoluble
4. **Comunicar**: "La tarea va para @[agente] porque [razón]. @[otro], quedas liberado."

Si El Supervisor no está disponible (conflicto de él contra otro agente):

1. **Parar:** ningún agente implementa nada mientras el conflicto no esté resuelto
2. **Documentar:** el agente que detecta el conflicto lo documenta en el chat
3. **Elevar al usuario:** presentar las dos opciones con pros/contras
4. **Decisión del usuario:** el usuario decide
5. **No hay conflicto eterno:** si el usuario no responde en la misma sesión, el agente con soberanía en el dominio más directamente afectado decide con la opción más conservadora

## Señales de conflicto que los agentes deben reconocer

- "Yo haría X, pero [Agente] sugirió Y" → conflicto detectado, escalar
- Un agente implementa algo que es dominio de otro → parar y derivar
- Dos agentes proponen soluciones contradictorias sin resolverlo → escalar al Supervisor
- Un agente dice "puedo hacerlo" cuando no es su especialidad → el Supervisor decide

## Integración con ETC — El Septeto Calavera

Los conflictos entre System Agents y ETC agents (ej. El Integrador vs El Herrero sobre el diseño de una API) se resuelven así:

| Conflicto entre | Resuelve | Razón |
|-----------------|----------|-------|
| System Agent vs ETC Agent | ⚖️ El Supervisor | Primera línea de resolución |
| Supervisor vs Árbitro | ⚖️ El Árbitro | Árbitro tiene soberanía sobre conflictos entre agentes |
| Supervisor no puede resolver | ⚖️ El Árbitro | Escalación natural |
| Ninguno puede resolver | Usuario | Decisión final humana |
