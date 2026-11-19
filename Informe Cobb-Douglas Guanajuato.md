# Relación entre capital, trabajo y valor agregado en la industria manufacturera de Guanajuato

Proyecto parcial de Econometría I\
12 de noviembre de 2026

## Resumen

En este trabajo se estima una función de producción Cobb-Douglas con información del Sistema Automatizado de Información Censal (SAIC) para 2023. El objetivo es analizar la relación entre el acervo de activos fijos, las horas trabajadas y el valor agregado censal bruto de la industria manufacturera, con atención a Guanajuato. La unidad de análisis es el cruce entre entidad federativa y subsector SCIAN. Después de depurar los registros se utilizaron 621 observaciones: 32 entidades y 21 subsectores, de los cuales 21 corresponden a Guanajuato. Se estimaron modelos log-log por mínimos cuadrados ordinarios, con efectos fijos de entidad y subsector y errores estándar robustos HC3. El modelo con interacciones obtuvo un R² de 0.9617. Para Guanajuato, las elasticidades estimadas fueron 0.6121 para capital y 0.5189 para trabajo; sin embargo, no se encontró evidencia estadística suficiente de que sus pendientes sean distintas de las del resto de las entidades. La prueba RESET también indicó problemas de especificación. Por ello, los resultados sirven como una primera aproximación a la relación entre los insumos y el valor agregado, pero no permiten afirmar causalidad ni considerar validada definitivamente la forma funcional.

**Palabras clave:** función Cobb-Douglas; industria manufacturera; capital; trabajo; Guanajuato.

## 1. Introducción

Una forma de estudiar la actividad manufacturera es analizar cómo se relacionan los recursos utilizados en la producción con el valor que generan. Entre esos recursos se encuentran el capital y el trabajo. La función de producción Cobb-Douglas permite representar esa relación y estimar la elasticidad del producto respecto a cada insumo.

En este proyecto se utiliza información del SAIC de 2023 para estudiar las manufacturas de las entidades federativas y revisar con mayor detalle el caso de Guanajuato. La pregunta principal es si la relación estimada entre activos fijos, horas trabajadas y valor agregado es diferente para Guanajuato frente al conjunto de las demás entidades. Para responderla se comparan dos especificaciones: una con efectos fijos de entidad y subsector, y otra que incorpora interacciones para permitir pendientes particulares para Guanajuato.

La información disponible está agregada por entidad y subsector, por lo que no representa empresas o establecimientos individuales. Esta característica es importante al interpretar los resultados: las estimaciones describen relaciones entre agregados y no necesariamente el comportamiento de una empresa manufacturera.

## 2. Objetivos del proyecto

### Objetivo general

Estimar la relación entre el capital, el trabajo y el valor agregado censal bruto de la industria manufacturera, utilizando una función Cobb-Douglas y prestando atención a las observaciones correspondientes a Guanajuato.

### Objetivos particulares

- Estimar las elasticidades del valor agregado respecto al capital y al trabajo.
- Comparar las elasticidades estimadas para Guanajuato con las del resto de las entidades federativas.
- Evaluar el ajuste del modelo y revisar si existen problemas de heterocedasticidad o de especificación funcional.
- Comprobar si los resultados principales cambian al utilizar medidas alternativas de capital y trabajo.

## 3. Alcance del proyecto

El análisis se limita a los datos agregados del SAIC correspondientes a 2023. Incluye las 32 entidades federativas y los 21 subsectores manufactureros considerados en la extracción, siempre que las variables necesarias para la estimación estén disponibles y sean positivas. El trabajo compara el comportamiento de Guanajuato con el de las otras 31 entidades.

No se estudian empresas individuales, diferencias entre años ni cambios en la productividad a lo largo del tiempo. Tampoco se estima un efecto causal del capital o del trabajo. Para ello se necesitaría una estrategia de identificación y datos que permitan atender problemas como la simultaneidad y las variables omitidas. Además, el acervo de activos fijos está expresado en valor monetario y no constituye una medida física homogénea de maquinaria; por esa razón, las elasticidades deben interpretarse con esta limitación.

## 4. Marco teórico

Una función de producción representa la relación entre los insumos utilizados y el producto obtenido. En la forma Cobb-Douglas, el producto depende del capital y del trabajo mediante una expresión multiplicativa (Cobb y Douglas, 1928):

Yi=AiKiαLiβ Y_i = A_i\\,K_i^{\\alpha}\\,L_i^{\\beta}

En esta expresión, Y representa el producto, K el capital, L el trabajo y A recoge otros factores relacionados con la productividad. Los parámetros α y β son las elasticidades del producto respecto al capital y al trabajo. Al expresar la función en logaritmos se obtiene una relación lineal:

ln(Yi)=ln(Ai)+αln(Ki)+βln(Li)+ui \\ln(Y_i) = \\ln(A_i) + \\alpha\\,\\ln(K_i) + \\beta\\,\\ln(L_i) + u_i

Así, por ejemplo, una elasticidad de 0.40 indica que un aumento de 1% en el insumo correspondiente se relaciona con un aumento aproximado de 0.40% en el producto, manteniendo constantes los demás elementos del modelo. La suma α + β permite clasificar los rendimientos a escala: si es igual a uno son constantes; si es mayor que uno son crecientes; y si es menor que uno son decrecientes.

