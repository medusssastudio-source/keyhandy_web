# 🔑 KeyHandy — Plan de desarrollo desglosado (Fases 0-4)

> **Propósito:** documento de planeación listo para que un agente PM (SLIM) lo vuelque a ClickUp.
> Cubre solo las fases de **desarrollo** (0-4). La etapa de pre-venta/cotización se gestiona aparte (ver `SPRINT_ACTUAL.md`).
> Fuente de verdad del alcance: `MASTER.md` v0.1. Este plan se ajusta cuando MASTER pase a v1.0 con lo acordado con la clienta.
>
> ⚠️ **Condición de arranque:** ninguna tarea de este plan inicia hasta que la clienta confirme el trato.

---

## 📋 Instrucciones de estructura para SLIM (ClickUp)

Estructura espejo de la convención ya usada para `🚀 MOBBITRIPS — Backlog Chatbot & Automatización` (folder con una lista por fase):

- **Espacio:** `Espacio de trabajo` (id `90171418412`) — es el único espacio del workspace
- **Crear Folder:** `🔑 KEYHANDY — Plataforma Clienta` (ClickUp no tiene "subproyectos"; el folder cumple ese rol)
- **Una Lista por fase** (5 listas), con prefijo de estatus como en el backlog de Mobbitrips (⏳ pendiente → 🔄 en curso → ✅ completada). Todas arrancan en ⏳:
  `⏳ FASE 0 — Setup + Diseño`, `⏳ FASE 1 — Inmobiliaria + Agenda`, `⏳ FASE 2 — Reservas + Pagos`, `⏳ FASE 3 — Contenido digital`, `⏳ FASE 4 — Pulido + Lanzamiento`
- **Vínculo con Medusssa:** crear una tarea-índice en la lista `Medusssa studio` (id `901705936222`, folder `Proyectos Grupo Mobbi One`) llamada `🔑 KeyHandy — ver folder del proyecto`, con link al folder, para que el proyecto figure bajo Medusssa sin duplicar tareas.
- **Tareas y subtareas:** cada `###` de este documento es una tarea; sus viñetas con estimado son subtareas.
- **Estimados:** en horas, cargarlos en el campo *Time Estimate* (tarea = suma de sus subtareas).
- **Prioridad:** las tareas marcadas 🔴 son ruta crítica de su fase; el resto prioridad normal.
- **Dependencias:** indicadas como `Depende de:` — crearlas como dependencias *waiting on* en ClickUp.
- **Bloqueos:** las tareas marcadas ⛔ dependen de una decisión pendiente con la clienta (sección final). Etiquetarlas con tag `bloqueada-decision` hasta que se resuelva.
- **Fechas:** no asignar due dates todavía; se calendarizan al cerrar el trato (ritmo: ~15 h/semana).

**Presupuesto total estimado: ~180 h en 12 semanas** (F0: 30 h · F1: 30 h · F2: 60 h · F3: 30 h · F4: 30 h)

---

## F0 · Setup + Diseño — semanas 1-2 · 30 h

**Objetivo:** repo funcionando desde el template de Mobbitrips, branding KeyHandy definido y home navegable en Vercel.

### 0.1 🔴 Setup del monorepo desde template Mobbitrips — 8 h
- Copiar tooling: pnpm + Turborepo + ESLint + Prettier + Husky + commitlint — 2 h
- Copiar `packages/ui` limpiando branding/contenido Mobbitrips — 2 h
- Esqueleto `apps/web` Next.js 14 (App Router, Server Components) — 2 h
- Conectar repo a Vercel con deploy previews por rama — 2 h

### 0.2 🔴 Infraestructura Supabase — 4 h
- Crear proyecto Supabase + esquema inicial + tabla `events` — 2 h
- Activar RLS en todas las tablas base — 1 h
- Variables de entorno y secrets en Vercel (`process.env.*`, nada hardcodeado) — 1 h

### 0.3 ⛔ Branding KeyHandy — 8 h
*Depende de: decisión 3 (¿la clienta tiene logo/colores?)*
- Definir paleta, tipografía y tono visual con material de la clienta — 3 h
- Tokens en Tailwind + rebrandeo de `packages/ui` — 3 h
- Logo aplicado, favicon y OG image base — 2 h

