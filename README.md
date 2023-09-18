*Autor Repositorio: Iván Rojas Gallego*<br>
*correo: idaroga@gmail.com*<br>
*Fecha: Septiembre del 2023*<br>

## 1- **Comprensión del negocio**

![Accidentes](src/01_intro.png)

### **Observaciones y conclusiones:**

Se realizará el analisis sobre una base de datos tomada para los accidentes viale para la iudad de Buenos Aires desde el 2016 hasta el 2021 ya que es de suma importancia reducir las tasas de mortalidad relacionadas con sinietros viales a través de la prevención de los mismos.

Para tal fin es importante establecer ciertos objetivos y analizar sus respectivos indicadores de rendimiento (KPIs)<br>

- `OBJETIVO 1`:
    Reducir en un 10% la tasa de homicidios en siniestros viales de los últimos seis meses, en CABA, en comparación con la tasa de homicidios en siniestros viales del semestre anterior.
    - `KPI 1`: Se define la tasa de homicidios en siniestros viales como el número de víctimas fatales en accidentes de tránsito por cada 100,000 habitantes en un área geográfica durante un período de tiempo específico.
    - `FORMULA 1`: (Número de homicidios en siniestros viales / Población total) * 100,000
    - `CORECCIÓN FORMULA 1`: (porcentaje de variación): {[[(Número de homicidios en siniestros viales `del semestre anterior` / Población total `del semestre anterior`) * 100,000] - [(Número de homicidios en siniestros viales `del semestre actual` / Población total `del semestre actual`) * 100,000]] / [(Número de homicidios en siniestros viales `del semestre anterior` / Población total `del semestre anterior`) * 100,000]} * 100<br>
    <br>
- `OBJETIVO 2`:
    Reducir en un 7% la cantidad de accidentes mortales de motociclistas en el último año, en CABA, respecto al año anterior
    - `KPI 2`: Se define la cantidad de accidentes mortales de motociclistas en siniestros viales como el número absoluto de accidentes fatales en los que estuvieron involucradas víctimas que viajaban en moto en un determinado periodo temporal.
    - `FORMULA 2` (porcentaje de variación): [(Número de accidentes mortales con víctimas en moto en el año anterior - Número de accidentes mortales con víctimas en moto en el año actual) / (Número de accidentes mortales con víctimas en moto en el año anterior)] * 100.<br>
    <br>
- `OBJETIVO 3`:
    planteado por el analista
    - `KPI 3`:  planteado por el analista de acuerdo al OBJETIVO 3
    - `FORMULA 3`: planteada por el analista de acuerdo al KPI 3<br>

## 2- **Exploración inicial**

![Exploración](src/01_explorar.png)

### **Conclusiones: df_hechos**

- ``ID``: categórico (str)
- ``N_VICTIMAS``: numérico (int).
- ``FECHA``: categórico (datetime.date).
- ``AAAA``: numérico (int).
- ``MM``: numérico (int).
- ``DD``: numérico (int).
- ``HORA``: numérico (datetime.time).
- ``HH``: numérico (int).
- ``LUGAR_DEL_HECHO``: categórico (str).
- ``TIPO_DE_CALLE``: categórico (str). 
- ``Calle``: categórico (str).
- ``Altura``: numérico (float).
- ``Cruce``: categórico (str).
- ``Dirección Normalizada``: categórico (str).
- ``COMUNA``: categórico (str).
- ``XY (CABA)``: categórico (str).
- ``pos x``: numérico (float).
- ``pos y``: numérico (float).
- ``PARTICIPANTES``: categórico (str).
- ``VICTIMA``: categórico (str).
- ``ACUSADO``: categórico (str).

## 3- **Planteamiento**

![Planteamientos](src/01_planteamientos.png)