Para distinguir a Guanajuato del resto de las entidades se incorporan interacciones entre una variable indicadora y los logaritmos de capital y trabajo. La especificación estimada es:

ln(Yi)=β0+βKln(Ki)+βLln(Li)+δK(Giln(Ki))+δL(Giln(Li))+μe+λs+ui \\begin{gathered}\\ln(Y_i) = \\beta_0 + \\beta_K\\ln(K_i) + \\beta_L\\ln(L_i)\\\\ + \\delta_K\\,(G_i\\ln(K_i)) + \\delta_L\\,(G_i\\ln(L_i))\\\\ + \\mu_e + \\lambda_s + u_i\\end{gathered}

G toma el valor de uno para Guanajuato y cero para las demás entidades; μe representa los efectos fijos de entidad y λs los de subsector. Para el resto de las entidades, las elasticidades son βK y βL. Para Guanajuato se calculan como βK + δK y βL + δL. La suma de ambas elasticidades es el rendimiento a escala de cada grupo.

## 5. Metodología

### 5.1. Datos y variables

Los datos provienen del SAIC de los Censos Económicos 2024, con año de referencia 2023. Se tomó como unidad de observación cada combinación de entidad federativa y subsector manufacturero SCIAN. Las variables utilizadas en el modelo principal se describen en la tabla 1. Las definiciones y unidades se revisaron con la documentación metodológica del INEGI (2024).

**Tabla 1. Variables utilizadas en el modelo principal**

| Variable | Código SAIC | Descripción | Unidad |
| --- | --- | --- | --- |
| Y | A131A | Valor agregado censal bruto | Millones de pesos |
| K | Q000A | Acervo total de activos fijos | Millones de pesos |
| L | H001D | Horas trabajadas por el personal ocupado total | Miles de horas |

Fuente: elaboración propia con información del SAIC (INEGI, 2024).

A131A representa el valor agregado censal bruto; Q000A corresponde al acervo actualizado de activos fijos, valuado a valor actual o costo de reposición; y H001D registra las horas trabajadas durante el año. Por tanto, el capital es un acervo y las horas son un flujo anual. Las variables monetarias están expresadas en pesos corrientes del año censal. Como el análisis utiliza un solo año, no se realiza una comparación temporal ni se aplica un deflactor que no esté desagregado para las diferencias entre sectores y entidades.

### 5.2. Depuración de la muestra

La extracción contemplaba 672 combinaciones posibles (32 entidades por 21 subsectores). Se obtuvieron 665 registros; siete combinaciones no aparecieron en la extracción. De los registros obtenidos, 39 no tenían información en las variables económicas centrales y cinco presentaban un valor agregado negativo. Como la estimación se realiza en logaritmos, se conservaron únicamente las observaciones con valores positivos de Y, K y L. La muestra final quedó integrada por 621 observaciones: 600 del resto de las entidades y 21 de Guanajuato. No se imputaron las celdas vacías como si fueran ceros. Las siete combinaciones que no aparecieron corresponden al universo teórico y no se restaron nuevamente de los 665 registros extraídos.

### 5.3. Estimación

Se estimaron dos modelos por mínimos cuadrados ordinarios (MCO). El primero incluye los logaritmos del capital y del trabajo, junto con efectos fijos de entidad y subsector. El segundo añade las interacciones con la indicadora de Guanajuato para estimar pendientes específicas para ese estado. En ambos casos se utiliza la misma muestra de 621 observaciones.

La inferencia se reporta con errores estándar robustos HC3. Esta matriz modifica los errores estándar y los intervalos de confianza, pero no los coeficientes estimados. Su uso es pertinente ante la presencia de heterocedasticidad; no corrige por sí sola la endogeneidad ni los problemas de especificación (White, 1980; MacKinnon y White, 1985). También se aplicaron las pruebas Breusch-Pagan/Koenker y RESET. Como revisiones adicionales se compararon medidas alternativas de los insumos y se estimó una especificación Translog exploratoria.

La estimación principal y las pruebas de robustez con medidas alternativas se obtuvieron en R. Los cálculos complementarios de VIF parcial, Translog y sensibilidad leave-one-out se realizaron en Python/statsmodels; por ello, estos últimos se reportan como ejercicios adicionales y no como parte de la ejecución original de R.

## 6. Resultados

### 6.1. Estadística descriptiva

Las medias de las tres variables son mayores que sus medianas, tanto en la muestra completa como en Guanajuato. Esto sugiere que hay diferencias importantes en el tamaño de las celdas sectoriales y que algunas observaciones tienen valores relativamente altos. En Guanajuato, las medias de valor agregado, activos fijos y horas trabajadas son mayores que las del resto de las entidades, aunque el grupo estatal contiene solo 21 observaciones.

**Tabla 2. Media y mediana de las variables principales**

