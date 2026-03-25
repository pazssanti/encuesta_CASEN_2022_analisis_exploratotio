# 📋 Minería de Datos — Encuesta CASEN 2022

Aplicación de técnicas de **minería de datos** a la Encuesta de Caracterización Socioeconómica Nacional (CASEN) 2022, con foco en el análisis de la variable **ingreso laboral** y sus principales predictores en la población chilena.

## 📊 Datos

| Atributo | Detalle |
|----------|---------|
| Fuente | Ministerio de Desarrollo Social y Familia — [CASEN 2022](https://observatorio.ministeriodesarrollosocial.gob.cl/encuesta-casen-2022) |
| Observaciones | 202.231 personas |
| Formato original | SPSS (.sav) |
| Período de aplicación | 1 nov 2022 — 2 feb 2023 |
| Tasa de respuesta | 68,7% |
| Módulos analizados | Registro de Residentes · Educación · Trabajo · Ingreso · Salud · Identidad · Vivienda |

## ⚙️ Métodos

### 1. Análisis exploratorio (EDA)
- Revisión de valores posibles, faltantes y outliers por módulo (2 variables por módulo)
- Todos los datos faltantes clasificados como **MAR** (Missing At Random)

### 2. Análisis detallado — Variable Ingreso
- Estadísticos descriptivos: media = 643.252 CLP, mediana = 477.000 CLP
- Detección de outliers con **z-score** (umbral doble):
  - Outlier global: 1 obs. con ingreso = 25.000.000 CLP (z = 23)
  - Outliers colectivos: 202 obs. en rango 5M–15M CLP (z = 6,7)
- Distribución asimétrica positiva → transformación por raíz cuadrada

### 3. Imputación múltiple (65,69% datos faltantes en ingreso)
Comparación de tres métodos con librería `mice`:

| Método | Resultado |
|--------|-----------|
| PMM (Predictive Mean Matching) | Distribución similar al original |
| **CART** | **Mejor ajuste — distribución más fiel al original** |
| Lasso Regression | Descartado — genera valores negativos |

### 4. Selección de variables
Variables consideradas: edad, sexo, región, jefatura de hogar, personas en el hogar, analfabetismo, nivel educacional, tipo de institución de educación superior, metros cuadrados de vivienda.

| Método | Top 3 variables predictoras del ingreso |
|--------|----------------------------------------|
| Information Gain | Nivel educacional · Tipo institución superior · Edad |
| **Gain Ratio** | **Tipo institución superior (0,107) · Nivel educacional (0,087) · Analfabetismo (0,051)** |

> **Conclusión:** El nivel educativo alcanzado y el tipo de institución de educación superior son los factores que mejor explican el ingreso laboral en Chile.

## 🛠 Herramientas

`R` · `mice` · `FSelector` · `haven` · `ggplot2` · `tidyverse`

## 📁 Contenido del repositorio

```
├── script_casen_2022.R         # Código completo en R
├── informe_final.pdf           # Informe con resultados y análisis
├── libro_codigos.xlsx          # Referencia de variables CASEN
└── README.md
```

## 📚 Referencias

- Ministerio de Desarrollo Social y Familia (2022). *Encuesta de Caracterización Socioeconómica Nacional*.
- Van Buuren, S. (2018). *Flexible Imputation of Missing Data*.
- Romanski, P. et al. (2022). Package 'FSelector' v0.34.
