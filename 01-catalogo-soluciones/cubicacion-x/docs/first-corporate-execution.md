# Primera ejecución corporativa

## Resultado

Se implementó el patrón candidato completo para Maestros y Proveedores sin modificar legacy ni Supabase. Estado: `PARCIAL - PENDIENTE INTEGRACION CORPORATIVA`.

## Entregables

- Feature `CubicarModule` compatible con Angular 15.2, routing hijo, modelos, tokens, services y dos componentes.
- Contrato desacoplado `ProductoGateway` sin referencia a `pdesarrollo`.
- Cinco endpoints Node, cada uno con acción fija y ejecución del SP del módulo.
- `spCubicarMaestros` y `spCubicarProveedores`, con listas cerradas, JSON, `DATOS`, `ErrMensaje` y transacción donde corresponde.
- Fixtures de once escenarios y matrices de reglas/paridad.
- Harness de compilación/pruebas Angular y servidor Node, ambos `DEV ONLY`.

## Validación realizada

- Angular `ngc` 15.2: correcto.
- Contratos Angular: 4/4 pruebas.
- Transporte Node: 4/4 pruebas.
- Fixtures/estructura SP: 3/3 pruebas.
- Legacy Vite: build correcto, 1.675 módulos.
- Supabase: lectura de metadata, constraints y agregados; cero escrituras.
- SQL Server real: no disponible; sintaxis y contratos revisados estáticamente, no ejecutados.

Las instalaciones reportaron vulnerabilidades conocidas de dependencias (Angular harness: 1 baja/7 altas; Node harness: 2 moderadas/2 altas; legacy: 4 altas). No se aplicó `audit fix --force` porque rompería versiones fijadas, especialmente Angular 15.2.

## Legacy modificado

Ningún archivo funcional legacy fue modificado. La implementación vive bajo `corporate/`.
