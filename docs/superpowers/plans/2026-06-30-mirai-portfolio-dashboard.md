# Mirai Portfolio Dashboard — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Construir un dashboard web estático (HTML + JSON) que muestra las 37 empresas activas del portfolio de Mirai Investments, organizadas por sector, con diseño Astara Intelligence.

**Architecture:** Un único `index.html` con todos los tokens CSS, componentes y lógica JS; un `data.json` que contiene las 37 empresas agrupadas por sector y que se carga con `fetch()` al arrancar. Sin build process, sin dependencias externas de JS — funciona abriéndolo directamente en el navegador.

**Tech Stack:** HTML5 · CSS3 (custom properties) · Vanilla JavaScript (ES2020) · Montserrat via Google Fonts · SVG icons inline · Fetch API

**Assets disponibles:**
- `assets/logo-white.png` — logo Astara Intelligence blanco (para topbar navy)
- `assets/logo-dark.svg` — logo Astara Intelligence oscuro (reserva)
- `docs/superpowers/specs/2026-06-30-mirai-portfolio-dashboard-design.md` — spec completo

---

## File map

| Fichero | Responsabilidad |
|---|---|
| `data.json` | Datos de 37 empresas en 9 sectores (única fuente de verdad) |
| `index.html` | UI completa: tokens CSS + HTML shell + JS de toda la lógica |
| `assets/logo-white.png` | Logo Astara Intelligence para topbar (ya copiado) |

---

## Task 1: Crear `data.json` con las 37 empresas

**Files:**
- Create: `data.json`

- [ ] **Step 1.1: Crear `data.json` con todos los sectores y empresas**

