# 🔑 KeyHandy — Contexto para Claude Code

> Proyecto en etapa de **COTIZACIÓN** (junio 2026). Plataforma web para clienta: reservas de alojamientos (iCal) + venta de contenido digital + catálogo inmobiliario + agenda de videollamadas.

## Protocolo de sesión

1. Lee `docs/MASTER.md` — fuente de verdad (alcance, stack, fases, decisiones pendientes).
2. Lee `docs/BITACORA.md` — última sesión y dónde quedamos.
3. Lee `docs/SPRINT_ACTUAL.md` — qué toca hoy.
4. Al cerrar sesión: actualiza la bitácora (entrada nueva arriba) y haz commit/push.

## Reglas heredadas de Mobbitrips (no negociables)

- Visualizador canónico único: `pnpm dev` → `http://localhost:3000`. NUNCA `file:///`.
- Scroll-reveal SIEMPRE con `<AnimatedSection>` (IntersectionObserver + CSS). NUNCA Framer Motion para scroll.
- NUNCA `overflow: clip` en globals.css (rompe la compilación CSS).
- Pull al iniciar + commit/push al cerrar, siempre.
- Nunca editar `main` directo — ramas `design/*`, `content/*`, `fix/*`.
- Secretos solo en `process.env.*`. APIs externas solo server-side. RLS activo en Supabase.

## Estado actual

- ⏳ Esperando confirmación de la clienta. No iniciar desarrollo de producto.
- Template base: `C:\Users\Emilio\mobbitrips-web-v2` (copiar tooling + packages/ui al cerrar trato).
