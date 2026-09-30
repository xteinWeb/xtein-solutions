# Pendientes de integración corporativa

Solo decisiones que requieren a Sistemas:

1. Repositorio/ubicación del host Angular y convenciones de módulos, rutas, guards y diseño.
2. Proyecto Node real, montaje de rutas, middleware de identidad/logging y firma de `getConnection`.
3. Valor real de `prmConexion` y gestión de configuración por ambiente.
4. Instancia y versión SQL Server DEV para ejecutar DDL/SP y paridad de integración.
5. Forma exacta consumida de `DATOS` (texto JSON o JSON ya deserializado) y tratamiento host de `ErrMensaje`.
6. Autorización de mantenimiento de proveedores y si un ID inexistente debe seguir siendo no-op o convertirse en error funcional.
7. Longitudes, collation, zona horaria y precisión corporativas.
8. Implementación del `ProductoGateway` contra el maestro corporativo.

No bloquean el patrón local, pero impiden declarar E2E corporativo.