- `OBJETIVO 3`:
    Reducir en un 5% el número de accidentes mortales en el ultimo semestre en CABA, ocasionados por el mayor responsable de siniestros viales del ultimo semestre, respecto al mismo responsable en el semestre anterior.
    - `KPI 3`: Se define la cantidad de accidentes mortales ocasionado por el mayor responsable de homicidios en siniestros viales del ultimo semestre como el número absoluto de accidentes fatales causados por el mayor responsable de siniestros viales del ultimo semestre en un determinado periodo temporal. 
    - `FORMULA 3` (porcentaje de variación): {(número de accidentes mortales ocasionados por el mayor responsable de siniestros viales del ultimo semestre en el semestre anterior - número de accidentes mortales ocasionados por el mayor responsable de siniestros viales del ultimo semestre en el semestre actual) / (número de accidentes mortales ocasionados por el mayor responsable de siniestros viales del ultimo semestre en el semestre anterior)} * 100.

Según los KPI planteados se requieren los siguientes campos para realizar el análisis:

- KPI 1: tasa de homicidios en siniestros viales
    - Semestre anterior
    - Número homicidios semestre anterior
    - Poblacion total en el semestre anterior
    - Semestre actual
    - Número homicidios semestre actual
    - Poblacion total en el semestre actual<br>
    <br>
- KPI 2: Cantidad de accidentes mortales de motociclistas en siniestros viales
    - Victima = MOTO
    - Año anterior
    - Número accidentes año anterior
    - Año actual
    - Número accidentes año actual<br>
    <br>
- KPI 3: Cantidad de accidentes mortales ocasionado por el mayor responsable de homicidios en siniestros viales del ultimo semestre
    - Mayor responsable de accidentes
    - Semestre anterior
    - Número accidentes semestre anterior
    - Semestre actual
    - Número accidentes semestre actual<br>

Se debe importar un dataset que contenga la población anual por comuna extraído de la página oficial del gobierno `https://www.estadisticaciudad.gob.ar/eyc/?p=28146`<br>

Se deben crear los siguientes campos necesarios en el análisis:
- `AAAA_SEMESTRE`: categórico (str). columna calculada a partir de la columna MM y el año actual
- `POBLACION_AAAA_SEMESTRE`: numérico (int). población anual por comuna
- `AAAA_SEMESTRE_ANTERIOR`: categórico (str).
- `POBLACION_AAAA_SEMESTRE_ANTERIOR`: numérico (int).
- `AAAA_ANTERIOR`: categórico (str)<br>

Se mantienen los siguientes campos:
- `ID`: categórico (str). No se evidencian valores duplicados a través de la columna ID
- `N_VICTIMAS`: numérico (int).
- `AAAA`: numérico (int).
- `MM`: numérico (int). Elimianr despues de crear la columna SEMESTRE
- `VICTIMA`: categórico (str).
- `ACUSADO`: categórico (str).<br>

Se eliminan los siguientes campos irrelevantes para el análisis de los KPIs
- `FECHA`
- `DD`
- `HORA`
- `HH`
- `LUGAR_DEL_HECHO`
- `TIPO_DE_CALLE`
- `Calle`
- `Altura`
- `Cruce`
- `Dirección Normalizada`
- ``COMUNA``
- `XY (CABA)`
- `pos x`
- `pos y`
- `PARTICIPANTES`<br>

## 4- **Limpieza de datos**

## 5- **Enriquecimiento de columnas**

## 6- **Análisis Univariado**

### **df_hechos.N_VICTIMAS**

![N_VICTIMAS](src/grafica_n_victimas.png)

**Conclusiones**

- Solamente hay 3 posibilidades de victimas por accidente: 1, 2, 3
- La media del número de víctimas es aproximadamente 1.03, lo que sugiere que, en promedio, la mayoría de los accidentes tienen alrededor de una víctima.
- Dado que el 75% de los valores están en el primer cuartil, esto significa que el 75% de los accidentes tienen 1 víctima, y el segundo y tercer cuartiles son también 1. El valor máximo en el cuartil (75%) es 3, lo que indica que el 25% restante de los accidentes tiene 2 o 3 víctimas.
- Mayor frecuencia de numero de víctimas por accidente: 1 (97.13%)
- Menor frecuencia de numero de víctimas por accidente: 3 (0.14%)

### **df_hechos.VICTIMA**

![VICTIMA](src/grafica_victima.png)

**Conclusiones**

