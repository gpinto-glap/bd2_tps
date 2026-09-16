# Informe de Mediciones

## Consulta 1: Facturación por categoría y mes

### Estado ANTES de optimizar (Sin índices)
- **Tiempo de ejecución:** 1.413 ms
- **Plan de ejecución:** Realiza Seq Scan en `detalle_pedido`, `producto`, `categoria` y `pedido`.

```text

"Sort  (cost=160.38..162.68 rows=920 width=266) (actual time=0.767..0.772 rows=4.00 loops=1)"
"  Sort Key: (date_trunc('month'::text, pe.fecha_hora)), (sum(dp.subtotal)) DESC"
"  Sort Method: quicksort  Memory: 25kB"
"  Buffers: shared hit=10"
"  ->  HashAggregate  (cost=101.30..115.10 rows=920 width=266) (actual time=0.218..0.228 rows=4.00 loops=1)"
"        Group Key: date_trunc('month'::text, pe.fecha_hora), c.nombre"
"        Batches: 1  Memory Usage: 49kB"
"        Buffers: shared hit=4"
"        ->  Hash Join  (cost=65.55..94.40 rows=920 width=250) (actual time=0.184..0.198 rows=6.00 loops=1)"
"              Hash Cond: (dp.pedido_id = pe.id)"
"              Buffers: shared hit=4"
"              ->  Hash Join  (cost=31.48..55.59 rows=920 width=250) (actual time=0.098..0.105 rows=6.00 loops=1)"
"                    Hash Cond: (p.categoria_id = c.id)"
"                    Buffers: shared hit=3"
"                    ->  Hash Join  (cost=14.50..36.17 rows=920 width=32) (actual time=0.052..0.057 rows=6.00 loops=1)"
"                          Hash Cond: (dp.producto_id = p.id)"
"                          Buffers: shared hit=2"
"                          ->  Seq Scan on detalle_pedido dp  (cost=0.00..19.20 rows=920 width=32) (actual time=0.014..0.015 rows=6.00 loops=1)"
"                                Buffers: shared hit=1"
"                          ->  Hash  (cost=12.00..12.00 rows=200 width=16) (actual time=0.024..0.025 rows=10.00 loops=1)"
"                                Buckets: 1024  Batches: 1  Memory Usage: 9kB"
"                                Buffers: shared hit=1"
"                                ->  Seq Scan on producto p  (cost=0.00..12.00 rows=200 width=16) (actual time=0.014..0.016 rows=10.00 loops=1)"
"                                      Buffers: shared hit=1"
"                    ->  Hash  (cost=13.10..13.10 rows=310 width=226) (actual time=0.032..0.032 rows=4.00 loops=1)"
"                          Buckets: 1024  Batches: 1  Memory Usage: 9kB"
"                          Buffers: shared hit=1"
"                          ->  Seq Scan on categoria c  (cost=0.00..13.10 rows=310 width=226) (actual time=0.014..0.015 rows=4.00 loops=1)"
"                                Buffers: shared hit=1"
"              ->  Hash  (cost=20.70..20.70 rows=1070 width=16) (actual time=0.053..0.055 rows=4.00 loops=1)"
"                    Buckets: 2048  Batches: 1  Memory Usage: 17kB"
"                    Buffers: shared hit=1"
"                    ->  Seq Scan on pedido pe  (cost=0.00..20.70 rows=1070 width=16) (actual time=0.044..0.046 rows=4.00 loops=1)"
"                          Buffers: shared hit=1"
"Planning:"
"  Buffers: shared hit=56"
"Planning Time: 0.988 ms"
"Execution Time: 1.413 ms"


