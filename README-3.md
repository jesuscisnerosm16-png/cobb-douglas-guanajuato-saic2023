# Cobb-Douglas en la manufactura de Guanajuato · SAIC 2023

Paquete reproducible del proyecto parcial de **Econometría I**: *Relación entre capital, trabajo y valor agregado en la industria manufacturera de Guanajuato*.

Estima una función de producción Cobb-Douglas log-log por MCO con efectos fijos de entidad y subsector, errores estándar robustos HC3 e interacciones que permiten pendientes propias para Guanajuato. La unidad de análisis es la celda **entidad × subsector SCIAN** del SAIC (Censos Económicos 2024, año de referencia 2023): **621 observaciones, 32 entidades, 21 subsectores; 21 celdas son de Guanajuato**.

> **Fuente: INEGI, SAIC, Censos Económicos 2024** (año de referencia 2023). Análisis y transformaciones de elaboración propia; no son del INEGI ni cuentan con su aval.

> **Versión de referencia:** el informe final es [`informe/Informe_Cobb_Douglas_Guanajuato_final.html`](informe/Informe_Cobb_Douglas_Guanajuato_final.html) (12-nov-2026). Todo el paquete se construyó para reproducir **ese** documento. La versión anterior (10-nov-2026, informe de auditoría en Quarto) está archivada en [`historico/`](historico/).

## Resultados principales (los que reproduce el paquete)

| Resultado | Valor |
|---|---|
| R² modelo base / con interacciones | 0.961533 / 0.961655 |
| Elasticidad capital · resto / Guanajuato | 0.4198 / 0.6121 |
| Elasticidad trabajo · resto / Guanajuato | 0.7099 / 0.5189 |
| Rendimientos a escala · resto / Guanajuato | 1.1297 / 1.1310 |
| H₀: RTS = 1 (p, HC3) · resto / Guanajuato | 2.65 × 10⁻⁸ / 0.0609 |
| H₀: pendientes de Guanajuato iguales (F, p) | 1.9810, 0.1389 |
| Breusch-Pagan/Koenker (p) · RESET HC3 (p) | 1.29 × 10⁻⁵ · 4.83 × 10⁻⁴ |
| Leave-one-out · RTS Guanajuato (rango) / p (rango) | 1.1008–1.1735 / 0.0011–0.2105 |

Son asociaciones condicionales entre agregados, **no efectos causales**. RESET rechaza la forma funcional, por lo que el modelo es una referencia y no una especificación validada (ver el informe, §6.4 y §7).

## Inicio rápido

```bash
git clone <URL-del-repositorio> && cd cobb-douglas-guanajuato-saic2023
python -m venv .venv && source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements-lock.txt
python scripts/python/ejecutar_todo.py                    # ~10 s
```

La última línea debe ser `CADENA PYTHON COMPLETA Y VERIFICADA.` (123 comprobaciones superadas). La estimación original en R está en la sección siguiente; instrucciones detalladas en [`docs/REPRODUCIBILIDAD.md`](docs/REPRODUCIBILIDAD.md).

## Dos rutas de reproducción

| Ruta | Qué hace | Para qué sirve | Estado |
|---|---|---|---|
| **R** (`EJECUTAR_PROYECTO_COBB_DOUGLAS.R`) | Audita la extracción, reconstruye la muestra y estima los modelos originales | Es la **fuente de los resultados del informe** (modelo, HC3, pruebas, influencia, robustez) | Ejecutada por el autor el 10-nov-2026 (R 4.6.1, Windows 11); sus salidas están en `resultados/COBB_DOUGLAS_20261110_204101/`. Esta preparación del paquete **no pudo volver a correrla** (sin R disponible) |
| **Python** (`scripts/python/`) | Réplica independiente con statsmodels + los tres ejercicios complementarios (VIF parcial, Translog, leave-one-out) + figuras | Verificar los resultados de R **y** reproducir lo que el informe declara calculado en Python | Ejecutada y verificada al preparar el paquete (Python 3.13.18) |

