# 📓 Bitácora KeyHandy

> Log cronológico de sesiones de trabajo. **Las entradas más recientes van arriba.**
> Claude Code actualiza este archivo al cierre de cada sesión.

---

## 2026-06-04 · Sesión 1 — Plan de desarrollo desglosado y re-baseo a 5 semanas

**Etapa**: Pre-venta (clienta casi confirmada) · Trabajó con: Emilio (máquina casa, `C:\Users\PC\keyhandy_web`)

**Tasks cerradas:**

- `docs/PLAN_DESARROLLO.md` creado: F0-F4 desglosadas en 29 tareas / ~95 subtareas con estimados (ref. ~180 h), formateado para que SLIM (agente PM) lo vuelque a ClickUp
- Estructura ClickUp verificada contra el workspace real: Folder `🔑 KEYHANDY — Plataforma Clienta` con una lista por fase (espejo del backlog de Mobbitrips) + tarea-índice en la lista `Medusssa studio`
- **Re-baseo a 5 semanas** (compromiso con la clienta: 4 módulos en vivo en 5 semanas desde el anticipo) → MASTER.md v0.2
- Nueva **Semana 0** pre-arranque (adelantable antes del anticipo): cerrar las 7 decisiones, pedir contenido con fecha límite, abrir cuentas (Stripe/dominio/Resend), mockup del home, repo listo
- Tabla de riesgos del calendario: el cuello de botella son dependencias externas (verificación de pasarela, feeds iCal de OTAs, contenido de la clienta), no la velocidad de desarrollo

**Decisiones:**

- Calendario: F0 sem 1 · F1 sem 2 · F2 sem 2-4 · F3 sem 4 · F4/go-live sem 5
- Los estimados en horas quedan como esfuerzo de referencia (el desarrollo es intensivo con Claude Code)

**Bloqueos / pendientes:**

- ⚠️ El repo está **PÚBLICO** en GitHub aunque la bitácora de sesión 0 dice "privado" — pendiente hacerlo privado
- Trato aún no cerrado; las tareas de Semana 0 sí pueden arrancar ya

**Próximo paso:**

- Redactar mensaje a la clienta: 7 decisiones + petición de contenido con fecha límite + que abra cuenta de Stripe ya
- Pasar `PLAN_DESARROLLO.md` a SLIM para volcarlo a ClickUp (seguir la sección "Instrucciones de estructura para SLIM")

---

## 2026-06-04 · Sesión 0 — Definición de alcance y plan de cotización

**Etapa**: Pre-venta (cotizando, clienta casi confirmada) · Trabajó con: Emilio

**Tasks cerradas:**

- Definición de los 4 módulos con la información de la clienta
- Creación de `docs/MASTER.md` v0.1 (borrador para cotización)
- Estructura inicial del proyecto (docs + metodología heredada de mobbitrips-web-v2)

**Decisiones:**

- **Reservas vía iCal** (no channel manager de pago como Hostex) — solo sincroniza fechas; precios y fichas viven en Supabase
- **Contenido digital con entrega simple** — email con link de acceso/descarga tras el pago, sin área de miembros
- **Inmobiliaria sin pagos en línea** — solo catálogo + captura de leads
- Se reutiliza la base de `mobbitrips-web-v2`: metodología, tooling, `packages/ui`, patrón Supabase

**Pendiente (cerrar con la clienta):**

- Pasarela de pago (recomendado: Stripe)
- Agenda: Calendly vs Cal.com (recomendado: Cal.com)
- Branding (¿tiene logo/colores?), dominio, hosting de video
- Número de alojamientos e inmuebles iniciales
- ¿Cobra las videollamadas?

**Repo creado:**

- GitHub: `https://github.com/medusssastudio-source/keyhandy_web` (privado, cuenta Medusssa)
- `mobbimx` agregado como collaborator (es la identidad que pushea desde las máquinas de Emilio)
- Commit inicial `9724423` en `main`

**Bloqueos:**

- Trato no cerrado aún — no iniciar desarrollo hasta confirmación

**Próximo paso:**

- Resolver con la clienta las 7 decisiones pendientes (MASTER.md sección 4) y armar cotización con el plan de fases
- Opcional pro-venta: mockup del home con Claude Design
- Al cerrar el trato: copiar template desde mobbitrips-web-v2, arrancar Fase 0

---