| Variable | Muestra completa (n=621) | Guanajuato (n=21) |  |  |
| --- | --- | --- | --- | --- |
|  | Media | Mediana | Media | Mediana |
| VAB (millones de pesos) | 8,654.2 | 1,263.7 | 25,790.1 | 7,373.7 |
| Activos fijos (millones de pesos) | 6,128.5 | 971.2 | 20,161.6 | 6,717.3 |
| Horas trabajadas (miles) | 25,967.6 | 8,401.6 | 58,800.3 | 20,735.1 |

Fuente: cálculos propios con la muestra depurada del SAIC 2023.

La Figura 2 complementa los estadísticos descriptivos al mostrar la distribución de ln(VAB) en Guanajuato y en el resto de las entidades. La comparación es descriptiva y debe leerse considerando que los grupos tienen tamaños distintos: 21 observaciones para Guanajuato y 600 para el resto del país.

Diagrama de cajas de la distribución de ln(VAB), comparando Guanajuato (21 observaciones) y el resto de las entidades (600 observaciones).

*Figura 1. Distribución del logaritmo del valor agregado por grupo territorial.*

Fuente: muestra depurada del SAIC 2023. Nota: el diagrama presenta ln(VAB); los puntos fuera de los bigotes son observaciones que el gráfico representa separadamente y no implican que hayan sido eliminadas de la estimación.

### 6.2. Comparación de las especificaciones

El modelo con interacciones tiene un R² ligeramente mayor que el modelo base: pasa de 0.961533 a 0.961655. La diferencia es muy pequeña. Además, el R² ajustado, el AIC y el BIC favorecen al modelo sin interacciones. El RMSE del modelo con interacciones es un poco menor, pero la prueba conjunta de las dos interacciones no rechaza que sean iguales a cero (p = 0.138882). Por estos resultados, el modelo base es una referencia más sencilla, mientras que el modelo con interacciones permite revisar específicamente las elasticidades de Guanajuato.

**Tabla 3. Comparación de los modelos estimados**

| Indicador | Modelo base | Con interacciones de Guanajuato |
| --- | --- | --- |
| Observaciones | 621 | 621 |
| Parámetros de regresión | 54 | 56 |
| R² | 0.961533 | 0.961655 |
| R² ajustado | 0.957937 | 0.957923 |
| AIC | 958.193 | 960.212 |
| BIC | 1,201.917 | 1,212.798 |
| RMSE en logaritmos | 0.479020 | 0.478256 |

Fuente: resultados de la estimación en R. Un menor AIC o BIC indica un mejor equilibrio entre ajuste y número de parámetros.

La Figura 3 compara ln(VAB) observado con ln(VAB) ajustado por el modelo Cobb-Douglas con efectos fijos de entidad y subsector e interacciones de Guanajuato. La línea de 45° representa coincidencia exacta entre ambos valores; la cercanía de los puntos a esa línea resume visualmente el ajuste dentro de la muestra.

Gráfica de dispersión de ln(VAB) observado frente a ln(VAB) ajustado, con 600 observaciones del resto de entidades y 21 de Guanajuato y una línea de igualdad de 45 grados.

*Figura 2. Valores observados frente a valores ajustados del modelo con interacciones, en escala logarítmica.*

Fuente: cálculo propio con el archivo de predicciones del modelo con interacciones, estimado sobre las 621 observaciones. Nota: son valores ajustados dentro de la misma muestra utilizada para estimar el modelo; no constituyen una evaluación fuera de muestra ni pronósticos. Los valores y la línea se presentan en escala logarítmica.

### 6.3. Elasticidades y rendimientos a escala

La especificación con interacciones permite obtener elasticidades diferenciadas para Guanajuato y para el resto de las entidades. En el resto del país, las elasticidades estimadas son 0.4198 para capital y 0.7099 para trabajo; para Guanajuato, las elasticidades combinadas son 0.6121 y 0.5189, respectivamente. En términos económicos, manteniendo constante el otro factor y los efectos incluidos en el modelo, un aumento de 1% en los activos fijos se asocia con un aumento aproximado de 0.61% en el valor agregado de Guanajuato; un aumento de 1% en las horas trabajadas se asocia con un aumento aproximado de 0.52%. Estas son asociaciones condicionales estimadas con datos agregados por entidad y subsector: no representan efectos causales ni elasticidades tecnológicas de establecimientos individuales.

**Tabla 4. Elasticidades estimadas e inferencia del modelo con interacciones**

| Parámetro | Estimación | EE HC3 | p-valor | IC 95% HC3 | N | Sig. |
| --- | --- | --- | --- | --- | --- | --- |
| Panel A. Elasticidades de los factores (H₀: elasticidad = 0) |  |  |  |  |  |  |
| Capital: resto de entidades | 0.4198 | 0.0535 | 2.195 × 10−14 | \[0.3147, 0.5249\] | 621 | \*\*\* |
| Trabajo: resto de entidades | 0.7099 | 0.0608 | 2.100 × 10−28 | \[0.5905, 0.8292\] | 621 | \*\*\* |
| Capital: Guanajuato | 0.6121 | 0.0969 | 5.412 × 10−10 | \[0.4218, 0.8024\] | 621 | \*\*\* |
| Trabajo: Guanajuato | 0.5189 | 0.1193 | 1.617 × 10−5 | \[0.2846, 0.7532\] | 621 | \*\*\* |
| Panel B. Rendimientos a escala (H₀: suma de elasticidades = 1) |  |  |  |  |  |  |
| Rendimientos a escala: resto | 1.1297 | 0.0230 | 2.652 × 10−8 | \[1.0845, 1.1748\] | 621 | \*\*\* |
| Rendimientos a escala: Guanajuato | 1.1310 | 0.0697 | 0.06088 | \[0.9940, 1.2679\] | 621 | * |

