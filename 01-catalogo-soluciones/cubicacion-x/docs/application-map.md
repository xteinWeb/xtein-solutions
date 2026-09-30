# Mapa canónico de Cubicar

## Stack y entry points

- Angular 20 para autenticación, shell, navegación y todos los módulos; `src/main.ts` → `AppModule` → `CubicarModule`.
- No hay runtime React/Vite ni carga dinámica de HTML/JavaScript legacy.
- Supabase JS con clave publicable en `src/config/supabase.js`; Google Apps Script (GAS) para PDF/reportes; Netlify como hosting actual.
- No hay Angular ni TypeScript. No hay backend propio: navegador y GAS acceden directamente a Supabase.

## Runtime, navegación y estado

`AppComponent` expone Aserrío, Consumos, Registro, Proveedores, Administración y Reportes mediante rutas Angular. El estado se encapsula en servicios Angular; `localStorage` conserva el operador. No es autenticación Supabase: operador/PIN se consulta desde `operadores`.

## Módulos reales

| Módulo | Vista / script | Tablas/vistas | RPC | GAS y reglas principales |
|---|---|---|---|---|
| Login / Shell | `AppComponent` Angular | `operadores`, maestros | `get_next_id` | PIN local y timeout |
| Registro | `RegistroComponent` | `registros`, `registros_detalle`, maestros | `get_next_id` | Bloque/dimensionada, máximo dos espesores, cierre y PDF |
| Aserrío | `AserrioComponent` | `aserrio`, tres tablas detalle, valorización | `get_next_id`, `valorizar_idaserrio` | Bloque, dimensionada, ajustes, cierre y PDF |
| Consumos | `ConsumosComponent` | `consumos`, relaciones, detalles, registros y productos | `get_next_id`, `get_estibas_consumo_disponibles` | Orden-productos y consumo de tablas |
| Proveedores | `ProveedoresComponent` | `proveedores` | — | CRUD directo |
| Reportes | `ReportesComponent` | `registros`, `aserrio` y detalles | — | GAS genera PDF, consolidado, precios y CSV |
| Administración | `AdminComponent` | Aserrío, valorización y costo mensual | RPC de valorización/costo | Correcciones y recálculo |

## GAS y reportes

`GAS/code.gs` enruta acciones. `informe.gs`, `InformeAserrio.gs`, `informeconsolidado.gs`, `informeprecios.gs` y `preciosbloque.gs` consultan REST/RPC de Supabase y generan archivos. `GAS/Index.html` es la UI administrativa de precios/gastos. La decisión de conservar o reemplazar GAS queda pendiente del backend corporativo.

## Dependencias externas

Supabase (PostgreSQL/Data API), Google Apps Script/Drive, Netlify, React/Lucide. La vista pública `productos` depende indirectamente del esquema compartido `pdesarrollo`.
