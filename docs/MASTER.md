# 🔑 WEB_KEYHANDY — Prompt Maestro v0.1
## Plataforma web: Reservas + Contenido digital + Inmobiliaria + Agenda

> **Este documento es la fuente de verdad del proyecto.**
> Estado: **COTIZACIÓN** (clienta casi confirmada). Cuando se cierre el trato, este documento pasa a v1.0 y se ajusta con lo acordado.
> Cualquier decisión arquitectónica debe actualizar este archivo.

---

## 🆕 Changelog

### v0.2 (2026-06-04) — Compromiso de 5 semanas
- **Compromiso con la clienta: 4 módulos completos y en vivo en 5 semanas** desde el anticipo.
- El plan de fases (sección 5) se re-basea de 12 semanas (~15 h/sem) a 5 semanas con desarrollo intensivo vía Claude Code; el cuello de botella pasa a ser las dependencias externas (decisiones, contenido, altas de cuentas).
- Se agrega **Semana 0** (pre-arranque, adelantable antes del anticipo): cerrar decisiones, pedir contenido, abrir cuentas, mockup del home, repo listo.
- Desglose operativo en `docs/PLAN_DESARROLLO.md` (tareas/subtareas para ClickUp vía SLIM).

### v0.1 (junio 2026) — Borrador para cotización
- Definición inicial de los 4 módulos con la clienta.
- Decisión: reservas vía **sincronización iCal** (no channel manager de pago).
- Decisión: contenido digital con **entrega simple** (acceso/descarga tras pago, sin área de miembros).
- Base técnica: se reutiliza el stack y la metodología de `mobbitrips-web-v2`.
- Pendiente: pasarela de pago, branding, dominio, herramienta de agenda.

---

## 1. Visión

**KeyHandy** es la plataforma web de una clienta que combina 4 líneas de negocio en un solo sitio:

| # | Módulo | Qué hace | Pago |
|---|--------|----------|------|
| 1 | **Reservas** | Catálogo de alojamientos + motor de reserva con calendario sincronizado vía iCal (Airbnb/Booking) | ✅ Sí |
| 2 | **Contenido digital** | Venta de cursos, guías y contenido pregrabado. Entrega simple post-pago | ✅ Sí |
| 3 | **Inmobiliaria** | Catálogo de casas/terrenos en venta con ficha completa (fotos, características, ubicación, precio) + captura de leads | ❌ Solo leads |
| 4 | **Agenda** | Reservar videollamadas / atención personalizada (Calendly o Cal.com embebido) | Opcional |

---

## 2. Base técnica — reutilización de Mobbitrips

Se parte del monorepo `mobbitrips-web-v2` como template. **Qué se reutiliza:**

| Pieza | Reutilización |
|-------|--------------|
| Metodología completa (bitácora, sprints, reglas, flujo Claude Design ↔ Claude Code) | ✅ Directa |
| Tooling: pnpm + Turborepo + ESLint + Prettier + Husky + commitlint | ✅ Directa |
| `packages/ui` (AnimatedSection, componentes base) | ✅ Adaptando branding |
| Estructura `apps/web` Next.js 14 (App Router, Server Components) | ✅ Como esqueleto |
| Patrón Supabase (DB + Auth + Storage + RLS + tabla `events`) | ✅ Directa |
| Flujo de checkout/pagos (cuando se confirme pasarela) | ✅ Adaptando |
| `hostex-client` | ❌ No aplica (aquí es iCal) |
| Contenido, copy e identidad Mobbitrips | ❌ No aplica |

### Stack

| Capa | Tecnología |
|------|-----------|
| Framework | Next.js 14 (App Router, Server Components) |
| Lenguaje | TypeScript estricto |
| Estilos | Tailwind CSS |
| Animación | `<AnimatedSection>` (IntersectionObserver + CSS) — **NUNCA Framer Motion para scroll-reveal** |
| DB | Supabase (Postgres + Auth + Storage) |
| Pagos | ⏳ Por definir (recomendado: Stripe) |
| Agenda | ⏳ Por definir (Calendly embed o Cal.com) |
| Email transaccional | Resend |
| Deploy | Vercel |
| Monorepo | Turborepo + pnpm workspaces |

---

## 3. Módulos en detalle

### 3.1 Reservas de alojamientos (iCal)

**Cómo funciona la sincronización iCal:**
- Cada alojamiento en Airbnb/Booking expone una URL `.ics` con sus fechas ocupadas.
- Un cron (Vercel Cron) importa esos calendarios cada ~30-60 min y bloquea fechas en Supabase.
- Nuestro sitio expone a su vez un `.ics` por alojamiento para que Airbnb/Booking bloqueen las fechas reservadas con nosotros.

**⚠️ Limitación clave de iCal (explicar a la clienta):** solo sincroniza **fechas**, no precios ni datos de huéspedes. Los precios, fotos y fichas viven en nuestra base. La sincronización no es instantánea (ventana de ~30-60 min) → riesgo bajo de doble reserva, mitigable con confirmación manual o margen de bloqueo.

**Alcance:**
- Catálogo de alojamientos (fichas con galería, amenidades, ubicación, precios por temporada)
- Calendario de disponibilidad + selector de fechas
- Checkout con pasarela de pago
- Emails de confirmación (Resend)
- Import/export iCal automático

### 3.2 Contenido digital (entrega simple)

- Catálogo de productos: cursos, guías (PDF), videos pregrabados
- Checkout con pasarela
- **Entrega post-pago:** email automático con link de acceso — Supabase Storage con signed URLs (PDFs/descargas) y/o Vimeo unlisted (videos)
- Sin login ni área de miembros (decisión confirmada — mantiene el alcance acotado)
- Panel simple para que la clienta suba/edite productos (fase posterior; al inicio lo gestionamos nosotros)