Fuente: estimación propia con errores estándar HC3. N = 621 en cada renglón. En el panel A, los valores p contrastan H₀: elasticidad = 0; en el panel B, contrastan H₀: rendimientos a escala = 1. Significancia: \*\*\* p \< 0.01; \*\* p \< 0.05; * p \< 0.10. Las elasticidades por grupo son combinaciones lineales de los coeficientes del modelo con interacciones, no la reproducción de todos los coeficientes de efectos fijos.

Elasticidades estimadas de capital y trabajo para el resto de las entidades y Guanajuato, con intervalos de confianza HC3 al 95 por ciento.

*Figura 3. Elasticidades estimadas e intervalos de confianza al 95% con errores estándar HC3.*

La suma de elasticidades —una medida de los rendimientos a escala dentro de la función Cobb-Douglas— es 1.1297 para el resto de las entidades y 1.1310 para Guanajuato. Para el resto de las entidades se rechaza la hipótesis de rendimientos constantes (p = 2.65 × 10−8), de modo que la estimación es compatible con rendimientos crecientes. Para Guanajuato, la prueba no rechaza rendimientos constantes al nivel de 5% (p = 0.0609). Esto no demuestra que los rendimientos sean exactamente constantes: significa que la muestra no aporta evidencia suficiente para rechazar la hipótesis en ese nivel de significancia. Además, la prueba conjunta no encuentra diferencias estadísticamente significativas entre las elasticidades de capital y trabajo de Guanajuato y las del resto de las entidades (F = 1.9810; p = 0.1389); tampoco se encuentra diferencia en la suma de elasticidades (p = 0.9857). Por último, este análisis no estima productividad total de los factores ni productividad marginal en unidades físicas; por ello, no corresponde interpretar las elasticidades como una medición directa de productividad.

### 6.4. Diagnósticos y revisiones adicionales

#### Heterocedasticidad e inferencia

La prueba Breusch-Pagan/Koenker obtuvo un estadístico de 110.6651 y un valor p de 0.0000129; por tanto, se rechaza la hipótesis de homocedasticidad. En consecuencia, la inferencia principal se reporta con errores estándar robustos HC3. Esta corrección ajusta la estimación de la incertidumbre ante heterocedasticidad, pero no corrige por sí sola la endogeneidad, una posible dependencia entre observaciones de una misma entidad o subsector, ni los problemas de especificación funcional.

**Tabla 5. Pruebas principales del modelo**

| Prueba | Estadístico | Valor p | Resultado al 5% |
| --- | --- | --- | --- |
| Breusch-Pagan/Koenker | 110.6651 | 0.0000129 | Se rechaza homocedasticidad |
| RESET convencional | F = 6.2515 | 0.002064 | Se rechaza la especificación |
| RESET robusto HC3 | F = 7.7397 | 0.000483 | Se rechaza la especificación |
| Diferencia conjunta de pendientes de Guanajuato | F = 1.9810 | 0.138882 | No se rechaza igualdad |
| Rendimientos constantes: Guanajuato | F = 3.5274 | 0.060876 | No se rechaza RTS = 1 |

Fuente: resultados de la estimación y pruebas del proyecto. La prueba RESET se utiliza para detectar posibles errores de especificación funcional (Ramsey, 1969).

#### Especificación funcional y extensión Translog

Las pruebas RESET convencional y robusta HC3 rechazan la especificación al 5%. Esto indica que la forma funcional estimada puede estar omitiendo curvatura u otros términos relevantes, pero RESET no identifica por sí sola cuál sería la especificación correcta. Como comprobación exploratoria se estimó una función Translog con tres términos adicionales de curvatura: el contraste conjunto de esos términos obtuvo p = 0.0002357 y el R² aumentó a 0.964657, frente a 0.961655 del modelo Cobb-Douglas con interacciones. La mejora del R² no basta para preferir la Translog. Este cálculo se realizó en Python/statsmodels y no en la ejecución original de R; antes de considerarlo un resultado definitivo debe reproducirse bajo el mismo flujo de trabajo y someterse a diagnósticos comparables (Christensen, Jorgenson y Lau, 1973).

#### Colinealidad y efectos fijos

Los VIF calculados sobre el diseño completo son elevados para las interacciones de Guanajuato. Sin embargo, al descontar primero los efectos fijos mediante el procedimiento Frisch-Waugh-Lovell, los VIF parciales de las cuatro variables de pendiente se ubican entre 3.22 y 3.47. La diferencia importa: los VIF completos reflejan también la estructura de los efectos fijos, mientras que los parciales examinan la colinealidad de los regresores de interés una vez descontados esos efectos. No deben interpretarse como indicadores equivalentes ni como evidencia aislada de que el modelo sea adecuado (O’Brien, 2007).