Crear el fichero en la raíz del proyecto con el siguiente contenido completo:

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
          "definition": "Plataforma industrial creada por Mirai desde la adquisición inicial de IMAR en 2019.",
          "products": ["Transformación metálica", "Fabricación", "Montaje", "Componentes industriales"],
          "status": "coparticipada",
          "platform": true
        },
        {
          "name": "IMAR",
          "url": "https://mirai.investments/portfolio/imar/",
          "definition": "Compañía industrial de transformación metálica; primera base de Innometal.",
          "products": ["Chapa perforada", "Chapa plegada", "Chapa punzonada", "Soluciones arquitectónicas"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Naivan",
          "url": "https://mirai.investments/portfolio/naivan/",
          "definition": "Empresa de transformación metálica y fabricación de estructuras y componentes de acero y aluminio.",
          "products": ["Maquinaria industrial", "Ferrocarril", "Aeronáutica", "Energías renovables"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Fervilor",
          "url": "https://mirai.investments/portfolio/fervilor/",
          "definition": "Empresa de corte, soldadura y transformación de chapa para industria, automoción y construcción.",
          "products": ["Corte láser", "Soldadura", "Plegado", "Automoción", "Maquinaria agrícola"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Model Metal",
          "url": "https://mirai.investments/portfolio/model-metal/",
          "definition": "Centro de servicio y transformación metálica. Integra las unidades productivas Servichap y Peymo.",
          "products": ["Corte de bobina", "Estructuras metálicas"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Servichap",
          "url": "https://mirai.investments/portfolio/model-metal/",
          "definition": "Unidad productiva incorporada dentro de Model Metal. Servicio de chapa y transformación metálica.",
          "products": ["Transformación de chapa"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Peymo",
          "url": "https://mirai.investments/portfolio/model-metal/",
          "definition": "Unidad productiva incorporada dentro de Model Metal. Producción y transformación de estructuras metálicas.",
          "products": ["Estructuras metálicas"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Afarvi",
          "url": "https://mirai.investments/portfolio/afarvi/",
          "definition": "Ingeniería y fabricación de sistemas de proceso de agua para farmacéutica, cosmética y alimentación.",
          "products": ["Diseño de sistemas", "Fabricación", "Montaje", "Mantenimiento", "Agua farmacéutica"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "MAM",
          "url": "https://mirai.investments/portfolio/mam/",
          "definition": "Empresa catalana de estructuras y componentes metálicos complejos con ensamblajes electromecánicos.",
          "products": ["Corte láser", "Soldadura", "Plegado", "Ensamblajes electromecánicos"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Metalec",
          "url": "https://www.innometalgroup.com/en/mam-and-metalec-join-innometal-group/",
          "definition": "Empresa integrada en Innometal junto con MAM. Componentes y soluciones de transformación metálica.",
          "products": ["Transformación metálica", "Componentes industriales"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Tecro Spaces",
          "url": "https://www.innometalgroup.com/en/mirai-acquires-the-company-tecro-spaces-located-in-la-rioja/",
          "definition": "Compañía riojana especializada en soluciones metálicas modulares para optimización de espacios.",
          "products": ["Entreplantas", "Altillos", "Estructuras modulares metálicas"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "IMAT",
          "url": "https://capital-riesgo.es/en/articles/mirai-investments-acquires-lava-based-company-imat/",
          "definition": "Compañía alavesa especializada en mobiliario aeroportuario con fuerte perfil exportador.",
          "products": ["Asientos aeroportuarios", "Mobiliario para aeropuertos", "Exportación"],
          "status": "integrated",
          "platform": false
        }
      ]
    },
    {
      "id": "electronica",
      "name": "Electrónica",
      "companies": [
        {
          "name": "Ohmnia Group",
          "url": "https://mirai.investments/en/ohmnia-2/",
          "definition": "Plataforma de electrónica industrial creada desde la adquisición de TER. One-stop shop de fabricación electrónica.",
          "products": ["Diseño electrónico", "Industrialización", "Fabricación", "Montaje"],
          "status": "coparticipada",
          "platform": true
        },
        {
          "name": "TER / Técnicas Electrónicas Reunidas",
          "url": "https://mirai.investments/en/ohmnia-2/",
          "definition": "Primera compañía sobre la que se construye Ohmnia. Soluciones de industrialización de producto electrónico.",
          "products": ["Industrialización electrónica"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Coycavi",
          "url": "https://mirai.investments/portfolio/coycavi/",
          "definition": "Empresa especializada en cableado e interconexión para industrias técnicas de alta exigencia.",
          "products": ["Cable harnesses", "Interconexiones", "Renovables", "Ferrocarril", "Automatización"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Tectron",
          "url": "https://mirai.investments/portfolio/tectron/",
          "definition": "Fabricante de interfaces y componentes electrónicos de control para equipamiento especializado.",
          "products": ["Membranas", "Teclados capacitivos", "Frontales", "Electromedicina", "Elevadores"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "IDK Elektronika",
          "url": "https://mirai.investments/portfolio/idk/",
          "definition": "Empresa de montaje de circuitos electrónicos para vehículo eléctrico, IoT y smart city.",
          "products": ["Tarjetas electrónicas", "Vehículo eléctrico", "Control de accesos", "Ferrocarril", "IoT"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Alcoelectro",
          "url": "https://mirai.investments/portfolio/alcoelectro/",
          "definition": "Empresa madrileña de montaje y fabricación electrónica para sectores industriales y de consumo.",
          "products": ["Iluminación", "Aeronáutica", "Telecomunicaciones", "Electromedicina", "Ferrocarril"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Arteixo Telecom",
          "url": "https://mirai.investments/portfolio/arteixo-telecom/",
          "definition": "Empresa gallega de diseño y fabricación de electrónica avanzada para sectores de alta fiabilidad.",
          "products": ["Aeronáutica", "Ferrocarril", "Renovables", "Defensa"],
          "status": "portfolio",
          "platform": false
        },
        {
          "name": "Idistek",
          "url": "https://mirai.investments/portfolio/idistek-2/",
          "definition": "Empresa vasca de diseño, fabricación e industrialización electrónica de conjuntos complejos.",
          "products": ["Placas electrónicas", "Conjuntos complejos", "Diseño", "Industrialización"],
          "status": "portfolio",
          "platform": false
        }
      ]
    },
    {
      "id": "cosmetica",
      "name": "Cosmética & personal care",
      "companies": [
        {
          "name": "Labery",
          "url": "https://mirai.investments/en/labery/",
          "definition": "División cosmética de Mirai, creada por integración de cuatro compañías. CDMO full-service.",
          "products": ["Ideación", "Formulación", "Fabricación", "Packaging", "Logística"],
          "status": "portfolio",
          "platform": true
        },
        {
          "name": "Laboratorios Coper",
          "url": "https://mirai.investments/portfolio/laboratorios-coper/",
          "definition": "CDMO de cosmética y perfumería premium integrado en Labery.",
          "products": ["Formulación", "Fabricación", "Envasado", "Acondicionamiento"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Jumsa Cosmetic",
          "url": "https://mirai.investments/portfolio/laboratorios-coper/",
          "definition": "Compañía de fabricación y llenado de productos cosméticos y perfumería integrada en Labery.",
          "products": ["Fabricación cosmética", "Llenado", "Perfumería"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Cosmeprint",
          "url": "https://mirai.investments/en/our-portfolio/cosmeprint/",
          "definition": "Especialista catalana en consultoría y distribución de packaging para cosmética.",
          "products": ["Packaging cosmético", "Diseño", "Acabados", "Alternativas recicladas"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Ternum Cosmetics",
          "url": "https://mirai.investments/en/our-portfolio/ternum-cosmetics/",
          "definition": "Empresa de creación, diseño y formulación cosmética a medida con más de 2.000 formulaciones.",
          "products": ["I+D cosmético", "Formulación", "Soporte técnico de fabricación"],
          "status": "integrated",
          "platform": false
        }
      ]
    },
    {
      "id": "salud",
      "name": "Salud estética",
      "companies": [
        {
          "name": "Grupo Salud Mirai",
          "url": "https://mirai.investments/salud/",
          "definition": "Plataforma de medicina y cirugía estética con presencia multiclínica.",
          "products": ["Medicina estética", "Cirugía estética", "Medicina capilar", "Tratamientos faciales"],
          "status": "portfolio",
          "platform": true
        },
        {
          "name": "Clínicas Diego de León",
          "url": "https://mirai.investments/portfolio/clinicas-diego-de-leon/",
          "definition": "Clínica de medicina y cirugía estética en Madrid integrada en el Grupo Salud Mirai.",
          "products": ["Cirugía facial", "Cirugía corporal", "Medicina estética"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Livet",
          "url": "https://mirai.investments/salud/",
          "definition": "Centro especializado en medicina y cirugía capilar integrado en el Grupo Salud Mirai.",
          "products": ["Medicina capilar", "Cirugía capilar", "Tratamientos médicos capilares"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Facial Clinique",
          "url": "https://mirai.investments/portfolio/facial-clinique/",
          "definition": "Red de clínicas de medicina estética facial integrada en el Grupo Salud Mirai.",
          "products": ["Medicina estética avanzada", "Pequeñas cirugías faciales", "Diagnóstico facial"],
          "status": "integrated",
          "platform": false
        }
      ]
    },
    {
      "id": "moda",
      "name": "Moda",
      "companies": [
        {
          "name": "Batela",
          "url": "https://mirai.investments/mirai-investments-adquiere-la-marca-vasca-de-moda-nautica-batela-para-impulsar-su-crecimiento/",
          "definition": "Marca vasca de moda náutica fundada en Getaria. Incluye la marca Tanté.",
          "products": ["Ropa náutica", "Moda impermeable", "1.500 referencias"],
          "status": "portfolio",
          "platform": false
        }
      ]
    },
    {
      "id": "agroindustria",
      "name": "Agroindustria",
      "companies": [
        {
          "name": "ISFA / Iberian Smart Financial Agro",
          "url": "https://mirai.investments/en/our-portfolio/isfa/",
          "definition": "Proyecto de industrialización agrícola centrado en almendro con sistema de cultivo eficiente SES.",
          "products": ["Cultivos eficientes", "Almendro", "Cultivos de alto valor", "Gestión agroindustrial"],
          "status": "coparticipada",
          "platform": false
        }
      ]
    },
    {
      "id": "ambiental",
      "name": "Servicios ambientales",
      "companies": [
        {
          "name": "Servicios Ambientales Mirai",
          "url": "https://mirai.investments/afesa-y-mendiola/",
          "definition": "Plataforma ambiental creada con Afesa y Excavaciones Mendiola para el sector industrial.",
          "products": ["Suelos contaminados", "Demolición industrial", "Gestión de residuos", "Excavación"],
          "status": "portfolio",
          "platform": true
        },
        {
          "name": "AFESA",
          "url": "https://www.afesa.es",
          "definition": "Empresa de tratamiento ambiental e industrial para energía, construcción e industria pesada.",
          "products": ["Suelos contaminados", "Residuos industriales", "Demolición", "Servicios ambientales"],
          "status": "integrated",
          "platform": false
        },
        {
          "name": "Excavaciones Mendiola",
          "url": "https://www.mendiola.es",
          "definition": "Empresa de excavación, demolición y gestión de residuos de construcción y demolición.",
          "products": ["Excavaciones", "Demolición industrial", "Gestión de RCD"],
          "status": "integrated",
          "platform": false
        }
      ]
    },
    {
      "id": "ferroviario",
      "name": "Ferroviario",
      "companies": [
        {
          "name": "Talgo",
          "url": "https://www.alantra.com/ib-transaction/mirai-investments-buy-side-advisory-talgo/",
          "definition": "Participación indirecta a través de consorcio inversor liderado por Mirai sobre el 29,8% de Talgo.",
          "products": ["Fabricación ferroviaria", "Trenes de alta velocidad", "Material rodante"],
          "status": "coparticipada",
          "platform": false
        }
      ]
    },
    {
      "id": "inmobiliario",
      "name": "Inmobiliario",
      "companies": [
        {
          "name": "Uztagroup",
          "url": "https://mirai.investments/en/our-track-record/",
          "definition": "Operación histórica listada en el track record de Mirai con actividad inmobiliaria.",
          "products": ["Actividad inmobiliaria"],
          "status": "portfolio",
          "platform": false
        }
      ]
    }
  ]
}
```

- [ ] **Step 1.2: Verificar el JSON**

Abrir una terminal y ejecutar:

```powershell
Get-Content "data.json" | ConvertFrom-Json | Select-Object -ExpandProperty sectors | ForEach-Object { "$($_.name): $($_.companies.Count) empresas" }
```

Salida esperada:
```
Metal & equipment: 12 empresas
Electrónica: 8 empresas
Cosmética & personal care: 5 empresas
Salud estética: 4 empresas
Moda: 1 empresas
Agroindustria: 1 empresas
Servicios ambientales: 3 empresas
Ferroviario: 1 empresas
Inmobiliario: 1 empresas
```

---

## Task 2: Crear `index.html` — shell y tokens CSS

**Files:**
- Create: `index.html`

- [ ] **Step 2.1: Crear el esqueleto HTML con todos los tokens Astara**

```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mirai Investments · Portfolio Intelligence</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
/* ═══════════════════════════════════════════
   ASTARA INTELLIGENCE DESIGN SYSTEM — TOKENS
═══════════════════════════════════════════ */
:root {
  --as-bg-page: #f2f4f6;
  --as-surface: #ffffff;
  --as-surface-muted: #f8fbff;
  --as-bg-dark: #221e41;
  --as-bg-mid: #243a63;
  --as-accent: #1a4d7a;
  --as-accent-strong: #143d61;
  --as-accent-light: #8bcdff;
  --as-accent-teal: #86bfc6;
  --as-accent-lime: #c1e14e;
  --as-fg-1: #221e41;
  --as-fg-2: #2e4a62;
  --as-fg-3: #5a7a94;
  --as-fg-on-dark: #eaf1f8;
  --as-border: #c4d3df;
  --as-border-subtle: rgba(26,77,122,.10);
  --as-success: #2f7d5b;
  --as-warning: #8a6d1f;
  --as-danger: #b4452f;
  --as-shadow-sm: 0 8px 20px rgba(34,30,65,.05);
  --as-shadow-md: 0 14px 30px rgba(26,77,122,.12);
  --as-shadow-lg: 0 30px 70px rgba(34,30,65,.24);
  --as-radius-xs: 8px;
  --as-radius-sm: 12px;
  --as-radius-md: 16px;
  --as-radius-lg: 22px;
  --as-radius-pill: 9999px;
  --as-font-sans: 'Montserrat', ui-sans-serif, system-ui, sans-serif;
  --as-text-xs: 11px;
  --as-text-sm: 13px;
  --as-text-base: 15px;
  --as-text-lg: 18px;
  --as-text-xl: 22px;
  --as-text-2xl: 28px;
  --as-text-3xl: 36px;
  --as-dur-fast: 120ms;
  --as-dur: 200ms;
  --as-dur-slow: 320ms;
  --as-ease: cubic-bezier(.2,.7,.2,1);
  --as-z-dropdown: 400;
  --as-z-overlay: 1000;
  --as-z-modal: 1010;
}
@media (prefers-reduced-motion: reduce) {
  :root { --as-dur-fast: 0ms; --as-dur: 0ms; --as-dur-slow: 0ms; }
}

/* ── RESET ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body {
  font-family: var(--as-font-sans);
  background: var(--as-bg-page);
  color: var(--as-fg-1);
  font-size: var(--as-text-base);
  line-height: 1.5;
  min-height: 100vh;
}
button { font-family: var(--as-font-sans); cursor: pointer; }
a { text-decoration: none; }
</style>
</head>
<body>

<!-- TOPBAR -->
<header id="topbar"></header>

<!-- KPI STRIP -->
<section id="kpi-strip"></section>

<!-- TABS + CONTENT -->
<div id="tabs-wrapper">
  <nav id="tablist" role="tablist" aria-label="Sectores del portfolio"></nav>
</div>

<main id="main-content">
  <!-- FILTER BAR -->
  <div id="filter-bar-wrap"></div>
  <!-- COMPANY CARDS -->
  <div id="cards-container" role="tabpanel"></div>
</main>

<!-- MODAL -->
<div id="modal-backdrop" role="dialog" aria-modal="true" aria-labelledby="modal-company-name" hidden></div>

<script>
// ═══════════════════════════════════════════
//  MIRAI PORTFOLIO DASHBOARD — main.js
// ═══════════════════════════════════════════
// State
let allData = null;
let activeSectorId = null;
let activeFilter = 'all';
let searchQuery = '';

// Boot
document.addEventListener('DOMContentLoaded', init);

async function init() {
  const res = await fetch('data.json');
  allData = await res.json();
  renderTopbar();
  renderKpiStrip();
  renderTabs();
  setActiveSector(allData.sectors[0].id);
}
</script>
</body>
</html>
```

- [ ] **Step 2.2: Verificar en el navegador**

Abrir `index.html` directamente en el navegador (doble clic o arrastrar).  
Abrir DevTools → consola: no debe haber errores. La página aparece en blanco (normal — aún no hay CSS de componentes).

---

## Task 3: CSS de todos los componentes

**Files:**
- Modify: `index.html` — añadir bloque CSS de componentes dentro del `<style>` existente, antes del cierre `</style>`

- [ ] **Step 3.1: Añadir CSS del topbar**

```css
/* ── TOPBAR ── */
#topbar {
  position: sticky; top: 0; z-index: 100;
  background: linear-gradient(135deg, #1a4d7a 0%, #243a63 52%, #221e41 100%);
  padding: 0 32px;
  display: flex; align-items: center; justify-content: space-between;
  height: 56px;
  box-shadow: var(--as-shadow-md);
}
.topbar-logo { display: flex; align-items: center; gap: 12px; }
.topbar-logo img { height: 28px; width: auto; object-fit: contain; }
.topbar-product {
  font-size: var(--as-text-sm); font-weight: 600;
  color: rgba(234,241,248,.5); letter-spacing: .06em;
  border-left: 1px solid rgba(255,255,255,.15); padding-left: 12px;
}
.topbar-meta { display: flex; align-items: center; gap: 12px; }
.topbar-badge {
  background: rgba(139,205,255,.15); border: 1px solid rgba(139,205,255,.3);
  color: var(--as-accent-light); font-size: var(--as-text-xs); font-weight: 700;
  padding: 3px 10px; border-radius: var(--as-radius-pill); letter-spacing: .05em;
}
```

- [ ] **Step 3.2: Añadir CSS del KPI strip**

```css
/* ── KPI STRIP ── */
#kpi-strip {
  background: linear-gradient(135deg, #1a4d7a 0%, #243a63 52%, #221e41 100%);
  padding: 24px 32px 28px;
  position: relative; overflow: hidden;
}
#kpi-strip::before {
  content: ''; position: absolute; top: -40%; right: -5%;
  width: 50%; height: 200%;
  background: radial-gradient(ellipse, rgba(139,205,255,.18) 0%, transparent 65%);
  pointer-events: none;
}
.kpi-eyebrow {
  font-size: var(--as-text-xs); font-weight: 700; letter-spacing: .14em;
  text-transform: uppercase; color: var(--as-accent-light);
  margin-bottom: 16px; opacity: .85;
  max-width: 1200px; margin-left: auto; margin-right: auto;
}
.kpi-row {
  display: flex; gap: 12px;
  max-width: 1200px; margin: 0 auto;
}
.kpi-card {
  flex: 1; background: rgba(255,255,255,.07);
  border: 1px solid rgba(139,205,255,.15);
  border-radius: var(--as-radius-md); padding: 16px 20px;
  backdrop-filter: blur(8px);
}
.kpi-card.featured {
  background: rgba(139,205,255,.15);
  border-color: rgba(139,205,255,.35);
}
.kpi-label {
  font-size: var(--as-text-xs); font-weight: 700; letter-spacing: .12em;
  text-transform: uppercase; color: rgba(234,241,248,.55); margin-bottom: 8px;
}
.kpi-value {
  font-size: var(--as-text-2xl); font-weight: 700;
  color: var(--as-fg-on-dark); letter-spacing: -0.02em; line-height: 1;
}
.kpi-card.featured .kpi-value { color: var(--as-accent-light); }
.kpi-note { font-size: var(--as-text-xs); color: rgba(234,241,248,.45); margin-top: 4px; }
```

- [ ] **Step 3.3: Añadir CSS de tabs**

```css
/* ── TABS ── */
#tabs-wrapper {
  background: rgba(255,255,255,.92); backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--as-border);
  padding: 0 32px;
  position: sticky; top: 56px; z-index: 90;
}
#tablist {
  display: flex; gap: 2px; overflow-x: auto;
  scrollbar-width: none; padding: 8px 0;
  max-width: 1200px; margin: 0 auto;
}
#tablist::-webkit-scrollbar { display: none; }
.tab-btn {
  flex-shrink: 0; padding: 7px 16px;
  border-radius: var(--as-radius-pill);
  font-size: var(--as-text-sm); font-weight: 600;
  color: var(--as-fg-3); border: none; background: transparent;
  white-space: nowrap; transition: background var(--as-dur) var(--as-ease), color var(--as-dur) var(--as-ease), box-shadow var(--as-dur) var(--as-ease);
}
.tab-btn:hover { background: rgba(26,77,122,.06); color: var(--as-accent); }
.tab-btn[aria-selected="true"] {
  background: var(--as-surface); color: var(--as-accent);
  box-shadow: var(--as-shadow-md);
}
.tab-count {
  display: inline-flex; align-items: center; justify-content: center;
  width: 18px; height: 18px; border-radius: 50%;
  background: rgba(26,77,122,.1); color: var(--as-accent);
  font-size: 10px; font-weight: 700; margin-left: 5px;
  transition: background var(--as-dur), color var(--as-dur);
}
.tab-btn[aria-selected="true"] .tab-count { background: var(--as-accent); color: #fff; }
```

- [ ] **Step 3.4: Añadir CSS de filtros y contenido**

```css
/* ── MAIN CONTENT ── */
#main-content {
  max-width: 1200px; margin: 0 auto;
  padding: 28px 32px 64px;
}

/* ── FILTER BAR ── */
.filter-bar {
  display: flex; align-items: center; gap: 10px;
  background: var(--as-surface); border: 1px solid var(--as-border);
  border-radius: var(--as-radius-pill); padding: 8px 16px;
  margin-bottom: 24px; box-shadow: var(--as-shadow-sm);
}
.filter-icon { display: flex; align-items: center; flex-shrink: 0; }
.filter-search {
  flex: 1; border: none; outline: none;
  font-family: var(--as-font-sans); font-size: var(--as-text-sm);
  color: var(--as-fg-2); background: transparent;
}
.filter-search::placeholder { color: var(--as-fg-3); }
.filter-sep { width: 1px; height: 20px; background: var(--as-border); flex-shrink: 0; }
.filter-chip {
  font-size: var(--as-text-xs); font-weight: 700; padding: 4px 12px;
  border-radius: var(--as-radius-pill); border: 1.5px solid var(--as-border);
  background: transparent; color: var(--as-fg-3); white-space: nowrap;
  transition: all var(--as-dur-fast) var(--as-ease);
}
.filter-chip:hover:not([aria-pressed="true"]) { border-color: var(--as-accent); color: var(--as-accent); }
.filter-chip[aria-pressed="true"] { background: var(--as-accent); color: #fff; border-color: var(--as-accent); }

/* ── SECTOR HEADER ── */
.sector-header { display: flex; align-items: baseline; gap: 12px; margin-bottom: 20px; }
.sector-eyebrow {
  font-size: var(--as-text-xs); font-weight: 700; letter-spacing: .13em;
  text-transform: uppercase; color: var(--as-fg-3); margin-bottom: 4px;
}
.sector-title { font-size: var(--as-text-xl); font-weight: 700; letter-spacing: -0.02em; }
.sector-count { font-size: var(--as-text-sm); color: var(--as-fg-3); font-weight: 500; }

/* ── COMPANY CARDS ── */
#cards-container { display: flex; flex-direction: column; gap: 10px; }
.company-card {
  background: var(--as-surface); border: 1px solid var(--as-border);
  border-radius: var(--as-radius-lg); padding: 18px 22px;
  display: flex; align-items: flex-start; gap: 16px;
  box-shadow: var(--as-shadow-sm);
  transition: box-shadow var(--as-dur) var(--as-ease), transform var(--as-dur) var(--as-ease), border-color var(--as-dur) var(--as-ease);
  cursor: pointer;
}
.company-card:hover {
  box-shadow: var(--as-shadow-md); transform: translateY(-1px);
  border-color: rgba(26,77,122,.25);
}
.company-card:focus-visible {
  outline: 3px solid var(--as-accent); outline-offset: 2px;
}
.company-card.platform { border-left: 3px solid var(--as-accent); background: var(--as-surface-muted); }

.card-avatar {
  width: 44px; height: 44px; border-radius: 12px; flex-shrink: 0;
  background: linear-gradient(135deg, var(--as-accent) 0%, #243a63 100%);
  display: flex; align-items: center; justify-content: center;
  color: var(--as-accent-light); font-size: 13px; font-weight: 700;
  letter-spacing: -.01em; user-select: none;
}
.card-body { flex: 1; min-width: 0; }
.card-name { font-size: var(--as-text-base); font-weight: 700; color: var(--as-fg-1); margin-bottom: 4px; }
.card-def { font-size: var(--as-text-sm); color: var(--as-fg-2); margin-bottom: 8px; line-height: 1.45; }
.card-tags { display: flex; flex-wrap: wrap; gap: 5px; }
.card-tag {
  font-size: var(--as-text-xs); font-weight: 600; padding: 3px 9px;
  border-radius: var(--as-radius-pill);
  background: rgba(26,77,122,.07); color: var(--as-accent);
  border: 1px solid rgba(26,77,122,.12);
}
.card-right { display: flex; flex-direction: column; align-items: flex-end; gap: 8px; flex-shrink: 0; }

.status-badge { font-size: var(--as-text-xs); font-weight: 700; padding: 4px 12px; border-radius: var(--as-radius-pill); white-space: nowrap; }
.status-portfolio  { background: rgba(47,125,91,.1);  color: #2f7d5b; border: 1px solid rgba(47,125,91,.2);  }
.status-integrated { background: rgba(134,191,198,.15); color: #2e7580; border: 1px solid rgba(134,191,198,.3); }
.status-coparticipada { background: rgba(26,77,122,.1); color: var(--as-accent); border: 1px solid rgba(26,77,122,.2); }

.card-link {
  font-size: var(--as-text-xs); color: var(--as-accent-light);
  font-weight: 600; opacity: .8; display: flex; align-items: center; gap: 4px;
  transition: opacity var(--as-dur-fast);
}
.card-link:hover { opacity: 1; }

/* ── EMPTY STATE ── */
.empty-state {
  text-align: center; padding: 48px 24px;
  color: var(--as-fg-3); font-size: var(--as-text-sm);
}
.empty-state p { margin-top: 8px; }
```

- [ ] **Step 3.5: Añadir CSS del modal**

```css
/* ── MODAL ── */
#modal-backdrop {
  position: fixed; inset: 0; z-index: var(--as-z-overlay);
  background: rgba(34,30,65,.45); backdrop-filter: blur(4px);
  display: flex; align-items: center; justify-content: center; padding: 24px;
}
#modal-backdrop[hidden] { display: none; }

.modal {
  background: var(--as-surface); border-radius: var(--as-radius-lg);
  width: 100%; max-width: 620px; max-height: 90vh; overflow-y: auto;
  box-shadow: var(--as-shadow-lg);
  animation: modal-in var(--as-dur-slow) var(--as-ease);
}
@keyframes modal-in {
  from { opacity: 0; transform: translateY(12px) scale(.98); }
  to   { opacity: 1; transform: none; }
}
.modal-header {
  background: linear-gradient(135deg, #1a4d7a 0%, #243a63 52%, #221e41 100%);
  border-radius: var(--as-radius-lg) var(--as-radius-lg) 0 0;
  padding: 24px 28px; position: relative; overflow: hidden;
}
.modal-header::before {
  content: ''; position: absolute; top: -30%; right: -5%; width: 50%; height: 160%;
  background: radial-gradient(ellipse, rgba(139,205,255,.2) 0%, transparent 65%);
  pointer-events: none;
}
.modal-close {
  position: absolute; top: 18px; right: 20px;
  width: 28px; height: 28px; border-radius: 50%;
  background: rgba(255,255,255,.12); border: none; cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  transition: background var(--as-dur-fast);
}
.modal-close:hover { background: rgba(255,255,255,.22); }
.modal-close:focus-visible { outline: 3px solid var(--as-accent-light); outline-offset: 2px; }
.modal-avatar {
  width: 52px; height: 52px; border-radius: 14px;
  background: rgba(139,205,255,.18); border: 1.5px solid rgba(139,205,255,.35);
  display: flex; align-items: center; justify-content: center;
  color: var(--as-accent-light); font-size: 16px; font-weight: 700; margin-bottom: 12px;
  user-select: none;
}
.modal-name { font-size: var(--as-text-xl); font-weight: 700; color: var(--as-fg-on-dark); letter-spacing: -.02em; margin-bottom: 4px; }
.modal-sector { font-size: var(--as-text-xs); font-weight: 700; letter-spacing: .12em; text-transform: uppercase; color: rgba(139,205,255,.7); }
.modal-body { padding: 24px 28px; }
.modal-status-row { display: flex; align-items: center; justify-content: space-between; margin-bottom: 20px; flex-wrap: wrap; gap: 10px; }
.modal-status-label { font-size: var(--as-text-xs); font-weight: 700; letter-spacing: .13em; text-transform: uppercase; color: var(--as-fg-3); margin-bottom: 6px; }
.modal-link {
  display: inline-flex; align-items: center; gap: 6px;
  font-size: var(--as-text-xs); font-weight: 700; color: var(--as-accent);
  background: rgba(26,77,122,.07); border: 1.5px solid rgba(26,77,122,.15);
  padding: 7px 16px; border-radius: var(--as-radius-pill);
  transition: all var(--as-dur-fast) var(--as-ease);
}
.modal-link:hover { background: var(--as-accent); color: #fff; border-color: var(--as-accent); }
.modal-link:focus-visible { outline: 3px solid var(--as-accent); outline-offset: 2px; }
.modal-divider { border: none; border-top: 1px solid var(--as-border); margin: 0 0 20px; }
.modal-field { margin-bottom: 20px; }
.field-label { font-size: var(--as-text-xs); font-weight: 700; letter-spacing: .13em; text-transform: uppercase; color: var(--as-fg-3); margin-bottom: 6px; }
.field-value { font-size: 14px; color: var(--as-fg-2); line-height: 1.55; }
.field-tags { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 4px; }
.field-tag {
  font-size: var(--as-text-xs); font-weight: 600; padding: 4px 11px;
  border-radius: var(--as-radius-pill);
  background: rgba(26,77,122,.07); color: var(--as-accent); border: 1px solid rgba(26,77,122,.12);
}
```

- [ ] **Step 3.6: Verificar en el navegador**

Recargar `index.html`. La página sigue en blanco pero sin errores en consola. Los estilos están definidos pero no hay HTML renderizado aún.

---

## Task 4: Renderizar topbar y KPI strip

**Files:**
- Modify: `index.html` — añadir funciones JS en el bloque `<script>`

- [ ] **Step 4.1: Función `renderTopbar()`**

Añadir dentro del `<script>`, después de la función `init`:

```javascript
function renderTopbar() {
  document.getElementById('topbar').innerHTML = `
    <div class="topbar-logo">
      <img src="assets/logo-white.png" alt="Astara Intelligence" />
      <span class="topbar-product">Portfolio Intelligence</span>
    </div>
    <div class="topbar-meta">
      <span class="topbar-badge">Mirai Investments</span>
    </div>
  `;
}
```

- [ ] **Step 4.2: Función `renderKpiStrip()`**

```javascript
function renderKpiStrip() {
  const sectors = allData.sectors;
  const totalCompanies = sectors.reduce((n, s) => n + s.companies.length, 0);
  const activeCompanies = sectors.reduce((n, s) =>
    n + s.companies.filter(c => c.status === 'portfolio' || c.status === 'integrated').length, 0);
  const totalSectors = sectors.length;

  document.getElementById('kpi-strip').innerHTML = `
    <div class="kpi-eyebrow">Portfolio · Resumen global</div>
    <div class="kpi-row">
      <div class="kpi-card featured">
        <div class="kpi-label">Total empresas</div>
        <div class="kpi-value">${totalCompanies.toLocaleString('es-ES')}</div>
        <div class="kpi-note">en seguimiento activo</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-label">Adquiridas / Integradas</div>
        <div class="kpi-value">${activeCompanies}</div>
        <div class="kpi-note">portfolio + integradas</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-label">Sectores</div>
        <div class="kpi-value">${totalSectors}</div>
        <div class="kpi-note">en seguimiento</div>
      </div>
    </div>
  `;
}
```

- [ ] **Step 4.3: Verificar en el navegador**

Recargar. Debe verse:
- Topbar navy con logo Astara Intelligence blanco + badge "Mirai Investments"
- Franja KPI navy con 3 cards: 37 total · número adquiridas · 9 sectores

---

## Task 5: Renderizar tabs

**Files:**
- Modify: `index.html` — añadir funciones JS

- [ ] **Step 5.1: Función `renderTabs()` y `setActiveSector()`**

```javascript
function renderTabs() {
  const nav = document.getElementById('tablist');
  nav.innerHTML = allData.sectors.map(sector => `
    <button
      class="tab-btn"
      role="tab"
      aria-selected="false"
      aria-controls="cards-container"
      data-sector="${sector.id}"
    >
      ${sector.name}
      <span class="tab-count">${sector.companies.length}</span>
    </button>
  `).join('');

  nav.addEventListener('click', e => {
    const btn = e.target.closest('.tab-btn');
    if (!btn) return;
    setActiveSector(btn.dataset.sector);
  });

  nav.addEventListener('keydown', e => {
    const btns = [...nav.querySelectorAll('.tab-btn')];
    const idx = btns.indexOf(document.activeElement);
    if (e.key === 'ArrowRight') { btns[(idx + 1) % btns.length].focus(); e.preventDefault(); }
    if (e.key === 'ArrowLeft')  { btns[(idx - 1 + btns.length) % btns.length].focus(); e.preventDefault(); }
    if (e.key === 'Home') { btns[0].focus(); e.preventDefault(); }
    if (e.key === 'End')  { btns[btns.length - 1].focus(); e.preventDefault(); }
  });
}

function setActiveSector(sectorId) {
  activeSectorId = sectorId;
  activeFilter = 'all';
  searchQuery = '';

  document.querySelectorAll('.tab-btn').forEach(btn => {
    const isActive = btn.dataset.sector === sectorId;
    btn.setAttribute('aria-selected', isActive);
    btn.tabIndex = isActive ? 0 : -1;
  });

  renderFilterBar();
  renderCards();
}
```

- [ ] **Step 5.2: Verificar en el navegador**

Recargar. Los 9 tabs deben aparecer en la barra pegajosa bajo el KPI strip. Al hacer clic en cada tab el activo cambia visualmente (fondo blanco + sombra). Teclado: flechas izquierda/derecha navegan entre tabs.

---

## Task 6: Renderizar filtros y cards

**Files:**
- Modify: `index.html` — añadir funciones JS

- [ ] **Step 6.1: Función `renderFilterBar()`**

```javascript
function renderFilterBar() {
  const wrap = document.getElementById('filter-bar-wrap');
  wrap.innerHTML = `
    <div class="filter-bar">
      <span class="filter-icon" aria-hidden="true">
        <svg width="16" height="16" viewBox="0 0 16 16" fill="none"
             stroke="var(--as-accent)" stroke-width="1.6"
             stroke-linecap="round" stroke-linejoin="round">
          <circle cx="6.5" cy="6.5" r="4.5"/>
          <line x1="10.5" y1="10.5" x2="14" y2="14"/>
        </svg>
      </span>
      <input
        class="filter-search"
        type="search"
        placeholder="Buscar empresa…"
        aria-label="Buscar empresa"
        value="${searchQuery}"
      />
      <div class="filter-sep" aria-hidden="true"></div>
      <button class="filter-chip" aria-pressed="${activeFilter === 'all'}"         data-filter="all">Todas</button>
      <button class="filter-chip" aria-pressed="${activeFilter === 'portfolio'}"   data-filter="portfolio">En cartera</button>
      <button class="filter-chip" aria-pressed="${activeFilter === 'integrated'}"  data-filter="integrated">Integrada</button>
      <button class="filter-chip" aria-pressed="${activeFilter === 'coparticipada'}" data-filter="coparticipada">Coparticipada</button>
    </div>
  `;

  wrap.querySelector('.filter-search').addEventListener('input', e => {
    searchQuery = e.target.value.toLowerCase();
    renderCards();
  });

  wrap.querySelectorAll('.filter-chip').forEach(btn => {
    btn.addEventListener('click', () => {
      activeFilter = btn.dataset.filter;
      renderFilterBar();
      renderCards();
    });
  });
}
```

- [ ] **Step 6.2: Función de utilidades de avatar y badge**

```javascript
function getInitials(name) {
  return name.replace(/[^a-zA-ZÀ-ÿ\s]/g, '').trim()
    .split(/\s+/).slice(0, 2)
    .map(w => w[0].toUpperCase()).join('');
}

const STATUS_LABELS = {
  portfolio:     'En cartera',
  integrated:    'Integrada',
  coparticipada: 'Coparticipada'
};

function statusBadge(status) {
  return `<span class="status-badge status-${status}">${STATUS_LABELS[status] ?? status}</span>`;
}

const ICON_EXTERNAL = `<svg width="11" height="11" viewBox="0 0 11 11" fill="none"
  stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
  <path d="M2 9L9 2M5 2h4v4"/>
</svg>`;

const ICON_CLOSE = `<svg width="12" height="12" viewBox="0 0 12 12" fill="none"
  stroke="var(--as-fg-on-dark)" stroke-width="2" stroke-linecap="round">
  <line x1="1" y1="1" x2="11" y2="11"/><line x1="11" y1="1" x2="1" y2="11"/>
</svg>`;
```

- [ ] **Step 6.3: Función `renderCards()`**

```javascript
function renderCards() {
  const sector = allData.sectors.find(s => s.id === activeSectorId);
  if (!sector) return;

  let companies = [...sector.companies].sort((a, b) => b.platform - a.platform);

  if (activeFilter !== 'all') {
    companies = companies.filter(c => c.status === activeFilter);
  }
  if (searchQuery) {
    companies = companies.filter(c => c.name.toLowerCase().includes(searchQuery));
  }

  const container = document.getElementById('cards-container');

  if (companies.length === 0) {
    container.innerHTML = `
      <div class="empty-state" role="status">
        <svg width="32" height="32" viewBox="0 0 32 32" fill="none"
             stroke="var(--as-fg-3)" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="14" cy="14" r="9"/><line x1="22" y1="22" x2="29" y2="29"/>
        </svg>
        <p>Sin resultados para los filtros actuales.</p>
      </div>`;
    return;
  }

  const sectorHeader = `
    <div class="sector-header">
      <div>
        <div class="sector-eyebrow">Sector activo</div>
        <div class="sector-title">${sector.name}</div>
      </div>
      <span class="sector-count">${companies.length} ${companies.length === 1 ? 'empresa' : 'empresas'}</span>
    </div>`;

  const cards = companies.map(c => `
    <article
      class="company-card${c.platform ? ' platform' : ''}"
      role="button"
      tabindex="0"
      data-company="${encodeURIComponent(JSON.stringify(c))}"
      data-sector-name="${sector.name}"
      aria-label="Ver detalle de ${c.name}"
    >
      <div class="card-avatar" aria-hidden="true">${getInitials(c.name)}</div>
      <div class="card-body">
        <div class="card-name">${c.name}</div>
        <div class="card-def">${c.definition}</div>
        <div class="card-tags">${c.products.slice(0, 3).map(p => `<span class="card-tag">${p}</span>`).join('')}</div>
      </div>
      <div class="card-right">
        ${statusBadge(c.status)}
        <a class="card-link" href="${c.url}" target="_blank" rel="noopener noreferrer"
           onclick="event.stopPropagation()">
          mirai.investments ${ICON_EXTERNAL}
        </a>
      </div>
    </article>
  `).join('');

  container.innerHTML = sectorHeader + cards;

  container.querySelectorAll('.company-card').forEach(card => {
    card.addEventListener('click', () => openModal(card));
    card.addEventListener('keydown', e => {
      if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); openModal(card); }
    });
  });
}
```

- [ ] **Step 6.4: Verificar en el navegador**

Recargar. Al hacer clic en cada tab se muestran las empresas del sector:
- La empresa madre (platform: true) aparece primera con borde azul izquierdo
- Cada card muestra avatar de iniciales, nombre, definición, hasta 3 tags y badge de estado
- El buscador filtra en tiempo real al escribir
- Los chips de filtro funcionan (Todas / En cartera / Integrada / Coparticipada)
- Con filtros que no dan resultado se muestra el empty state

---

## Task 7: Modal de detalle

**Files:**
- Modify: `index.html` — añadir funciones JS

- [ ] **Step 7.1: Funciones `openModal()` y `closeModal()`**

```javascript
function openModal(cardEl) {
  const company = JSON.parse(decodeURIComponent(cardEl.dataset.company));
  const sectorName = cardEl.dataset.sectorName;
  const backdrop = document.getElementById('modal-backdrop');

  backdrop.innerHTML = `
    <div class="modal" role="document">
      <div class="modal-header">
        <button class="modal-close" id="modal-close-btn" aria-label="Cerrar">${ICON_CLOSE}</button>
        <div class="modal-avatar" aria-hidden="true">${getInitials(company.name)}</div>
        <div id="modal-company-name" class="modal-name">${company.name}</div>
        <div class="modal-sector">${sectorName} · ${STATUS_LABELS[company.status] ?? company.status}</div>
      </div>
      <div class="modal-body">
        <div class="modal-status-row">
          <div>
            <div class="modal-status-label">Estado</div>
            ${statusBadge(company.status)}
          </div>
          <a class="modal-link" href="${company.url}" target="_blank" rel="noopener noreferrer">
            Ver en mirai.investments ${ICON_EXTERNAL}
          </a>
        </div>
        <hr class="modal-divider">
        <div class="modal-field">
          <div class="field-label">Definición</div>
          <div class="field-value">${company.definition}</div>
        </div>
        <div class="modal-field">
          <div class="field-label">Productos y servicios</div>
          <div class="field-tags">${company.products.map(p => `<span class="field-tag">${p}</span>`).join('')}</div>
        </div>
      </div>
    </div>
  `;

  backdrop.removeAttribute('hidden');
  document.body.style.overflow = 'hidden';

  const closeBtn = document.getElementById('modal-close-btn');
  closeBtn.focus();
  closeBtn.addEventListener('click', closeModal);
  backdrop.addEventListener('click', e => { if (e.target === backdrop) closeModal(); });

  // Focus trap
  const focusable = backdrop.querySelectorAll('button, a, [tabindex="0"]');
  const first = focusable[0], last = focusable[focusable.length - 1];
  backdrop.addEventListener('keydown', trapFocus);
  function trapFocus(e) {
    if (e.key === 'Tab') {
      if (e.shiftKey && document.activeElement === first) { last.focus(); e.preventDefault(); }
      else if (!e.shiftKey && document.activeElement === last) { first.focus(); e.preventDefault(); }
    }
    if (e.key === 'Escape') closeModal();
  }
  backdrop._trapFocus = trapFocus;
}

function closeModal() {
  const backdrop = document.getElementById('modal-backdrop');
  backdrop.removeEventListener('keydown', backdrop._trapFocus);
  backdrop.setAttribute('hidden', '');
  document.body.style.overflow = '';
}
```

- [ ] **Step 7.2: Verificar el modal en el navegador**

Recargar. Al hacer clic en cualquier card:
- Se abre el modal con header navy, avatar de iniciales, nombre y sector
- Se muestran el estado (badge), enlace a mirai.investments, definición completa y todos los tags de productos
- Clicar fuera del modal (en el backdrop) lo cierra
- Tecla Escape lo cierra
- El scroll del body queda bloqueado mientras el modal está abierto
- Foco queda atrapado dentro del modal (Tab/Shift+Tab ciclan solo por los elementos focusables del modal)

---

## Task 8: Pulido final y verificación completa

**Files:**
- Modify: `index.html` — ajustes menores de CSS responsive

- [ ] **Step 8.1: Añadir responsive para tablet**

Añadir al bloque `<style>`:

```css
@media (max-width: 1024px) {
  #topbar, #tabs-wrapper { padding: 0 20px; }
  #main-content { padding: 20px 20px 48px; }
  #kpi-strip { padding: 20px 20px 24px; }
}
@media (max-width: 768px) {
  .kpi-row { flex-wrap: wrap; }
  .kpi-card { flex: 1 1 calc(50% - 6px); }
  .company-card { flex-wrap: wrap; }
  .card-right { flex-direction: row; align-items: center; width: 100%; justify-content: space-between; }
  .filter-bar { flex-wrap: wrap; gap: 8px; border-radius: var(--as-radius-lg); }
  .filter-search { min-width: 120px; }
}
```

- [ ] **Step 8.2: Verificación final — recorrido completo**

Abrir `index.html` en el navegador y comprobar:

1. **Topbar:** logo Astara Intelligence blanco visible, badge "Mirai Investments"
2. **KPI strip:** 3 valores correctos (37 total, adquiridas/integradas, 9 sectores)
3. **Tabs:** los 9 sectores aparecen con contador; el primero (Metal & equipment) está activo
4. **Cards:** las 13 empresas de Metal aparecen; Innometal Group con borde navy a la izquierda
5. **Navegación tabs:** clicar "Electrónica" muestra 8 empresas; "Moda" muestra 1 (Batela)
6. **Búsqueda:** escribir "MAM" filtra a 1 resultado; borrar restaura todo
7. **Filtros:** chip "Integrada" muestra solo las integradas del sector activo; "Todas" restaura
8. **Modal:** clicar cualquier card abre el modal; Escape lo cierra; clic fuera lo cierra
9. **Enlace externo:** el enlace "mirai.investments" en la card NO abre el modal (stopPropagation)
10. **Responsive:** redimensionar a 768px — las cards y el KPI strip se adaptan

---

## Self-Review — Cobertura del spec

| Requisito del spec | Tarea |
|---|---|
| Topbar sticky navy + logo Astara Intelligence | Task 4 |
| KPI strip con 3 métricas | Task 4 |
| 9 tabs por sector con contadores | Task 5 |
| Cards ricas (avatar, def, tags, badge, link) | Task 6 |
| Filtro por estado (4 chips) | Task 6 |
| Búsqueda por nombre en tiempo real | Task 6 |
| Plataformas madre con borde navy y orden prioritario | Task 6 |
| Modal con información completa | Task 7 |
| Enlace a mirai.investments desde card y modal | Tasks 6 y 7 |
| Design system Astara (tokens, Montserrat, SVG icons) | Tasks 2, 3 |
| Responsive desktop y tablet | Task 8 |
| data.json separado con las 37 empresas | Task 1 |
| Sin desinversiones en ningún componente | Task 1 (JSON excluye Greenfarm, Dos Grados, Sidenhol) |
| Iconografía SVG monocroma en --as-accent | Tasks 3, 6, 7 |
