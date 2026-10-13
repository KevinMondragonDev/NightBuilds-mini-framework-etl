# 🚀 Sideproject — Mini framework de ETL

**Repositorio:** `sideproject-mini-framework-etl` · **Tipo:** framework + ETL de ejemplo · **Tiempo:** 8–10 h · **Después de:** lecciones 1 a 3 de esta sección

> Reglas, README y lista de cierre: [`SIDEPROJECTS.md`](docs/REGLAS.md). **No hay solución: el diseño es tuyo.**

## El caso

Ya escribiste varios ETL y todos repiten lo mismo: leer, validar, transformar, cargar, registrar, reintentar. Tu equipo quiere dejar de copiar y pegar: un pequeño framework donde un pipeline nuevo sea **configuración y un par de funciones**, no 200 líneas.

## Qué practicas

| Lección | Dónde aparece |
|---|---|
| Principios de diseño | Contratos (`Protocol`), inyección de dependencias, registro |
| Patrones para pipelines | Adapter (fuentes), cadena de pasos, Repository (destinos), Template Method |
| Patrones de datos | Idempotencia, incremental, cuarentena, write-audit-publish |

## Hitos

**Hito 1 — Los contratos.** Define `Fuente`, `Paso` y `Destino`. Implementa lo mínimo: fuente CSV, un paso y destino en memoria.
*Comprueba:* un pipeline de 10 líneas se ejecuta de punta a punta.

**Hito 2 — Más piezas, mismo contrato.** Fuentes: CSV, JSON, API, PostgreSQL. Destinos: Parquet, PostgreSQL. Cada una en su archivo.
*Comprueba:* añadir la fuente Parquet **no modifica ningún archivo existente**.

**Hito 3 — Piezas por nombre.** Un registro (`@fuente("csv")`) para construir un pipeline desde un YAML o un dict.
*Comprueba:* cambias de CSV a PostgreSQL editando solo la configuración.

**Hito 4 — Lo transversal, una sola vez.** Logging, medición de tiempo y reintentos como decoradores aplicados por el framework, no por cada pipeline.
*Comprueba:* un pipeline nuevo tiene logs sin haber escrito un solo `log.info`.

**Hito 5 — Seguro por defecto.** El framework aporta cuarentena con umbral y carga idempotente; el pipeline solo declara su clave.
*Comprueba:* relanzar un pipeline no duplica; una fila mala va a cuarentena con su motivo.

**Hito 6 — Úsalo.** Reescribe con tu framework el ETL de `04_retos_de_python/reto_11` y uno de tus sideprojects anteriores.
*Comprueba:* cuenta las líneas antes y después.

## Preguntas para defenderlo

- Señala en tu código cada patrón por su nombre y el problema concreto que resuelve ahí.
- ¿Qué patrón pensaste usar y descartaste? ¿Por qué?
- ¿Qué tendría que cambiar alguien para añadir un destino S3? ¿Cuántos archivos toca?
- ¿En qué se parece tu framework a Airflow o a dbt, y qué le falta?

## Súbelo de nivel

- Destino S3 probado contra **Floci**.
- Tests del framework con fuentes y destinos falsos (sin disco ni red).
