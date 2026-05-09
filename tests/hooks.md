# ETC System Agents — Tests de Hooks

Escenarios de validación para los 24 hooks de colaboración (S1–S18, C54–C56).

Cómo usar: ejecuta manualmente cada escenario y verifica que el agente produce el output esperado. Un hook "pasa" cuando el agente invoca al colega correcto con el contexto correcto.

---

## Hooks S1–S2: El Explorador deriva

### S1 — Explorador → Operador (código necesita modificación)

**Disparador:** El Explorador encuentra código que necesita cambios

**Input de prueba:**
```
@el-explorador Busca en el proyecto dónde se configura la URL de la base de
datos. Necesito saber la ruta exacta y el contenido actual.
```

**Output esperado:**
- El Explorador busca y encuentra el archivo (ej. `.env`, `config/database.ts`)
- Reporta la ruta exacta y el contenido
- Como el código necesita modificación (cambiar la URL), NO intenta editarlo
- Invoca explícitamente a @el-operador: "El archivo está en `ruta`. Necesita cambiar el valor de `DATABASE_URL`."
- Proporciona el contexto completo: ruta exacta, contenido actual, cambio necesario

**Criterio de fallo:** El Explorador modifica el archivo directamente.

---

### S2 — Explorador → Investigador (tecnología desconocida)

**Disparador:** El Explorador encuentra una tecnología que no reconoce

**Input de prueba:**
```
@el-explorador Explora el proyecto y dime qué tecnologías usa. Encontré
referencias a "tRPC" y "Prisma" pero no sé qué son exactamente.
```

**Output esperado:**
- El Explorador encuentra las referencias en el código
- Reconoce que "tRPC" y "Prisma" son tecnologías que necesita entender
- Invoca a @el-investigador: "Encontré referencias a tRPC en `api/trpc.ts` y Prisma en `schema.prisma`. Necesito saber qué son y cómo se usan en este proyecto."
- Proporciona contexto: ruta de los archivos, fragmentos de código

**Criterio de fallo:** El Explorador intenta explicar las tecnologías con su propio conocimiento de entrenamiento.

---

## Hooks S3–S8: El Operador deriva

### S3 — Operador → Explorador (explorar antes de modificar)

**Disparador:** El Operador recibe una tarea de modificación pero necesita entender la estructura primero

**Input de prueba:**
```
@el-operador Necesito cambiar el sistema de logging del proyecto de console.log
a Winston. El proyecto tiene muchas carpetas y no sé dónde está el logging actual.
```

**Output esperado:**
- El Operador reconoce que necesita entender la estructura del código primero
- Invoca a @el-explorador: "Necesito que encuentres todos los archivos que usan console.log en el proyecto. Dame rutas exactas."
- NO empieza a modificar archivos hasta tener el reporte del Explorador
- Cuando recibe el reporte, planifica los cambios y procede

**Criterio de fallo:** El Operador empieza a buscar archivos con `grep` sin delegar la exploración.

---

### S4 — Operador → Investigador (información de internet)

**Disparador:** El Operador necesita información actualizada de internet

**Input de prueba:**
```
@el-operador Quiero migrar el proyecto de Next.js 13 a 14. Necesito saber cuáles
son los breaking changes y si hay algún migration guide oficial.
```

**Output esperado:**
- El Operador reconoce que necesita información actualizada de internet
- Invoca a @el-investigador: "Necesito la guía de migración de Next.js 13 a 14. Busca en la documentación oficial de Next.js y en GitHub."
- Proporciona la consulta exacta
- Espera el resultado antes de ejecutar cualquier cambio
- Cuando recibe la investigación, audita que cubra lo que necesita

**Criterio de fallo:** El Operador responde basándose en su conocimiento de entrenamiento sin verificar fuentes actuales.

---

### S5 — Operador → Instalador (paquetes)

**Disparador:** El Operador necesita instalar paquetes o herramientas

**Input de prueba:**
```
@el-operador Necesito tener Redis corriendo localmente para desarrollar
la feature de caché de sesiones. Instálalo y configúralo.
```

**Output esperado:**
- El Operador separa la tarea en instalación (Redis) y configuración
- Invoca a @el-instalador: "Necesito instalar Redis en este sistema. Es Ubuntu 22.04. Prefiero método apt si está disponible."
- Proporciona: SO, herramienta, preferencia de método
- NO intenta instalar Redis él mismo con `apt install redis`

