# Informe de preparación y calidad de datos de empleados

## 1. Descripción del proyecto
Este repositorio contiene un flujo completo de **preparación de datos** para un caso de empleados, orientado a construir una base limpia y transformada para modelos de analítica predictiva (incluyendo clasificación de fuga).

## 2. Objetivo
Preparar los datos de empleados mediante un proceso estructurado de:
- Integración de fuentes.
- Limpieza de variables y calidad de datos.
- Tratamiento de nulos y atípicos.
- Análisis de correlaciones.
- Balanceo de la variable objetivo.
- Transformaciones finales para modelado.

## 3. Contenido del repositorio
- `1_Preparacion_de_datos_Empleados (1).ipynb`: notebook principal con todo el proceso.
- `output.html`: reporte de perfilado de datos generado con `ydata-profiling`.
- `datos_categoricos.xlsx`: salida con variables discretizadas/categorizadas.
- `datos_normalizados.xlsx`: salida con variables normalizadas y codificadas.

## 4. Metodología aplicada

### 4.1 Integración de datos
- Se cargan dos hojas del archivo fuente (`Informacion Personal` e `Informacion Laboral`).
- Se revisan y depuran IDs duplicados.
- Se realiza `merge` por `ID` para consolidar la información.

### 4.2 Eliminación de variables irrelevantes y redundantes
- Se elimina el identificador (`ID`) y se consideran criterios de relevancia de negocio y habeas data.
- Se revisan posibles redundancias matemáticas/estadísticas.

### 4.3 Descripción estadística y exploratoria
- Resumen estadístico (`describe`).
- Histogramas y diagramas de caja para variables numéricas.
- Gráficos de barras para variables categóricas.
- Matriz de dispersión para observar relaciones entre variables.

### 4.4 Perfilado y diagnóstico de calidad
Se genera un perfilado automático con `ydata-profiling` para evaluar dimensiones de calidad:
- **Completitud**
- **Exactitud**
- **Conformidad**
- **Oportunidad**

### 4.5 Limpieza de datos
- Tratamiento de atípicos/errores (ejemplo: incapacidades mayores a 365 días marcadas como nulas).
- Imputación de faltantes:
  - Media para variables numéricas.
  - Moda para variables categóricas.

### 4.6 Correlaciones
- Conversión temporal de categóricas a numéricas (dummies) para cálculo de correlaciones.
- Identificación de:
  - Variables potencialmente redundantes (|r| alto).
  - Variables potencialmente irrelevantes frente al objetivo `Fuga` (|r| bajo).

### 4.7 Balanceo de clases
- Aplicación de técnicas de sobremuestreo (`SMOTE` / `SMOTENC`) para equilibrar la variable objetivo en tareas de clasificación.

### 4.8 Transformaciones para modelado
- **Discretización** de variables numéricas seleccionadas.
- **Normalización** con `MinMaxScaler`.
- **Dummies** para variables categóricas predictoras.
- **Label Encoding** para la variable objetivo.

### 4.9 Exportación de resultados
Se generan dos datasets finales:
- `datos_categoricos.xlsx`
- `datos_normalizados.xlsx`

## 5. Principales hallazgos del diagnóstico
Con base en el análisis documentado en el notebook:
- Se detectan faltantes en algunas variables (por ejemplo, carro y antigüedad).
- Se identifican errores de calidad (por ejemplo, valores atípicos no válidos en incapacidades).
- Se ejecuta una estrategia de corrección e imputación para dejar los datos aptos para modelado.

## 6. Requisitos de ejecución
Entorno recomendado en Python con librerías:
- `pandas`
- `numpy`
- `matplotlib`
- `scikit-learn`
- `imblearn`
- `ydata-profiling`

## 7. Flujo resumido de ejecución
1. Abrir y ejecutar `1_Preparacion_de_datos_Empleados (1).ipynb`.
2. Revisar `output.html` para el perfilado.
3. Validar la generación de `datos_categoricos.xlsx` y `datos_normalizados.xlsx`.

## 8. Resultado final
El proyecto entrega un pipeline de preparación de datos organizado y reproducible, con diagnóstico de calidad, limpieza, balanceo y transformaciones necesarias para etapas posteriores de modelado analítico.