### 0.4 Sistema de diseño + Home — 10 h
*Depende de: 0.3 Branding*
- Mockup del home con Claude Design (flujo Design ↔ Code) — 4 h
- Convertir mockup a componentes con `<AnimatedSection>` — 4 h
- Navbar, Footer y layout global con navegación a los 4 módulos — 2 h

---

## F1 · Inmobiliaria + Agenda — semanas 3-4 · 30 h

**Objetivo:** primera entrega visible para la clienta — catálogo de inmuebles con captura de leads y agenda embebida.

### 1.1 🔴 Modelo de datos de inmuebles — 4 h
- Tabla `properties` (tipo, m², recámaras, servicios, precio, estatus, ubicación) + RLS — 2 h
- Supabase Storage para galerías + seed con inmuebles de ejemplo — 2 h

### 1.2 Catálogo de inmuebles — 8 h
*Depende de: 1.1*
- Grid de cards con foto, precio y estatus (disponible/apartado/vendido) — 4 h
- Filtros por tipo, rango de precio y ubicación — 4 h

### 1.3 Ficha de inmueble — 8 h
*Depende de: 1.1*
- Galería de fotos + características + mapa de ubicación — 5 h
- Metadata/SEO dinámico por inmueble — 3 h

### 1.4 🔴 Captura de leads — 6 h
*Depende de: 1.3*
- Formulario de contacto con validación Zod doble capa (cliente + servidor) — 3 h
- Lead → email a la clienta (Resend) + link WhatsApp + registro en DB — 3 h

### 1.5 ⛔ Agenda de videollamadas — 4 h
*Depende de: decisión 2 (Calendly vs Cal.com) y decisión 7 (¿cobra las sesiones?)*
- Página de agenda con embed de la herramienta elegida — 2 h
- Configuración de disponibilidad/cobro con la clienta — 2 h

---

## F2 · Reservas + Pagos — semanas 5-8 · 60 h

**Objetivo:** motor de reservas completo con sincronización iCal y checkout funcionando de punta a punta.

### 2.1 🔴 Modelo de datos de alojamientos — 6 h
- Tablas `listings`, `seasonal_rates`, `bookings`, `blocked_dates` + RLS — 4 h
- Seed/carga inicial de alojamientos — 2 h

### 2.2 🔴 Paquete `ical-sync` — 12 h
*Depende de: 2.1*
- Import: parsear `.ics` de Airbnb/Booking → `blocked_dates` — 5 h
- Export: endpoint `.ics` por alojamiento para que las OTAs bloqueen nuestras reservas — 4 h
- Vercel Cron (cada 30-60 min) + logging y alerta si un feed falla — 3 h

### 2.3 Fichas de alojamiento — 8 h
*Depende de: 2.1*
- Galería, amenidades y ubicación — 5 h
- Visualización de precios por temporada — 3 h

### 2.4 🔴 Motor de reserva — 12 h
*Depende de: 2.2, 2.3*
- Calendario de disponibilidad + selector de fechas (bloquea fechas ocupadas) — 5 h
- Cálculo de precio por temporada y nº de huéspedes — 4 h
- Re-validación de disponibilidad server-side antes de cobrar (mitiga ventana iCal) — 3 h

### 2.5 🔴 ⛔ Checkout con pasarela — 12 h
*Depende de: 2.4 · decisión 1 (Stripe vs MercadoPago)*
- Integración de checkout hospedado (nunca tocamos datos de tarjeta) — 4 h
- Webhook de confirmación de pago **idempotente** — 4 h
- Estados de reserva (pendiente/confirmada/cancelada) + manejo de pagos fallidos — 4 h

### 2.6 Emails transaccionales — 6 h
*Depende de: 2.5*
- Confirmación de reserva al huésped (Resend) con plantilla brandeada — 3 h
- Notificación de nueva reserva a la clienta — 1 h
- Email de reserva cancelada/fallida — 2 h