El informe distingue estas dos fuentes (§5.3 y §6.4); el paquete mantiene esa separación: nada calculado en Python se presenta como salida de R.

### Ruta R

```r
# 1) Abrir COBB_DOUGLAS_SAIC_2023_GUANAJUATO.Rproj en RStudio (fija la raíz del proyecto)
# 2) Ejecutar una sola vez:
source("EJECUTAR_PROYECTO_COBB_DOUGLAS.R")
```

o desde terminal, en la raíz: `Rscript EJECUTAR_PROYECTO_COBB_DOUGLAS.R`. Instala `sandwich`, `lmtest`, `ggplot2` y `knitr` si faltan (requiere Internet). Crea `resultados/COBB_DOUGLAS_<fecha_hora>/`; después `python tests/comparar_ejecucion_R.py` compara esa carpeta con la de referencia.

> Los scripts de R son **byte a byte los del paquete original**; no se editaron. Al correr el paso 00, R reescribe `data/processed/BASE_ANALITICA_COBB_DOUGLAS_621.csv` y los CSV de `data/audit/` (con los mismos datos; solo cambia la fecha en `REPORTE_AUDITORIA_REPRODUCIBLE.txt`).

## Estructura

```
.
├── README.md · LICENSE · CITATION.cff · Makefile · requirements*.txt
├── COBB_DOUGLAS_SAIC_2023_GUANAJUATO.Rproj      # ancla del proyecto R
├── EJECUTAR_PROYECTO_COBB_DOUGLAS.R             # lanzador R (etapas 00 y 01)
├── data/
│   ├── raw/        # extracción SAIC original (665 filas), NO se modifica
│   ├── processed/  # muestra log preparada (621) y base analítica
│   └── audit/      # conciliación 672→665→621, exclusiones, diccionario, procedencia
├── scripts/
│   ├── 00_verificar_y_preparar_datos.R · 01_estimacion_cobb_douglas.R   # originales
│   └── python/     # cdg_lib.py · 10 datos · 11 modelos · 12 complementarios · 13 figuras · ejecutar_todo.py
├── resultados/
│   ├── COBB_DOUGLAS_20261110_204101/   # salida de R usada por el informe (referencia, no tocar)
│   ├── complementarios_python/         # CSV de VIF parcial, Translog y LOO citados en el informe
│   └── python_recalculado/             # salida de scripts/python (se regenera; incluye figuras/)
├── informe/        # HTML final + sus 10 figuras extraídas
├── tests/          # verificar_reproduccion.py · comparar_ejecucion_R.py
├── docs/           # REPRODUCIBILIDAD · DATOS · METODOLOGIA · DECISIONES_METODOLOGICAS · CORRESPONDENCIA_INFORME · NOTAS_DE_VERSION
├── historico/      # versión anterior (10-nov): auditoría Quarto y documentos reemplazados
└── MANIFEST_SHA256.csv    # SHA-256 de cada archivo (regenerar: python scripts/python/generar_manifiesto.py)
```

## Qué comprueba `tests/verificar_reproduccion.py`

1. **Python ↔ R**: R², AIC/BIC, elasticidades, EE/IC/p HC3, contrastes de Wald, BP/Koenker, RESET (convencional y HC3), VIF completo, conteos de influencia y las cuatro especificaciones de robustez coinciden con la ejecución de R (47 comprobaciones; tolerancia relativa ≤ 10⁻⁵; la diferencia máxima observada fue ~10⁻¹³).
2. **Complementarios**: VIF parcial, Translog y leave-one-out recalculados coinciden con los CSV de referencia del informe (18 comprobaciones).
3. **Informe ↔ cálculo**: 58 comprobaciones sobre cifras clave impresas en el HTML (R², AIC, elasticidades, EE, contrastes, BP, RESET, Translog, VIF, rango LOO, umbrales y conteos de influencia, descriptivos y robustez): cada una aparece tal cual en el documento y coincide con lo recalculado. No cubre cada celda de cada cuadro (p. ej. los casos individuales del Cuadro A12).

