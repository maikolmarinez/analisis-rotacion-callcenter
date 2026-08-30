# Análisis de Retención de Agentes en Call Center

Proyecto de análisis de datos en Python que identifica los factores más asociados a la rotación (attrition) de empleados, aplicado al contexto de operaciones de call center. Incluye un dashboard interactivo en Power BI de 4 páginas para exploración visual de los hallazgos.

## Contexto

Con 7 años de experiencia en call centers, primero como agente y luego como supervisor, he vivido de cerca uno de los mayores retos operativos de la industria: la alta rotación de personal. Este proyecto nace de esa experiencia — busca aplicar herramientas de análisis de datos para entender, con evidencia cuantitativa, los factores que más influyen en que un agente decida quedarse o irse.

## Objetivo

Identificar los patrones y variables más asociados a la rotación de empleados, y traducir esos hallazgos en recomendaciones accionables para equipos de operaciones y recursos humanos en entornos de call center.

## Metodología

- **Dataset:** IBM HR Analytics Employee Attrition & Performance (adaptado al lenguaje de call center)
- **Variables sintéticas agregadas:** `AHT_Segundos`, `CSAT` y `Ausentismo_Dias`, generadas con relación lógica a variables existentes (turno extendido, satisfacción laboral, rotación) para enriquecer el análisis con métricas típicas de la industria
- **Herramientas:** Python (pandas, matplotlib, seaborn, scikit-learn) para el análisis y modelo predictivo; Power BI para el dashboard interactivo
- **Flujo de trabajo:** carga y limpieza de datos → análisis exploratorio (EDA) → variables sintéticas → modelo predictivo (regresión logística) → dashboard interactivo (4 páginas) → conclusiones y recomendaciones de negocio

## Dashboard interactivo (Power BI)

El dashboard está organizado en 4 páginas navegables mediante botones:

- **Inicio:** landing page con overview del proyecto, descripción, y tarjetas de navegación a cada sección con un indicador visual resumen (tendencia de rotación por antigüedad, distribución por estado civil, y precisión del modelo).
- **Rotación:** KPIs generales (% rotación, ausentismo promedio, antigüedad promedio) y las relaciones clave: turno extendido, ausentismo y antigüedad, con filtro interactivo por departamento.
- **Perfil Demográfico:** rotación por estado civil, nivel de puesto, nivel educativo, salario mensual y género, con filtro interactivo por campo de estudio.
- **Compensación y Desarrollo:** rotación por tiempo sin ascenso, nivel de beneficios (stock options) e historial de empresas previas — las variables de mayor peso en el modelo predictivo que no se cubren en las páginas anteriores.

Todas las visualizaciones de rotación usan un esquema de formato condicional de 3 niveles (bajo/medio/alto riesgo) para identificar rápidamente los grupos de mayor riesgo.

**Nota de diseño sobre los filtros:** en las páginas con slicer (Rotación y Perfil Demográfico), los colores de alerta comparan siempre contra el promedio general de la empresa, no contra el grupo actualmente filtrado. Esto es una decisión de diseño intencional: al aplicar un filtro muy específico, algunos grupos pueden quedar con pocos empleados, por lo que los promedios resultantes deben interpretarse con cautela.

Archivo: `dashboard_callcenter.pbix`
<img width="967" height="539" alt="Screenshot 2026-08-24 155213" src="https://github.com/user-attachments/assets/b2e3100f-58f4-45b1-988f-632d0d699b29" />
<img width="964" height="536" alt="Screenshot 2026-08-24 155309" src="https://github.com/user-attachments/assets/edbdfa8a-3bc2-4353-903f-f776e696754b" />
<img width="974" height="544" alt="Screenshot 2026-08-24 155039" src="https://github.com/user-attachments/assets/4212b787-ee0c-42d0-bef1-113f7ac54088" />

## Hallazgos clave