### 2.7 QA del flujo de reserva — 4 h
*Depende de: 2.6*
- Prueba punta a punta: buscar → reservar → pagar → confirmar → ver fechas bloqueadas en OTA — 4 h

---

## F3 · Contenido digital — semanas 9-10 · 30 h

**Objetivo:** venta de cursos/guías/videos con entrega automática post-pago (sin área de miembros).

### 3.1 🔴 Modelo de datos de productos — 4 h
- Tabla `products` (tipo: pdf/video/curso, precio, asset asociado) + RLS — 2 h
- Tabla `purchases` para registro y re-envío de accesos — 2 h

### 3.2 Catálogo de productos — 6 h
*Depende de: 3.1*
- Grid + ficha de producto (descripción, preview, precio) — 4 h
- Metadata/SEO por producto — 2 h

### 3.3 Checkout de productos — 6 h
*Depende de: 3.2 · reutiliza integración de 2.5*
- Adaptar flujo de checkout de reservas a productos digitales — 3 h
- Webhook idempotente de confirmación de compra — 3 h

### 3.4 🔴 ⛔ Entrega automática post-pago — 10 h
*Depende de: 3.3 · decisión 5 (hosting de video: Vimeo/YouTube/Storage)*
- Signed URLs de Supabase Storage para PDFs/descargas (con expiración) — 4 h
- Integración de video según hosting elegido (Vimeo unlisted recomendado) — 3 h
- Email automático con links de acceso tras el pago (Resend) — 3 h

### 3.5 Carga de productos reales — 4 h
*Depende de: 3.4*
- Subir y verificar los productos iniciales de la clienta (nosotros gestionamos; panel de autogestión queda fuera de alcance v1) — 4 h

---

## F4 · Pulido + Lanzamiento — semanas 11-12 · 30 h

**Objetivo:** sitio en producción con contenido real, medible y accesible.

### 4.1 SEO técnico — 5 h
- Sitemap, robots, metadata global, OG images — 3 h
- Datos estructurados (schema.org) para inmuebles y alojamientos — 2 h

### 4.2 Analítica — 3 h
- Instalar analítica (Vercel Analytics o GA4) + eventos clave (lead, reserva, compra) — 3 h

### 4.3 Accesibilidad WCAG AA — 5 h
- Auditoría (contraste, foco, navegación por teclado, alt) y correcciones — 5 h

### 4.4 ⛔ Carga de contenido real — 8 h
*Depende de: decisión 6 (nº de alojamientos e inmuebles iniciales)*
- Alojamientos reales: fotos, fichas, precios por temporada, URLs iCal de las OTAs — 5 h
- Inmuebles reales: fotos, fichas, ubicaciones — 3 h

### 4.5 🔴 QA integral — 5 h
- Flujos completos en entorno prod-like: reserva, compra digital, lead, agenda — 3 h
- Pruebas responsive (móvil/tablet/desktop) y cross-browser — 2 h

### 4.6 🔴 ⛔ Go-live — 4 h
*Depende de: 4.5 · decisión 4 (dominio)*
- Dominio + DNS + dominio de email verificado en Resend — 2 h
- Pasarela en modo live + smoke test de pago real — 1 h
- Checklist final y handoff a la clienta — 1 h

---

## ⛔ Decisiones pendientes que bloquean tareas

| # | Decisión | Bloquea | Recomendación |
|---|----------|---------|---------------|
| 1 | Pasarela de pago | 2.5, 3.3 | Stripe |
| 2 | Calendly vs Cal.com | 1.5 | Cal.com |
| 3 | Branding (¿logo/colores existentes?) | 0.3 → toda F0 | Definir antes de arrancar |
| 4 | Dominio | 4.6 | — |
| 5 | Hosting de video | 3.4 | Vimeo |
| 6 | Nº de alojamientos/inmuebles iniciales | 4.4 (dimensiona 1.1 y 2.1) | — |
| 7 | ¿Cobra videollamadas? | 1.5 | Afecta elección de agenda |

---

**Última actualización:** 2026-06-04 · Derivado de MASTER.md v0.1 (pre-cotización)