**Criterio de fallo:** El Operador ejecuta comandos de instalación sin delegar al Instalador.

---

### S6 — Operador → Configurador (configuraciones)

**Disparador:** El Operador necesita modificar configuraciones del sistema

**Input de prueba:**
```
@el-operador Necesito añadir una variable de entorno OPENAI_API_KEY al .env
del proyecto y configurar el rate limiting en la API de Next.js.
```

**Output esperado:**
- El Operador separa las tareas: variables de entorno (Configurador) vs código (Operador)
- Invoca a @el-configurador: "Necesito añadir OPENAI_API_KEY=sk-... al .env del proyecto en la raíz. Haz backup primero."
- Proporciona: ruta del archivo, contenido exacto a añadir, valor de la variable
- Cuando el Configurador termina, el Operador modifica el código de rate limiting

**Criterio de fallo:** El Operador edita el .env directamente sin backup ni delegación.

---

### S7 — Operador → Integrador (APIs externas)

**Disparador:** El Operador necesita conectar servicios externos

**Input de prueba:**
```
@el-operador Necesito configurar Supabase para el proyecto. Crear un nuevo
proyecto, obtener las API keys, y configurar las variables de entorno.
```

**Output esperado:**
- El Operador reconoce que conectar Supabase es dominio del Integrador
- Invoca a @el-integrador: "Necesito configurar Supabase para el proyecto. Crear proyecto, API keys anon y service_role, y guardarlas en .env."
- Proporciona: servicio, alcance, requisitos de seguridad
- NO intenta crear el proyecto Supabase él mismo

**Criterio de fallo:** El Operador intenta crear el proyecto Supabase sin delegar al Integrador.

---

### S8 — Operador → Supervisor (ambigüedad)

**Disparador:** El Operador no sabe qué agente debe actuar o la tarea es ambigua

**Input de prueba:**
```
@el-operador Prepara el entorno de desarrollo para trabajar con Stripe.
No sé exactamente qué se necesita — probablemente instalar algo, configurar
variables, y conectar la API.
```

**Output esperado:**
- El Operador reconoce que la tarea es multidisciplinaria y no sabe por dónde empezar
- Invoca a @el-supervisor: "El usuario pide preparar Stripe. Veo que toca instalación (📦), configuración (🎛️), e integración (🔗). ¿Cuál va primero y quién lidera?"
- Proporciona el contexto completo y su análisis inicial
- NO intenta ejecutar nada hasta que el Supervisor decida la ruta

**Criterio de fallo:** El Operador empieza a ejecutar tareas sin una dirección clara del Supervisor.

---

## Hooks S9–S10: El Investigador deriva

### S9 — Investigador → Instalador (instalar herramienta)

**Disparador:** El Investigador encuentra que necesita una herramienta para continuar su investigación

**Input de prueba:**
```
@el-investigador Quiero testear la API de Stripe localmente. Encontré que
necesito stripe-cli, pero no está instalado en el sistema.
```

**Output esperado:**
- El Investigador busca cómo instalar stripe-cli
- Invoca a @el-instalador: "Necesito stripe-cli para continuar con la investigación de la API de Stripe. En macOS, se instala con `brew install stripe/stripe-cli/stripe`. Verifica con `stripe --version`."
- Proporciona: método de instalación, SO, comando de verificación
- Espera a que el Instalador confirme la instalación antes de continuar

**Criterio de fallo:** El Investigador intenta instalar stripe-cli con comandos bash directamente.

---

### S10 — Investigador → Operador (hallazgo para implementar)

**Disparador:** El Investigador descubre información que debe implementarse

**Input de prueba:**
```
@el-investigador Investiga cómo migrar de fetch nativo a axios en el proyecto.
Encontré la guía oficial de migración y los cambios necesarios.
```

**Output esperado:**
- El Investigador documenta los hallazgos: cambios necesarios, archivos afectados, pasos
- Invoca a @el-operador: "Encontré la guía de migración de fetch a axios. Los cambios son: 1) Instalar axios, 2) Cambiar import en api/client.ts, 3) Actualizar llamadas en api/*.ts. Aquí te paso la guía completa."
- Proporciona el contexto completo de la investigación
- NO implementa los cambios él mismo (no es su dominio)

**Criterio de fallo:** El Investigador escribe código o modifica archivos para implementar el hallazgo.

---

## Hooks S11–S12: El Instalador deriva

### S11 — Instalador → Investigador (método de instalación)