#### Residuos, influencia y sensibilidad

Las Figuras A2 y A3 presentan, respectivamente, los residuos frente a los valores ajustados y el gráfico Q–Q de los residuos studentizados. Son diagnósticos visuales complementarios para examinar patrones en los errores y desviaciones respecto de la normalidad; no sustituyen las pruebas formales ni resuelven los problemas de especificación detectados por RESET. Los cuadros A10–A12 y las Figuras A5–A6 documentan la identificación de observaciones influyentes y la sensibilidad leave-one-out de Guanajuato.

En el ejercicio leave-one-out se retiró, una por una, cada una de las 21 observaciones de Guanajuato. La suma estimada de elasticidades permaneció por encima de uno, entre 1.1008 y 1.1735; sin embargo, el valor p de la prueba de rendimientos constantes varió entre 0.00114 y 0.21046. Por tanto, la decisión estadística sobre rendimientos constantes depende de cuáles celdas se excluyan. Esto aconseja conservar la muestra completa en la estimación principal y presentar el leave-one-out como una evaluación de sensibilidad, no como una razón para seleccionar observaciones.

#### Robustez de medición

Se estimaron especificaciones alternativas sustituyendo las horas trabajadas por el personal ocupado (H001A), el acervo total de activos por maquinaria y equipo de producción (Q010A), y ambas medidas simultáneamente. El R² se mantuvo elevado y las pruebas conjuntas de diferencias de pendientes de Guanajuato no rechazaron la igualdad al 5%. Estas variables no son equivalentes a las principales: H001A mide personas y no horas trabajadas, mientras que Q010A representa un componente del acervo de activos. En consecuencia, estos ejercicios evalúan la sensibilidad a la medición de los insumos; no constituyen reemplazos directamente comparables de las variables principales.

**Tabla 6. Resultados con medidas alternativas de capital y trabajo**

| Especificación | R² | RTS resto | RTS Guanajuato | Valor p de diferencias de pendientes |
| --- | --- | --- | --- | --- |
| Principal: Q000A + H001D | 0.9617 | 1.1297 | 1.1310 | 0.1389 |
| Trabajo alternativo: H001A | 0.9592 | 1.1319 | 1.1312 | 0.1764 |
| Capital alternativo: Q010A | 0.9640 | 1.0961 | 1.0906 | 0.3791 |
| Ambos alternativos | 0.9622 | 1.0986 | 1.0890 | 0.4058 |

Fuente: estimaciones de robustez realizadas en R con la misma muestra de 621 observaciones.

En conjunto, la Figura 3 resume las elasticidades con sus intervalos de confianza; la Figura A1 compara el ajuste de las especificaciones; las Figuras A2–A3 presentan los diagnósticos gráficos de residuos; la Figura A4 compara los VIF completos y parciales; las Figuras A5–A6 muestran la sensibilidad leave-one-out, y la Figura A7 compara el ajuste bajo medidas alternativas de los insumos. Cada figura responde a una pregunta distinta y complementa las tablas sin repetir sus cifras.

### 6.5. Resultados complementarios

El anexo reúne la evidencia técnica que respalda los resultados principales: conciliación de la muestra, definiciones de variables, estimaciones y contrastes, diagnósticos, observaciones influyentes, sensibilidad leave-one-out y ejercicios de robustez. Su función es permitir la verificación de los resultados sin sobrecargar la exposición central ni repetir interpretaciones ya presentadas.

*Relación entre capital, trabajo y valor agregado en la industria manufacturera de Guanajuato*\
Resultados complementarios · SAIC 2023 · Proyecto parcial de Econometría I

Este anexo conserva los cuadros y las gráficas que formaban parte del HTML de trabajo. En el artículo principal se presentan tablas más breves para respetar la extensión de cinco a siete páginas establecida en la rúbrica. Aquí se dejan disponibles los resultados completos de la muestra, los diagnósticos y las comprobaciones adicionales. Algunas tablas amplían los datos resumidos en el artículo; no representan estimaciones nuevas.

#### A. Datos y muestra

**Cuadro A1. Conciliación de la muestra**

| Control | Registros |
| --- | --- |
| Combinaciones teóricas (32 entidades × 21 subsectores) | 672 |
| Combinaciones no devueltas en la extracción | 7 |
| Registros efectivamente extraídos | 665 |
| Registros con las ocho variables económicas centrales vacías | 39 |
| Registros con faltantes parciales entre esas variables | 0 |
| Registros con VAB negativo | 5 |
| Muestra con A131A, Q000A y H001D estrictamente positivos | **621** |
| Observaciones de Guanajuato | **21** |

Las siete combinaciones no devueltas corresponden al universo teórico de 672 cruces y no se restan nuevamente de los 665 registros extraídos.

**Cuadro A2. Variables y unidades utilizadas en la estimación**

| Símbolo | Código SAIC | Variable | Unidad declarada | Papel |
| --- | --- | --- | --- | --- |
| Y | A131A | Valor agregado censal bruto | Millones de pesos | Dependiente |
| K | Q000A | Acervo total de activos fijos | Millones de pesos | Capital |
| L | H001D | Horas trabajadas por personal ocupado total | Miles de horas | Trabajo |
| K alternativo | Q010A | Acervo de maquinaria y equipo de producción | Millones de pesos | Robustez |
| L alternativo | H001A | Personal ocupado total | Personas | Robustez |