## Datos y licencias

* **Datos:** INEGI, SAIC, Censos Económicos 2024 (año de referencia 2023). Ver [`docs/DATOS.md`](docs/DATOS.md) para procedencia, diccionario y tratamiento de faltantes. Se redistribuyen conforme a los [Términos de libre uso del INEGI](https://www.inegi.org.mx/inegi/terminos.html): citar la fuente, no alterar metadatos e indicar que el análisis no es del INEGI (ver [`data/AVISO_FUENTE_INEGI.md`](data/AVISO_FUENTE_INEGI.md)).
* **Código:** MIT (ver `LICENSE`), © 2026 José de Jesús Cisneros Muñoz.
* **Informe:** el texto del informe pertenece a sus autores; no lo cubre la licencia del código.

## Limitaciones que conviene tener presentes

* Datos agregados por entidad-subsector, no empresas; capital en pesos corrientes (valor de reposición), no físico.
* Guanajuato aporta 21 celdas; la decisión sobre RTS = 1 depende de qué celdas se excluyan (leave-one-out).
* Los cálculos complementarios (VIF parcial, Translog, LOO) existen aquí solo en Python; el informe indica que falta portarlos a R. **No se incluye un port a R sin probar.**
* Las pruebas de Quarto/R de la versión histórica y el flujo de CI de R no se ejecutaron al preparar el paquete.

Hay **errores menores detectados en el HTML** (Figura A7 con etiquetas desacomodadas, referencias de figura desfasadas en §6.1–6.2 y numeración A8→A10). Detalle y corrección sugerida en [`docs/NOTAS_DE_VERSION.md`](docs/NOTAS_DE_VERSION.md).

## Cómo citar

Ver `CITATION.cff`.


## Publicación web y Quarto

La portada de GitHub Pages es [`index.html`](index.html). Es una copia **byte a byte** del informe final ya renderizado en `informe/Informe_Cobb_Douglas_Guanajuato_final.html`; por eso, la página principal conserva exactamente el HTML entregado, sin volver a generarlo ni cambiar su CSS, tablas, figuras o contenido. El mismo documento también está disponible con su nombre completo en la raíz del sitio.

La configuración de Quarto se conserva en [`_quarto.yml`](_quarto.yml) (ese es el nombre de archivo que reconoce Quarto; no `Quarto.yaml`). La entrada de Quarto es [`index.qmd`](index.qmd), que incorpora el documento maestro y los fragmentos de `_contenido/`. Quarto se renderiza en GitHub Actions para validar la estructura y las figuras, pero el resultado publicado como portada se copia del HTML aprobado; no se sustituye por el HTML reconstruido por Quarto.

- `assets/css/referencia-html.css` conserva los estilos internos del HTML de referencia.
- `assets/css/quarto-book-compat.css` adapta únicamente el contenedor exterior de Quarto.
- `docs/index.html` y `docs/Informe_Cobb_Douglas_Guanajuato_final_sin_nota_GitHub.html` se conservan como copias exactas del HTML patrón.
- `tests/verificar_quarto_book.py` comprueba que `index.html`, `docs/index.html` y el HTML de referencia sean idénticos, además de validar la estructura de la fuente modular.
- `tests/verificar_render_quarto.py` valida el HTML generado por Quarto y la correspondencia de las diez imágenes embebidas.
- `.github/workflows/publicar-quarto-book.yml` publica el HTML estático exacto en GitHub Pages y comprueba que la portada coincida con el archivo de referencia. El workflow `verificar.yml` ejecuta aparte la cadena de reproducibilidad, R, Python y Quarto. En GitHub, configura **Settings → Pages → Build and deployment → Source: GitHub Actions**.

La publicación requiere que el repositorio use la rama `main` o que se ejecute manualmente el workflow. La primera ejecución remota debe terminar correctamente para que GitHub Pages muestre la dirección del sitio.