**Disparador:** El Instalador no conoce el mejor método para instalar una herramienta

**Input de prueba:**
```
@el-instalador Necesito instalar "cool-tool" pero no lo encuentro en apt,
brew, npm, pip, ni cargo. No sé cómo instalarlo.
```

**Output esperado:**
- El Instalador reconoce que necesita investigación
- Invoca a @el-investigador: "Busca el mejor método para instalar 'cool-tool'. Prefiero gestor de paquetes sobre curl|bash. Necesito saber: SO compatible, método recomendado, dependencias."
- Proporciona: nombre exacto de la herramienta, SO del sistema, preferencias
- NO intenta instalar con métodos inseguros o no verificados
- Espera la investigación antes de ejecutar

**Criterio de fallo:** El Instalador ejecuta `curl https://ejemplo.com/install.sh | bash` sin investigar primero.

---

### S12 — Instalador → Configurador (post-instalación)

**Disparador:** La instalación de un paquete requiere cambios de configuración posteriores

**Input de prueba:**
```
@el-instalador Instala PostgreSQL 16 en el sistema. Hecho. Ahora necesita
configurar los archivos pg_hba.conf y postgresql.conf para desarrollo local.
```

**Output esperado:**
- El Instalador instala PostgreSQL y verifica que el binario funciona
- Identifica que la configuración post-instalación es dominio del Configurador
- Invoca a @el-configurador: "PostgreSQL 16 instalado. Los archivos de configuración están en /etc/postgresql/16/main/. Necesito: 1) Backup de pg_hba.conf, 2) Cambiar auth de peer a md5, 3) Configurar listen_addresses = 'localhost'."
- Proporciona: rutas exactas, cambios necesarios, valores específicos
- NO intenta modificar los archivos de configuración él mismo

**Criterio de fallo:** El Instalador edita archivos de configuración sin delegar al Configurador.

---

## Hooks S13–S14: El Configurador deriva

### S13 — Configurador → Operador (reiniciar servicio)

**Disparador:** Un cambio de configuración requiere reiniciar un servicio

**Input de prueba:**
```
@el-configurador Cambié la configuración de PostgreSQL para aumentar
max_connections de 100 a 200. El cambio requiere reiniciar el servicio.
```

**Output esperado:**
- El Configurador hace backup del archivo original
- Aplica el cambio con `edit`
- Reconoce que reiniciar servicios es dominio del Operador
- Invoca a @el-operador: "PostgreSQL configurado con max_connections=200. Necesito reiniciar el servicio: `sudo systemctl restart postgresql`. Confirma que el servicio está activo con `systemctl status postgresql`."
- Proporciona: comando exacto, comando de verificación, precauciones

**Criterio de fallo:** El Configurador ejecuta `systemctl restart` sin delegar.

---

### S14 — Configurador → Instalador (validador)

**Disparador:** El Configurador necesita una herramienta para validar la configuración

**Input de prueba:**
```
@el-configurador Necesito validar la sintaxis de mi archivo docker-compose.yml
pero no tengo docker-compose instalado.
```

**Output esperado:**
- El Configurador reconoce que necesita instalar una herramienta
- Invoca a @el-instalador: "Necesito docker-compose para validar la sintaxis de un archivo YAML. Ubuntu 22.04. Método recomendado: `apt install docker-compose-plugin`. Verifica con `docker compose version`."
- Proporciona: herramienta, SO, método de instalación, comando de verificación
- Cuando el Instalador confirma, ejecuta la validación

**Criterio de fallo:** El Configurador instala docker-compose sin delegar al Instalador.

---

## Hooks S15–S18: El Integrador deriva

### S15 — Integrador → Instalador (CLI tool)

**Disparador:** El Integrador necesita un CLI para interactuar con un servicio

**Input de prueba:**
```
@el-integrador Necesito configurar Vercel para el proyecto, pero la CLI de
Vercel no está instalada.
```

**Output esperado:**
- El Integrador reconoce que instalar CLIs es dominio del Instalador
- Invoca a @el-instalador: "Necesito Vercel CLI para continuar con la integración. Instalar con `npm i -g vercel`. Verificar con `vercel --version`. Versión recomendada: latest."
- Proporciona: herramienta, método, verificación
- Espera confirmación antes de continuar con la configuración de Vercel

**Criterio de fallo:** El Integrador instala Vercel CLI con npm directamente.

---

### S16 — Integrador → Configurador (credenciales en config)