Q010A y H001A se utilizan únicamente en las pruebas de robustez de medición.

**Cuadro A3. Estadística descriptiva por grupo**

| Variable | Grupo | Media | Mediana | P10 | P90 |
| --- | --- | --- | --- | --- | --- |
| VAB (millones de pesos) | Total (n=621) | 8,654.2 | 1,263.7 | 37.2 | 21,408.8 |
| Activos fijos (millones de pesos) | Total (n=621) | 6,128.5 | 971.2 | 35.1 | 14,206.3 |
| Horas (miles) | Total (n=621) | 25,967.6 | 8,401.6 | 519.0 | 63,327.3 |
| VAB (millones de pesos) | Resto (n=600) | 8,054.4 | 1,179.2 | 34.2 | 20,277.6 |
| Activos fijos (millones de pesos) | Resto (n=600) | 5,637.3 | 910.6 | 33.1 | 13,437.1 |
| Horas (miles) | Resto (n=600) | 24,818.5 | 7,373.1 | 502.5 | 61,492.3 |
| VAB (millones de pesos) | Guanajuato (n=21) | 25,790.1 | 7,373.7 | 1,220.4 | 36,072.7 |
| Activos fijos (millones de pesos) | Guanajuato (n=21) | 20,161.6 | 6,717.3 | 1,529.6 | 31,533.5 |
| Horas (miles) | Guanajuato (n=21) | 58,800.3 | 20,735.1 | 7,505.7 | 199,288.4 |

Las medias y medianas se reportan en las unidades originales. La diferencia entre ambas refleja asimetría en las distribuciones.

#### B. Estimación principal y pruebas

**Cuadro A4. Comparación del modelo base y el modelo con interacciones**

| Modelo | N | Parámetros de regresión | R² | R² ajustado | AIC | BIC | RMSE log |
| --- | --- | --- | --- | --- | --- | --- | --- |
| FE entidad + subsector | 621 | 54 | 0.961533 | **0.957937** | **958.193** | **1201.917** | 0.479020 |
| FE + interacciones Guanajuato | 621 | 56 | **0.961655** | 0.957923 | 960.212 | 1212.798 | **0.478256** |

**Cuadro A5. Elasticidades, errores estándar e intervalos de confianza HC3**

| Parámetro | Estimación | EE HC3 | IC 95% HC3 | p-valor (dos colas) |
| --- | --- | --- | --- | --- |
| Capital: resto de entidades | 0.4198 | 0.0535 | \[0.3147, 0.5249\] | 2.195e-14 |
| Trabajo: resto de entidades | 0.7099 | 0.0608 | \[0.5905, 0.8292\] | 2.1e-28 |
| Capital: Guanajuato | 0.6121 | 0.0969 | \[0.4218, 0.8024\] | 5.412e-10 |
| Trabajo: Guanajuato | 0.5189 | 0.1193 | \[0.2846, 0.7532\] | 1.617e-05 |
| RTS: resto de entidades (H0=1) | 1.1297 | 0.0230 | \[1.0845, 1.1748\] | 2.652e-08 |
| RTS: Guanajuato (H0=1) | 1.1310 | 0.0697 | \[0.9940, 1.2679\] | 0.06088 |

Los errores estándar e intervalos HC3 se reportan para las combinaciones lineales de cada grupo.

**Cuadro A6. Contrastes de hipótesis principales**

| Contraste | F HC3 | gl1 | gl2 | p-valor | Decisión (α = 0.05) |
| --- | --- | --- | --- | --- | --- |
| Rendimientos constantes: resto de entidades | 31.8391 | 1 | 565 | 2.6517e-08 | Rechazar H₀ |
| Rendimientos constantes: Guanajuato | 3.5274 | 1 | 565 | 0.0608756 | No rechazar H₀ |
| Diferencia conjunta de elasticidades de Guanajuato | 1.9810 | 2 | 565 | 0.138882 | No rechazar H₀ |
| Diferencia en rendimientos a escala Guanajuato - resto | 0.0003 | 1 | 565 | 0.985727 | No rechazar H₀ |

La prueba conjunta es la referencia para evaluar si las dos pendientes de Guanajuato difieren simultáneamente de las del resto de las entidades.

Comparación del R² de ambas especificaciones.

*Figura A1. Comparación del R² entre las especificaciones base y con interacciones.*

#### C. Diagnósticos econométricos

**Cuadro A7. Pruebas de especificación funcional (RESET)**

| Prueba | Estadístico | gl | p-valor | Decisión al 5% |
| --- | --- | --- | --- | --- |
| RESET convencional (fitted², fitted³) | F = 6.2515 | (2, 563) | 0.0020641 | Rechazar H₀ |
| RESET robusto HC3 | F = 7.7397 | (2, 563) | 0.0004832 | Rechazar H₀ |

El rechazo indica posibles términos omitidos o una forma funcional insuficiente; no determina por sí solo qué modelo alternativo debe elegirse.

Residuos frente a valores ajustados, salida original del script R.

