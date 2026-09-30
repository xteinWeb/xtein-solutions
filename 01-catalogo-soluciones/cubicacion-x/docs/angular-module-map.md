# Mapa Angular 15.2

| Pieza | Responsabilidad | Contrato |
|---|---|---|
| `CubicarModule` | Feature module integrable | Exporta componentes; importa routing hijo |
| `CubicarRoutingModule` | Rutas internas | `maestros`, `proveedores` |
| `CorporateApiService` | Envelope corporativo y normalización de `DATOS` textual | `prmAccion`, `prmDatos`, `prmConexion` |
| `MaestrosService` | Acción de catálogo | `LISTAR MAESTROS` |
| `ProveedoresService` | Operaciones observadas | listar, crear, actualizar, eliminar |
| `MaestrosComponent` | Visualización de catálogos | sin acceso a datos directo |
| `ProveedoresComponent` | Formulario, filtro y acciones | preserva trim, NIT opcional, duplicado UI y confirmación |
| `CUBICAR_USER` | Identidad aportada por host | `CubicarUser` |
| `ProductoGateway` | Frontera futura de productos | listar/obtener sin Supabase |

La presentación es deliberadamente mínima. La adaptación al design system y guards del host es `PENDIENTE_DE_DEFINICION`.