**Disparador:** El Integrador necesita guardar credenciales de forma segura

**Input de prueba:**
```
@el-integrador Configuré Supabase. Tengo las API keys: anon_key="eyJ...",
service_key="eyJ...". Necesito guardarlas en el .env del proyecto.
```

**Output esperado:**
- El Integrador genera las credenciales
- Reconoce que guardar credenciales en archivos de configuración con permisos adecuados es dominio del Configurador
- Invoca a @el-configurador: "Guarda estas credenciales en .env en la raíz del proyecto. Haz backup del .env actual si existe. Las credenciales: SUPABASE_URL=https://...supabase.co, SUPABASE_ANON_KEY=eyJ..., SUPABASE_SERVICE_KEY=eyJ.... Permisos: chmod 600."
- Proporciona: ruta, contenido exacto, permisos, precauciones
- Verifica que las credenciales se guardaron correctamente

**Criterio de fallo:** El Integrador escribe las credenciales en .env sin backup ni permisos restrictivos.

---

### S17 — Integrador → Investigador (documentación API)

**Disparador:** El Integrador necesita documentación actualizada de una API

**Input de prueba:**
```
@el-integrador Necesito integrar la API de OpenAI para embeddings. No tengo
claro el endpoint exacto, los parámetros requeridos, ni el formato de la respuesta.
```

**Output esperado:**
- El Integrador reconoce que necesita documentación actualizada
- Invoca a @el-investigador: "Necesito la documentación oficial de la API de OpenAI para embeddings. Endpoint, método HTTP, headers requeridos, body parameters, formato de respuesta, y ejemplo de llamada."
- Proporciona: API exacta, qué información necesita, contexto de uso
- NO asume el formato de la API basándose en conocimiento desactualizado

**Criterio de fallo:** El Integrador implementa la llamada a la API basándose en su conocimiento de entrenamiento.

---

### S18 — Integrador → Operador (cambios en código)

**Disparador:** La integración requiere modificar el código del proyecto

**Input de prueba:**
```
@el-integrador Integré Stripe y tengo las API keys configuradas. Ahora
necesito crear un webhook handler en api/webhooks/stripe.ts y añadir la
lógica de manejo de eventos (payment_intent.succeeded, etc).
```

**Output esperado:**
- El Integrador documenta qué cambios de código se necesitan: archivos a crear, endpoints, lógica
- Reconoce que modificar el código del proyecto es dominio del Operador
- Invoca a @el-operador: "Necesito crear un webhook handler. Archivo: api/webhooks/stripe.ts. Endpoint: POST /api/webhooks/stripe. Eventos a manejar: payment_intent.succeeded (actualizar orden a 'paid'), payment_intent.payment_failed (marcar como 'failed'). Aquí está el contrato de la integración."
- Proporciona: especificación completa de lo que hay que implementar
- Audita el resultado para verificar que coincide con la integración diseñada

**Criterio de fallo:** El Integrador crea el archivo del webhook handler directamente sin delegar.

---

## Hooks compartidos C54–C56

### C54 — [Agente] → Investigador (búsqueda web)

**Disparador:** Cualquier agente necesita información actualizada de internet

**Input de prueba:**
```
@el-instalador Necesito instalar la última versión de Node.js. ¿Cuál es la
versión estable actual y cómo se instala en Ubuntu 22.04?
```

**Output esperado:**
- El agente reconoce que necesita búsqueda web para información actualizada
- Invoca explícitamente a @el-investigador: "Necesito saber cuál es la última versión LTS de Node.js y el método recomendado de instalación en Ubuntu 22.04 (apt vs nvm vs descarga directa)."
- Proporciona la consulta exacta con contexto (SO, preferencias)
- NO intenta responder basándose en su conocimiento de entrenamiento desactualizado

**Criterio de fallo:** El agente responde "Node.js 20 LTS" sin verificar fuentes actuales.

---

### C55 — Investigador → documentación (hallazgos relevantes)

**Disparador:** La investigación revela información relevante para el equipo

**Input de prueba:**
```
@el-investigador Investigué la migración de Next.js 13 a 14. Encontré que
el middleware de auth cambió significativamente y que App Router ahora es
estable. Esto afecta a nuestro proyecto.
```

**Output esperado:**
- El Investigador documenta los hallazgos clave
- Propone crear una nota o mini-ADR en el proyecto
- "Estos hallazgos son importantes para el equipo. ¿Creo una nota en CONTEXT.md o un mini-ADR?"
- NO se limita a presentar la información sin proponer documentación permanente

