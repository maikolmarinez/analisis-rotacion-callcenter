Análisis de Retención de Agentes en Call Center
Proyecto de análisis de datos en Python que identifica los factores más asociados a la rotación (attrition) de empleados, aplicado al contexto de operaciones de call center.
Contexto
Con 7 años de experiencia en call centers, primero como agente y luego como supervisor, he vivido de cerca uno de los mayores retos operativos de la industria: la alta rotación de personal. Este proyecto nace de esa experiencia — busca aplicar herramientas de análisis de datos para entender, con evidencia cuantitativa, los factores que más influyen en que un agente decida quedarse o irse.
Objetivo
Identificar los patrones y variables más asociados a la rotación de empleados, y traducir esos hallazgos en recomendaciones accionables para equipos de operaciones y recursos humanos en entornos de call center.
Metodología
Dataset: IBM HR Analytics Employee Attrition & Performance (adaptado al lenguaje de call center)
Herramientas: Python — pandas, matplotlib, seaborn, scikit-learn
Flujo de trabajo: carga y limpieza de datos → análisis exploratorio (EDA) → modelo predictivo (regresión logística) → conclusiones y recomendaciones de negocio
Hallazgos clave
La tasa de rotación general en la muestra analizada fue del 16.1%.
Los empleados con turno extendido (horas extra) presentan una proporción de rotación notablemente más alta.
La rotación se concentra en los primeros años de antigüedad (mediana ~3 años en quienes se van vs. ~5 años en quienes se quedan).
El tiempo sin ascenso y el historial de rotación previa (número de empresas anteriores) pesan más en la predicción que el salario mensual.
La distancia al trabajo también se asocia a mayor probabilidad de rotación.
El modelo de regresión logística alcanzó una precisión del 88.4%.
Recomendaciones
Priorizar la retención en los primeros 12-24 meses con seguimiento cercano de supervisor a nuevos ingresos.
Rotar o limitar la exposición a turnos extendidos, especialmente en agentes de baja antigüedad.
Crear rutas de crecimiento visibles a corto plazo que no dependan exclusivamente de años de servicio.
Evaluar políticas de flexibilidad de horario o modalidad remota/híbrida para agentes con mayor distancia al centro de trabajo.
Limitaciones
Este proyecto utilizó un dataset adaptado de IBM (no datos reales de un call center), por lo que los hallazgos deben tomarse como hipótesis a validar con datos operativos reales. Se recomienda replicar este análisis con variables específicas de la industria como AHT, CSAT y ausentismo para mayor precisión.
Cómo ejecutar el proyecto
Clona este repositorio o descarga los archivos.
Instala las librerías necesarias:
```
   pip install pandas matplotlib seaborn scikit-learn
   ```
Descarga el dataset IBM HR Analytics Employee Attrition & Performance desde Kaggle.
Coloca el archivo CSV en la misma carpeta que el notebook.
Abre `notebook.ipynb` en Jupyter Notebook o JupyterLab y ejecuta las celdas en orden.
Autor
Maikol — Analista con experiencia en operaciones de call center (agente y supervisor), aplicando análisis de datos en Python para conectar la experiencia operativa con evidencia cuantitativa.