*Figura A2. Residuos frente a valores ajustados.*

Gráfico Q–Q de residuos studentizados, salida original del script R.

*Figura A3. Gráfico Q–Q de los residuos studentizados.*

**Cuadro A8. VIF completo y VIF parcial después de descontar los efectos fijos**

| Regresor | VIF completo (incluye FE) | VIF parcial (después de FE) |
| --- | --- | --- |
| ln_K_model | 10.29 | 3.22 |
| ln_L_model | 10.07 | 3.23 |
| Gto_ln_K | 130.53 | 3.46 |
| Gto_ln_L | 259.10 | 3.47 |

Los indicadores responden preguntas distintas. El VIF parcial se calcula sobre los regresores de pendiente una vez retirada la proyección explicada por los efectos fijos.

Comparación de VIF completo y parcial.

*Figura A4. Comparación de los VIF completos y parciales.*

**Cuadro A10. Observaciones señaladas por criterios de influencia**

| Criterio | Umbral aplicado | Observaciones marcadas |
| --- | --- | --- |
| Distancia de Cook | 0.007080 | 27 |
| Leverage | 0.180354 | 8 |
| Residuo studentizado absoluto | 3 | 12 |
| DFFITS absoluto | 0.600590 | 33 |
| Máximo absoluto de DFBETAS | 0.080257 | 344 |
| Unión de criterios | — | 345 |

Las observaciones marcadas no se eliminaron automáticamente. Los diagnósticos sirven para revisar sensibilidad, no para depurar la muestra por sí solos.

#### D. Sensibilidad de los resultados para Guanajuato

**Cuadro A11. Rangos del análisis leave-one-out**

| Magnitud | Mínimo LOO | Máximo LOO |
| --- | --- | --- |
| Elasticidad del capital de Guanajuato | 0.5634 | 0.6402 |
| Elasticidad del trabajo de Guanajuato | 0.4617 | 0.5760 |
| RTS de Guanajuato | 1.1008 | 1.1735 |
| p-valor para H₀: RTS = 1 | 0.00114 | 0.21046 |

Se eliminó una a una cada celda sectorial de Guanajuato y se volvió a estimar el modelo con interacciones.

RTS en cada reestimación dejando fuera una celda de Guanajuato.

*Figura A5. Rendimientos a escala en cada reestimación leave-one-out.*

p-valores de la prueba RTS=1 en las 21 reestimaciones.

*Figura A6. Valores p de la prueba de rendimientos constantes en las 21 reestimaciones.*

**Cuadro A12. Casos seleccionados del análisis leave-one-out**

| Celda omitida (SCIAN) | Subsector | RTS Gto. | p (RTS=1) |
| --- | --- | --- | --- |
| 326 | Industria del plástico y del hule | 1.1735 | 0.0011 |
| 314 | Fabricación de productos textiles, excepto prendas de vestir | 1.1549 | 0.0189 |
| 324 | Fabricación de productos derivados del petróleo y del carbón | 1.1393 | 0.0470 |
| 336 | Fabricación de equipo de transporte | 1.1079 | 0.2105 |
| 311 | Industria alimentaria | 1.1146 | 0.1676 |
| 334 | Fabricación de equipo de computación, comunicación, medición y de otros equipos, componentes y accesorios electrónicos | 1.1008 | 0.1630 |

Se muestran tres casos de menor valor p y tres de mayor valor p. La muestra principal conserva las 21 observaciones de Guanajuato.

#### E. Extensión Translog y robustez de medición

La especificación Translog se calculó como comprobación complementaria en Python/statsmodels. Sus resultados son exploratorios y requieren reproducirse y someterse a los mismos diagnósticos antes de preferirla al modelo Cobb-Douglas.

**Cuadro A13. Coeficientes de los términos adicionales de la extensión Translog**

| Término cuadrático Translog | Coeficiente | EE HC3 | p individual HC3 |
| --- | --- | --- | --- |
| (ln K centrado)^2 | 0.01882 | 0.02554 | 0.4616 |
| (ln L centrado)^2 | -0.06298 | 0.04056 | 0.1211 |
| ln K centrado × ln L centrado | 0.01531 | 0.06061 | 0.8007 |

Los valores p individuales no sustituyen el contraste conjunto de los tres términos de curvatura.

**Cuadro A14. Comparación del ajuste entre Cobb-Douglas y la extensión Translog**

| Modelo | Rango de X | R² | R² ajustado | RMSE log | AIC\* | BIC\* |
| --- | --- | --- | --- | --- | --- | --- |
| Cobb–Douglas con interacciones | 56 | 0.961655 | 0.957923 | 0.478256 | 960.212 | 1212.798 |
| Translog complementario | 59 | 0.964657 | 0.961009 | 0.459157 | 915.595 | 1181.475 |

La mejora de los criterios dentro de muestra es una señal para continuar la revisión, no una validación definitiva de la forma Translog.

**Cuadro A15. Resultados completos de robustez de medición de capital y trabajo**