- Hay 10 tipos diferentes de víctimas involucradas.
- El valor más frecuente es "MOTO". Esto significa que "MOTO" es el tipo de víctima más común en los accidentes registrados.
- la frecuencia del tipo de víctima más común ("MOTO") es 295. Esto significa que hubo 295 accidentes en los que estuvieron involucradas motocicletas como víctimas.
- Victima con mayor frecuencia en accidentes: "MOTO" (42.39%)
- Victima con menor frecuencia en accidentes: "PEATON_MOTO" (0.14 %)

### **df_hechos.ACUSADO**

![ACUSADO](src/grafica_acusado.png)

**Conclusiones:**

- Hay 10 valores únicos en la columna "ACUSADO". Esto significa que existen 10 tipos diferentes de entidades o vehículos acusados en los accidentes registrados.
- El valor más frecuente en la columna "ACUSADO" es "AUTO". Esto significa que "AUTO" es el tipo de entidad o vehículo más comúnmente acusado en los accidentes registrados en el DataFrame.
- Indica que la frecuencia del tipo de entidad o vehículo más comúnmente acusado ("AUTO") es 204. Esto significa que hubo 204 accidentes en los que se acusó a un automóvil como la entidad responsable.
- Acusado con mayor frecuencia de accidentes: AUTO (29.31 %)
- Acusado con menor frecuencia de accidentes: TREN (0.14 %)

### **df_hechos.AAAA**

![AAAA](src/grafica_aaaa.png)

![AAAA](src/grafica_aaaa_2.png)

**Conclusiones**

- Hay 6 años únicos diferentes en la columna "AAAA", desde 2016 hasta 2021.
- (Cuartiles): Estos valores representan los cuartiles del conjunto de datos. Por ejemplo, el valor del primer cuartil (25%) es 2017, lo que significa que el 25% de los accidentes ocurrieron en 2017 o antes. El segundo cuartil (50%) es 2018, que es la mediana, indicando que el 50% de los accidentes ocurrieron en 2018 o antes. El tercer cuartil (75%) es 2020, lo que sugiere que el 75% de los accidentes ocurrieron en 2020 o antes.
- Año con mayor frecuencia de accidentes: 2016 (20.69%)
- Año con menor frecuencia de accidentes: 2020 (11.21%)

## 7- **Manejo de valores faltantes (nulos)**

## 8- **Análisis Multivariado**

### **KPI 1:** tasa de homicidios en siniestros viales

![KPI1](src/grafica_kpi_1.png)

**Conclusiones:**

1. Dado que no tenemos datos previos al año 2016-1 nuestra primer medida relaciona el semestre `2016-1` y `2016-2` por eso solo se evidencian valores a partir del semestre `2016-2`.<br>

2. Si el valor del semestre en la gráfica es positivo significa que para ese semestre hubo ``menos homicidios`` que el semestre pasado.<br>

3. Si la gráfica tiene pendiente positiva (creciente) significa que la ``diferencia de accidentes de motos`` vs. el semestre anterior ``aumentó de manera positiva``.<br>

4. El valor que se representa en la gráfica indica el porcentaje en que se redujo la ``tasa de homicidios en accidentes de tránsito`` del semestre anterior vs. el actual. Dado que el objetivo es que dicho valor sea ``superior al 10%`` se puede concluir que en el periodo de 6 años comprendido entre 2016 y 2021 se cumplió para los semestres:

    - 2017-1: En comparación con el semestre anterior se ``redujeron`` los homicidios y ese numero fue ``mayor`` que el logrado el semestre anterior.<br>

    - 2019-1: En comparación con el semestre anterior se ``redujeron`` los homicidios y ese numero fue ``mayor`` que el logrado el semestre anterior.<br>

    - 2019-2: En comparación con el semestre anterior se ``redujeron`` los homicidios y ese numero fue ``menor`` que el logrado el semestre anterior.<br>
    
    - 2021-2: En comparación con el semestre anterior se ``redujeron`` los homicidios y ese numero fue ``mayor`` que el logrado el semestre anterior.

5. 4 semestres de 11 cumplieron el objetivo lo cual nos indica que ``no es positivo el balance`` de acuerdo a lo planteado inicialmente

6. 5 semestres de 11 tienen un porcentaje de cambio negativo, es decir, aumenta la tasa de homicidios vs. el semestre anterior. Aunque es minoría sigue siendo alarmante la cantidad

