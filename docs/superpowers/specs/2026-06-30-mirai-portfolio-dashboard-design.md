# Mirai Portfolio Dashboard — Design Spec

**Fecha:** 2026-06-30  
**Proyecto:** Plataforma Mirai Investments  
**Cliente:** Astara Intelligence (Álvaro López)  
**Tipo:** PoC — primera entrega funcional  

---

## 1. Contexto y objetivo

Astara Intelligence analiza el portfolio de [Mirai Investments](https://mirai.investments), un family office industrial vasco con participaciones en 37 empresas activas distribuidas en 9 sectores. El objetivo de este PoC es crear una **plataforma web interna** que organice y presente toda esa información de forma clara, buscable y visualmente coherente con el design system de Astara Intelligence.

Los usuarios son el equipo interno de Astara Intelligence. No hay acceso público ni autenticación en esta primera versión.

---

## 2. Decisiones de diseño

| Decisión | Elección | Motivo |
|---|---|---|
| Audiencia | Equipo interno Astara Intelligence | Análisis privado de portfolio |
| Navegación | Tabs por sector (9 sectores) | Refleja la granularidad sectorial real del CSV |
| Formato de empresa | Cards ricas con avatar, definición, tags y badge | Máxima info visible sin abrir detalle |
| Iconografía | SVG monocromo de trazo fino en `--as-accent` (#1a4d7a) | Coherente con design system Astara; sin emojis |
| Datos vendidos/desinvertidos | Excluidos completamente | No interesan en el seguimiento activo |
| Implementación | HTML estático + `data.json` separado | Sin dependencias, fácil de actualizar datos |

---

## 3. Datos

**Fuente:** `PORTFOLIO(General).csv` (directorio raíz del proyecto)  
**Scope activo:** 37 empresas en 9 sectores (se excluyen Nutrición animal y Energías renovables por ser desinversiones completas)

### Sectores y recuento

| Sector | Empresas |
|---|---|
| Metal & equipment | 13 |
| Electrónica | 8 |
| Cosmética & personal care | 5 |
| Salud estética | 4 |
| Servicios ambientales | 3 |
| Moda | 1 |
| Agroindustria | 1 |
| Ferroviario | 1 |
| Inmobiliario | 1 |
| **Total** | **37** |

### Estructura de `data.json`

```json
{
  "sectors": [
    {
      "id": "metal",
      "name": "Metal & equipment",
      "companies": [
        {
          "name": "Innometal Group",
          "url": "https://mirai.investments/innometal-group/",
          "definition": "Plataforma industrial creada por Mirai desde la adquisición de IMAR en 2019.",
          "products": ["Transformación metálica", "Fabricación", "Montaje"],
          "status": "coparticipada",
          "platform": true
        }
      ]
    }
  ]
}
```

**Valores de `status`:** `"portfolio"` · `"integrated"` · `"coparticipada"`  
**Flag `platform: true`:** empresa madre de grupo — muestra borde navy izquierdo y aparece primera en la lista.

---

## 4. Arquitectura técnica

**Opción elegida:** HTML estático + JSON separado (Opción A del brainstorming).

```
07 PLATAFORMA MIRAI/
├── index.html          ← UI completa + lógica de filtrado
├── data.json           ← datos de las 37 empresas (editable sin tocar código)
└── PORTFOLIO(General).csv   ← fuente original (referencia)
```

`index.html` hace un `fetch('data.json')` al arrancar y renderiza toda la UI. Sin dependencias externas de JS ni build process. Se abre directamente en el navegador o se sirve desde cualquier servidor estático.

---

## 5. Componentes de la UI

### 5.1 Topbar (sticky)
- Fondo: gradiente navy `linear-gradient(135deg, #1a4d7a, #243a63, #221e41)`
- Izquierda: logo mark "M" + texto "Mirai **Investments**" (palabra en `--as-accent-light`)
- Derecha: etiqueta "Portfolio Intelligence" + badge "Astara Intelligence"
- Altura: 56px · z-index: 100

### 5.2 KPI Strip
- Fondo: mismo gradiente navy + glow radial en esquina superior derecha (`rgba(139,205,255,.18)`)
- 3 cards glassmorphic:
  - **Total empresas** (featured, electric-blue): **37**
  - **Adquiridas / Integradas**: número de empresas con status `portfolio` o `integrated` (excluye coparticipadas)
  - **Sectores**: **9**
- Padding: 24px 32px · max-width: 1200px centrado

### 5.3 Tab navigation (sticky, bajo el topbar)
- 9 tabs, una por sector, con contador de empresas como badge circular
- Estilo pill: activa = fondo blanco + `--as-shadow-md`; inactiva = transparente
- Scroll horizontal sin scrollbar en overflow
- Fondo: `rgba(255,255,255,.92)` + `backdrop-filter: blur(10px)`
- z-index: 90 (bajo el topbar)

### 5.4 Barra de filtros
- Barra pill blanca con: icono lupa SVG navy + input de búsqueda por nombre + separador + 4 chips
- Chips: **Todas** · **En cartera** · **Integrada** · **Coparticipada**
- Activo: fondo `--as-accent` blanco · hover: borde + texto navy
- Filtra en tiempo real sobre las cards del sector activo

### 5.5 Company Cards (rich)
- Layout: avatar (44×44 iniciales) + cuerpo (nombre, definición, tags) + derecha (badge estado + enlace)
- Avatar: gradiente navy, color `--as-accent-light`, 2 letras iniciales
- Nombre: 15px bold navy
- Definición: 13px `--as-fg-2`, 1.45 line-height
- Tags: pills `--as-accent` sobre fondo `rgba(26,77,122,.07)`
- Badge estado: colores por tipo (verde = portfolio, azul = coparticipada, teal = integrated)
- Enlace: "mirai.investments" + icono flecha diagonal SVG en `--as-accent-light`
- Hover: `translateY(-1px)` + `--as-shadow-md` + borde `rgba(26,77,122,.25)`
- **Plataformas madre** (`platform: true`): borde izquierdo 3px navy + fondo `--as-surface-muted`, ordenadas primero

### 5.6 Modal de detalle
- Se abre al clicar cualquier card
- Header: gradiente navy + glow + avatar grande + nombre + sector/estado como eyebrow
- Body: campo Estado (badge) + enlace CTA a mirai.investments · Definición completa · Productos como tags · Contexto de inversión (texto literal del campo "Estado" del CSV, que incluye información de estructura accionarial y referencia de fuente)
- Cierre: botón × SVG, clic en backdrop, Escape
- Backdrop: `rgba(34,30,65,.45)` + `backdrop-filter: blur(4px)`
- Animación de entrada: `opacity 0→1` + `translateY(12px→0)` + `scale(.98→1)` en 220ms

---

## 6. Design system aplicado

Todos los valores se leen de tokens CSS (bloque `:root`). Se usa el design system completo de Astara Intelligence definido en `ASTARA_DASHBOARD_DESIGN_SYSTEM.md`:

- **Tipografía:** Montserrat 400/500/600/700 (máximo 700, nunca 800/900)
- **Colores:** tokens `--as-*` del §11 del design system
- **Iconografía:** SVG stroke monocromo en `--as-accent`, grosor 1.6px, `stroke-linecap: round`
- **Sombras:** `--as-shadow-sm` en reposo, `--as-shadow-md` en hover
- **Radios:** cards `--as-radius-lg (22px)`, controles `--as-radius-md (16px)`, pills `--as-radius-pill`
- **Movimiento:** `cubic-bezier(.2,.7,.2,1)`, `--as-dur (200ms)`, colapsa bajo `prefers-reduced-motion`
- **Reglas duras:** sin em-dashes, sin pesos >700, sin colores fuera de paleta como accents UI, sin `overflow:hidden` en hosts de dropdowns

---

## 7. Alcance del PoC

### Incluido
- [x] Topbar sticky navy con identidad visual
- [x] KPI strip con 3 métricas (37 empresas, en cartera, 9 sectores)
- [x] 9 tabs por sector con contadores
- [x] Cards ricas para las 37 empresas completas (todos los datos del CSV)
- [x] Filtro por estado (4 chips) + búsqueda por nombre en tiempo real
- [x] Modal de detalle con información completa
- [x] Enlace directo a ficha mirai.investments desde card y modal
- [x] Design system Astara Intelligence completo
- [x] Responsive desktop y tablet (≥ 768px)

### Excluido (iteración siguiente)
- [ ] Logos reales de cada empresa (ahora: avatares de iniciales)
- [ ] Métricas financieras (facturación, EBITDA, participación %)
- [ ] Gráficos de evolución temporal
- [ ] Exportar a PDF / Excel
- [ ] Autenticación y control de acceso
- [ ] Backend o base de datos
- [ ] Edición inline de fichas
- [ ] Vista móvil optimizada (< 480px)

---

## 8. Flujo de actualización de datos

Para añadir o editar empresas en el futuro, el flujo es:

1. Editar `data.json` — añadir/modificar objetos en el array `companies` del sector correspondiente
2. Recargar `index.html` en el navegador — los cambios se reflejan automáticamente
3. Para un sector nuevo: añadir un objeto al array `sectors` con `id`, `name` y `companies`

---

*Spec aprobado por Álvaro López — 2026-06-30*
