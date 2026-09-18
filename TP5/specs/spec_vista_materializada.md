# spec: vista_materializada_facturacion

Objetivo: Crear una vista materializada para el reporte analítico de facturación por categoría y mes.

1. Nombre de la vista: mv_facturacion_categoria_mes
   - Campos: anio, mes, categoria_id, categoria_nombre, total_facturado, cantidad_pedidos.
   - Opción: WITH DATA.

2. Índice Único (Requisito para REFRESH CONCURRENTLY):
   - Nombre: idx_mv_facturacion_cat_mes
   - Columnas: (anio, mes, categoria_id)