### 3.3 Inmobiliaria

- Catálogo de inmuebles (casas/terrenos): galería, m², recámaras, servicios, ubicación con mapa, precio, estatus (disponible/apartado/vendido)
- Filtros por tipo, precio, ubicación
- Ficha completa por inmueble con formulario de contacto → lead a email/WhatsApp de la clienta
- Sin pagos en línea (las ventas inmobiliarias se cierran en persona)

### 3.4 Agenda de videollamadas

- Página con embed de Calendly o Cal.com
- **Recomendación:** Cal.com (gratis en plan básico, embebible, soporta cobro por sesión si la clienta quiere cobrar la atención personalizada). Calendly es la alternativa si ella ya lo usa.

---

## 4. Decisiones pendientes (cerrar con la clienta)

| # | Decisión | Opciones | Recomendación |
|---|----------|----------|---------------|
| 1 | Pasarela de pago | Stripe / MercadoPago / ambas | Stripe (una sola integración cubre reservas + contenido) |
| 2 | Herramienta de agenda | Calendly / Cal.com | Cal.com (gratis + cobro por sesión) |
| 3 | Branding | ¿Tiene logo/colores o lo diseñamos? | Definir antes de Fase 1 |
| 4 | Dominio y hosting de correo | ¿Ya tiene dominio? | — |
| 5 | Hosting de video | Vimeo / YouTube unlisted / Supabase Storage | Vimeo (privacidad real) |
| 6 | ¿Cuántos alojamientos e inmuebles arranca? | — | Define esfuerzo de carga inicial |
| 7 | ¿Cobra las videollamadas? | Sí / No | Afecta elección de agenda |

---

## 5. Plan de fases — compromiso de 5 semanas

**Comprometido con la clienta: 4 módulos completos y en vivo en 5 semanas desde el anticipo.** Desarrollo intensivo con Claude Code (la implementación la hace el agente; el tiempo de Emilio es dirección, revisión y QA). Esfuerzo relativo: S < M < L. Desglose operativo completo en `PLAN_DESARROLLO.md`.

| Fase | Semana | Foco | Esfuerzo |
|------|--------|------|----------|
| **Semana 0 — Pre-arranque** | antes del anticipo | Cerrar las 7 decisiones, pedir TODO el contenido, abrir cuentas (pasarela/dominio/Resend), mockup del home, repo listo | S |
| **Fase 0 — Setup + Diseño** | 1 | Repo desde template Mobbitrips, branding KeyHandy, sistema de diseño, home | M |
| **Fase 1 — Inmobiliaria + Agenda** | 2 | Catálogo de inmuebles + fichas + leads + embed de agenda. *Entrega visible temprana* | M |
| **Fase 2 — Reservas + Pagos** | 2-4 | Fichas de alojamientos, sync iCal, motor de reserva, checkout, emails | L |
| **Fase 3 — Contenido digital** | 4 | Catálogo de productos, checkout, entrega automática post-pago | M |
| **Fase 4 — Pulido + Lanzamiento** | 5 | SEO, analítica, accesibilidad, carga de contenido real, QA, go-live | M |

> El orden pone primero lo más simple (inmobiliaria/agenda) para que la clienta vea avances pronto, y deja lo más complejo (reservas) para cuando el sistema de diseño ya está maduro.
>
> ⚠️ **El calendario se sostiene solo si las dependencias externas llegan a tiempo**: decisiones cerradas en Semana 0, contenido de la clienta a fin de semana 1, cuentas verificadas temprano. El riesgo del plan no es la velocidad de desarrollo — son los tiempos de terceros (ver riesgos en `PLAN_DESARROLLO.md`).

---

## 6. Reglas de oro (heredadas de Mobbitrips)

1. Secretos solo en `process.env.*`.
2. Nunca tocar datos de tarjeta — siempre checkout hospedado/Elements de la pasarela.
3. Idempotencia en todo webhook.
4. Server Components por defecto; `'use client'` solo con interactividad real.
5. Validación doble capa: Zod en cliente Y servidor.
6. RLS activo en todas las tablas Supabase.
7. APIs externas solo desde el servidor, nunca del cliente.
8. Accesibilidad WCAG AA mínimo.
9. **NUNCA `overflow: clip` en globals.css** (rompe la compilación CSS — usar `overflow: hidden` + padding).
10. Visualizador canónico único: `pnpm dev` → `http://localhost:3000`. Nunca `file:///`.
11. Pull al iniciar sesión + commit/push al cerrar, siempre.
12. Nunca editar `main` directo — ramas `design/*`, `content/*`, `fix/*`.

---

## 7. Estructura del monorepo (objetivo)

```
web_keyhandy/
├── CLAUDE.md
├── docs/
│   ├── MASTER.md                ← este archivo
│   ├── BITACORA.md              ← log de sesiones ⭐
│   ├── SPRINT_ACTUAL.md
│   ├── decisiones/              ← ADRs
│   └── sprints/completados/
├── apps/
│   └── web/                     ← Next.js keyhandy
├── packages/
│   ├── ui/                      ← desde mobbitrips, rebrandeado
│   ├── ical-sync/               ← NUEVO: import/export iCal
│   ├── supabase-client/
│   └── types/
├── design/exports/              ← HTML versionados de Claude Design
└── supabase/migrations/
```

---

**Última actualización**: 2026-06-04 · **Versión**: 0.2 (compromiso de 5 semanas; pendiente promover a v1.0 al recibir anticipo)