| Especificación | Capital | Trabajo | R² | RTS resto | p (RTS=1, resto) | RTS Guanajuato | p (RTS=1, Gto.) | p (δK=δL=0) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Principal: Q000A + H001D | Q000A | H001D | 0.9617 | 1.1297 | 2.652e-08 | 1.1310 | 0.0609 | 0.1389 |
| Trabajo alternativo: H001A | Q000A | H001A | 0.9592 | 1.1319 | 9.028e-08 | 1.1312 | 0.0677 | 0.1764 |
| Capital alternativo: Q010A | Q010A | H001D | 0.9640 | 1.0961 | 9.285e-06 | 1.0906 | 0.2469 | 0.3791 |
| Ambos alternativos | Q010A | H001A | 0.9622 | 1.0986 | 1.374e-05 | 1.0890 | 0.2716 | 0.4058 |

Las variables alternativas no son idénticas a las principales: H001A mide personas y Q010A un componente de los activos fijos, no el acervo total.

Comparación del R² en las cuatro especificaciones de insumos.

*Figura A7. Comparación del R² con distintas medidas de capital y trabajo.*

## 7. Conclusiones

Con los datos del SAIC para 2023 se encontró una relación positiva entre el valor agregado manufacturero, el acervo de activos fijos y las horas trabajadas. La función Cobb-Douglas presenta un R² elevado, aunque este resultado por sí solo no garantiza que la especificación sea adecuada. Al comparar el modelo base con el que incorpora interacciones para Guanajuato, la mejora del ajuste es mínima y los criterios AIC y BIC favorecen al modelo más sencillo.

Las elasticidades estimadas para Guanajuato fueron 0.6121 para capital y 0.5189 para trabajo. Son asociaciones condicionales y no efectos causales. El contraste conjunto no permitió afirmar que las pendientes de Guanajuato sean diferentes de las del resto de las entidades. En rendimientos a escala, se rechazó la hipótesis de rendimientos constantes para el resto de las entidades, pero no para Guanajuato al nivel de 5%; esto último no demuestra que los rendimientos sean exactamente constantes. Además, la revisión leave-one-out mostró que la decisión estadística para Guanajuato es sensible a algunas observaciones del estado.

Las pruebas señalaron heterocedasticidad y posibles problemas de forma funcional. Los errores estándar HC3 atienden la primera cuestión en la inferencia, pero no corrigen por sí solos la posible dependencia entre observaciones ni la endogeneidad. RESET rechazó la especificación Cobb-Douglas restringida. La extensión Translog ofrece una vía para examinar la curvatura, aunque todavía debe reproducirse y someterse a diagnósticos comparables antes de considerarla preferible. Por ello, el modelo debe interpretarse como una aproximación condicionada por los datos y la especificación utilizada, no como una representación definitiva de la producción manufacturera.

Por último, los resultados no deben interpretarse como efectos causales ni como elasticidades tecnológicas de empresas individuales. La base reúne agregados por entidad y subsector, y el capital está medido en términos monetarios. Para profundizar el análisis sería conveniente trabajar con información de panel o microdatos y con medidas de capital que permitan distinguir mejor las cantidades físicas y los cambios de precios.

## 8. Referencias

Christensen, L. R., Jorgenson, D. W., y Lau, L. J. (1973). Transcendental logarithmic production frontiers. *The Review of Economics and Statistics, 55*(1), 28-45. [https://doi.org/10.2307/1927992](https://doi.org/10.2307/1927992)

Cobb, C. W., y Douglas, P. H. (1928). A theory of production. *The American Economic Review, 18*(1), 139-165.

Instituto Nacional de Estadística y Geografía (INEGI). (2024). *Sistema Automatizado de Información Censal (SAIC): documento metodológico de los Censos Económicos 2024*. [https://www.inegi.org.mx/contenidos/app/saic/saic_historico_metodologico_ce2024.pdf](https://www.inegi.org.mx/contenidos/app/saic/saic_historico_metodologico_ce2024.pdf)

Instituto Nacional de Estadística y Geografía (INEGI). (s. f.). *Sistema Automatizado de Información Censal (SAIC)*. [https://www.inegi.org.mx/app/saic/default.html](https://www.inegi.org.mx/app/saic/default.html)

MacKinnon, J. G., y White, H. (1985). Some heteroskedasticity-consistent covariance matrix estimators with improved finite sample properties. *Journal of Econometrics, 29*(3), 305-325. [https://doi.org/10.1016/0304-4076(85)90158-7](https://doi.org/10.1016/0304-4076%2885%2990158-7)

O'Brien, R. M. (2007). A caution regarding rules of thumb for variance inflation factors. *Quality & Quantity, 41*, 673-690. [https://doi.org/10.1007/s11135-006-9018-6](https://doi.org/10.1007/s11135-006-9018-6)

Ramsey, J. B. (1969). Tests for specification errors in classical linear least-squares regression analysis. *Journal of the Royal Statistical Society: Series B, 31*(2), 350-371. [https://doi.org/10.1111/j.2517-6161.1969.tb00796.x](https://doi.org/10.1111/j.2517-6161.1969.tb00796.x)

White, H. (1980). A heteroskedasticity-consistent covariance matrix estimator and a direct test for heteroskedasticity. *Econometrica, 48*(4), 817-838. [https://doi.org/10.2307/1912934](https://doi.org/10.2307/1912934)