- La tasa de rotación general en la muestra analizada fue del **16.1%**.
- Los empleados con **turno extendido (horas extra)** presentan una proporción de rotación notablemente más alta (~30% vs. ~10%).
- La rotación se concentra en los **primeros años de antigüedad** (mediana ~3 años en quienes se van vs. ~5-7 años en quienes se quedan).
- Los empleados **solteros** presentan una rotación notablemente mayor que casados o divorciados.
- La rotación es más alta en **niveles de puesto bajos (entry level)**, disminuyendo conforme sube el nivel jerárquico.
- El **nivel de beneficios (stock options)** funciona como factor protector: nivel 0 (sin beneficios) concentra el mayor riesgo.
- El **tiempo sin ascenso** y el **historial de rotación previa** (número de empresas anteriores) pesan más en la predicción que el salario mensual.
- La **distancia al trabajo** también se asocia a mayor probabilidad de rotación.
- El **ausentismo promedio** es notablemente mayor en empleados que rotaron (variable sintética, ver nota de limitaciones).
- El modelo de regresión logística alcanzó una precisión del **88.4%** con las variables originales, y del **93.2%** al incorporar las variables sintéticas de call center.

## Nota sobre data leakage

Al incorporar `Ausentismo_Dias` al modelo predictivo, la precisión subió a 93.2% y esta variable resultó ser, por mucho, la más predictiva (peso muy por encima del resto). Esto se debe a que la variable fue construida deliberadamente con una relación directa a `Rotacion` (se le asignó más ausentismo a quienes rotaron), lo cual constituye un caso de **data leakage**: el modelo "aprende" una relación que en parte fue definida artificialmente, no descubierta de los datos. En un entorno real, esta métrica se calcularía de forma independiente a partir de registros de asistencia, y su relación con la rotación tendría que validarse, no asumirse. Este resultado se documenta de forma transparente como parte del ejercicio, no como una conclusión definitiva.

## Recomendaciones

- Priorizar la retención en los primeros 12-24 meses con seguimiento cercano de supervisor a nuevos ingresos.
- Rotar o limitar la exposición a turnos extendidos, especialmente en agentes de baja antigüedad.
- Crear rutas de crecimiento visibles a corto plazo que no dependan exclusivamente de años de servicio.
- Evaluar políticas de flexibilidad de horario o modalidad remota/híbrida para agentes con mayor distancia al centro de trabajo.
- Revisar la estructura de beneficios (stock options u otros incentivos) para agentes en niveles de puesto iniciales, donde se concentra el mayor riesgo.

## Limitaciones

Este proyecto utilizó un dataset adaptado de IBM (no datos reales de un call center), por lo que los hallazgos deben tomarse como hipótesis a validar con datos operativos reales. Las variables de AHT, CSAT y Ausentismo son sintéticas y con fines ilustrativos (ver nota de data leakage arriba). Al filtrar por departamento o campo de estudio, algunos segmentos quedan con muestras pequeñas, lo que reduce la confiabilidad estadística de esos subgrupos. Se recomienda replicar este análisis con datos operativos genuinos para validar los patrones encontrados.

## Nota personal

*Durante mi desempeño como supervisor, tuve muchas rotaciones de parte de agentes que eran estudiantes activos y, en su gran mayoría, fueron a causa del cambio de horario en la universidad. Otros simplemente no podían con la carga académica y el estrés laboral.*

## Cómo ejecutar el proyecto

1. Clona este repositorio o descarga los archivos.
2. Instala las librerías necesarias:
   ```
   pip install pandas matplotlib seaborn scikit-learn numpy
   ```
3. Descarga el dataset [IBM HR Analytics Employee Attrition & Performance](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) desde Kaggle.
4. Coloca el archivo CSV en la misma carpeta que el notebook.
5. Abre `notebook.ipynb` en Jupyter Notebook o JupyterLab y ejecuta las celdas en orden.
6. Para el dashboard, abre `dashboard_callcenter.pbix` con Power BI Desktop. Usa los botones de la página "Inicio" para navegar entre secciones (requiere modo de lectura/presentación, no modo edición).

## Autor

Maikol — Analista con experiencia en operaciones de call center (agente y supervisor), aplicando análisis de datos en Python y Power BI para conectar la experiencia operativa con evidencia cuantitativa.
