# 📓 Bitácora KeyHandy

> Log cronológico de sesiones de trabajo. **Las entradas más recientes van arriba.**
> Claude Code actualiza este archivo al cierre de cada sesión.

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

**Bloqueos:**

- Trato no cerrado aún — no iniciar desarrollo hasta confirmación

**Próximo paso:**

- Presentar cotización a la clienta usando el plan de fases del MASTER.md
- Al cerrar el trato: crear repo en GitHub, copiar template desde mobbitrips-web-v2, arrancar Fase 0

---