### **KPI 2:** Cantidad de accidentes mortales de motociclistas en siniestros viales

![KPI2](src/grafica_kpi_2.png)

**Conclusiones:**

1. Dado que no tenemos datos previos al año 2016 nuestra primer medida relaciona el año `2016` y `2017` por eso solo se evidencian valores a partir del año `2017`.<br>

2. Si el valor del año en la gráfica es positivo significa que para ese año hubo ``menos homicidios`` que el año pasado.<br>

3. Si la gráfica tiene pendiente positiva (creciente) significa que la ``diferencia de accidentes de motos`` vs. el año anterior ``aumentó de manera positiva``.<br>

4. El valor que se representa en la gráfica indica el porcentaje en que se redujo la ``cantidad de homicidios en accidentes de motos`` del año anterior vs. el actual. Dado que el objetivo es que dicho valor sea ``superior al 7%`` se puede concluir que en el periodo de 6 años comprendido entre 2016 y 2021 se cumplió para los semestres:

    - 2017: En comparación con el año anterior se ``redujeron`` los homicidios y dado que no tenemos valores para el año anterior no podemos decir si fue mayor o menor respecto de ese año.<br>

    - 2019: En comparación con el año anterior se ``redujeron`` los homicidios y ese numero fue ``mayor`` que el logrado el año anterior.<br>

    - 2020: En comparación con el año anterior se ``redujeron`` los homicidios y ese numero fue ``mayor`` que el logrado el año anterior.<br>

5. 3 años de 5 cumplieron el objetivo lo cual nos indica que ``es positivo el balance`` de acuerdo a lo planteado inicialmente

6. 2 años de 5 tienen un porcentaje de cambio negativo, es decir, aumenta la tasa de accidentes en moto vs. el año anterior. Aunque es minoría sigue siendo alarmante la cantidad

### **KPI 3:** Cantidad de accidentes mortales ocasionado por el mayor responsable de homicidios en siniestros viales del ultimo semestre

![KPI3](src/grafica_kpi_3.png)

**Conclusiones:**

1. El mayor responsable de accidentes de tránsito del último semestre (2021-2) es el ``auto`` por está razón de realiza todo el análisis para este acusado.

2. Dado que no tenemos datos previos al año 2016 nuestra primer medida relaciona el semestre `2016_1` y `2016_2` por eso solo se evidencian valores a partir del semestre `2016_2`.<br>

3. Si el valor del semestre en la gráfica es positivo significa que para ese semestre hubo ``menos accidentes ocasionados por autos`` que el semestre pasado.<br>

4. Si la gráfica tiene pendiente positiva (creciente) significa que la ``diferencia de accidentes ocasionados por autos`` vs. el semestre anterior ``aumentó de manera positiva``.<br>

5. El valor que se representa en la gráfica indica el porcentaje en que se redujo la ``cantidad de accidentes causados por autos`` del semestre anterior vs. el actual. Dado que el objetivo es que dicho valor sea ``superior al 5%`` se puede concluir que en el periodo de 6 años comprendido entre 2016 y 2021 se cumplió para los semestres:

    - 2017_2: Se ``reducen`` los accidentes causados por autos vs. el semestre anterior. Dicha diferencia es mayor que la del semestre pasado..<br>

    - 2019_2: Se ``reducen`` los accidentes causados por autos vs. el semestre anterior. Dicha diferencia es mayor que la del semestre pasado.<br>

    - 2020_1: Se ``reducen`` los accidentes causados por autos vs. el semestre anterior. Dicha diferencia es menor que la del semestre pasado.<br>

    - 2021_1: Se ``reducen`` los accidentes causados por autos vs. el semestre anterior. Dicha diferencia es mayor que la del semestre pasado.

6. 4 semestres de 11 cumplieron el objetivo lo cual nos indica que ``no es positivo el balance`` de acuerdo a lo planteado inicialmente

7. 5 semestres de 11 tienen un porcentaje de cambio negativo, es decir, aumentan los accidentes ocasionados vs. el semestre anterior. Aunque es minoría sigue siendo alarmante la cantidad