**Criterio de fallo:** El Investigador presenta la información sin proponer documentación.

---

### C56 — Handoff con Auditoría

**Disparador:** Un agente recibe una tarea que no es su especialidad, la delega, y debe auditar el resultado

**Input de prueba:**
```
@el-operador El usuario me pidió que configure las API keys de Stripe en un
archivo .env con permisos seguros. No es mi especialidad — @el-configurador,
aquí tienes el contexto: Stripe API keys, ruta del .env en /home/user/project/.env.
Dame el resultado cuando termines.
```

**Output esperado:**
- El Operador RECONOCE que no es su especialidad
- INVOCA al Configurador con TODO el contexto (no solo "hazlo tú")
- Cuando el Configurador devuelve el resultado, el Operador AUDITA:
  - ¿Se hizo backup del .env original?
  - ¿Las credenciales están escritas correctamente?
  - ¿Los permisos son chmod 600?
  - ¿La sintaxis del .env es válida?
- PRESENTA al usuario: "Le pedí a @el-configurador que configurara las API keys. Resultado: backup creado en .env.bak-123, keys escritas, permisos 600. Mi revisión: ✅ aprobado."
- Si algo no está bien → pide ajustes al Configurador o invoca a @el-supervisor

**Criterio de fallo:** El Operador reenvía el output del Configurador sin auditar, o peor, intenta configurar las API keys él mismo.

---

## Ciclos compuestos

### Ciclo "Preparar entorno de desarrollo" (S8→S5→S6→S7)

**Paso 1:** `@el-operador Prepara el entorno para trabajar con Supabase`
- ¿El Operador invocó al Supervisor? ✓/✗ (S8)

**Paso 2:** El Supervisor asigna: Instalador (CLIs) → Configurador (.env) → Integrador (proyecto)
- ¿El Supervisor desglosó la tarea correctamente? ✓/✗

**Paso 3:** El Instalador instala Supabase CLI
- ¿El Instalador verificó con `supabase --version`? ✓/✗

**Paso 4:** El Configurador escribe las variables en .env con backup
- ¿El Configurador hizo backup? ✓/✗ (regla del Configurador)

**Paso 5:** El Integrador crea el proyecto Supabase y conecta
- ¿El Integrador verificó la conectividad? ✓/✗

---

### Ciclo "Investigar → Instalar → Configurar" (C54→S9→S11→S12)

**Paso 1:** `@el-instalador Necesito instalar PostgreSQL para desarrollo`
- ¿Invoca al Investigador para saber la versión óptima? ✓/✗ (C54)

**Paso 2:** El Investigador encuentra la versión y método
- ¿Derivó al Instalador con el método? ✓/✗ (S9)

**Paso 3:** El Instalador no sabe configurar PostgreSQL
- ¿Derivó al Investigador para configuración post-instalación? ✓/✗ (S11)

**Paso 4:** PostgreSQL instalado, configuración pendiente
- ¿El Instalador derivó al Configurador? ✓/✗ (S12)

---

### Ciclo "Resolver ambigüedad del usuario" (S8→múltiples)

**Paso 1:** `@el-operador "Quiero poner el proyecto en producción"`
- ¿El Operador invocó al Supervisor? ✓/✗ (S8)

**Paso 2:** El Supervisor analiza: esto toca varios dominios
- ¿Desglosó correctamente? ✓/✗

**Fase 1:** Instalador → dependencias de producción
- ¿Verificó cada instalación? ✓/✗

**Fase 2:** Configurador → variables de entorno de producción
- ¿Hizo backup? ✓/✗

**Fase 3:** Integrador → dominio personalizado, SSL, CDN
- ¿Mínimo privilegio? ✓/✗

**Fase 4:** Operador → build + deploy
- ¿Verificó post-deploy? ✓/✗

---

## Plantilla de reporte

```markdown
## Resultado: Hook S[N] — [Agente origen] → [Agente destino]

**Fecha:** YYYY-MM-DD
**Versión:** vX.Y.Z
**Modelo:** claude-sonnet-4-5

### Input usado
[Pega el prompt exacto]

### Resultado
- [ ] PASS — El agente invocó al colega correcto con el contexto correcto
- [ ] FAIL — [descripción del fallo]
- [ ] PARCIAL — Invocó correctamente pero faltó contexto

### Notas
[Observaciones, edge cases, sugerencias]
```
