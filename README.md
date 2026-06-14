# 📈 Análisis Exploratorio y Modelo Predictivo de Riesgo Cardiovascular (Estudio Framingham)

Este repositorio contiene el Análisis Exploratorio de Datos (EDA) y el desarrollo de un modelo de Machine Learning diseñado para predecir el riesgo de enfermedad coronaria a diez años (TenYearCHD) en pacientes, utilizando los datos históricos del estudio clínico Framingham.

## 📊 Resumen Ejecutivo para la Alta Dirección

### 1. Diagnóstico de la Materia Prima (Calidad de los Datos)
El conjunto de datos cuenta con un registro histórico de 4,238 pacientes y 16 variables clínicas. Durante la fase de auditoría e ingeniería de datos, se detectaron las siguientes anomalías:
- **Datos Ausentes:** Se identificaron valores nulos significativos en variables críticas como Glucosa (388 registros nulos) y Educación (105 nulos).
- **Estrategia de Imputación:** Para evitar sesgos, las variables cuantitativas continuas (Glucosa, BMI, Colesterol) fueron imputadas utilizando la mediana de la población, aislando así el impacto de los valores atípicos (outliers). Las variables categóricas se completaron utilizando la moda.
- **Desbalance Crítico de Clases:** Solo el 15.19% de los pacientes analizados presentan un riesgo real de enfermedad coronaria frente a un 84.80% de pacientes sanos. Este severo desbalance exigió una estrategia analítica avanzada para evitar falsos negativos en el diagnóstico.

### 2. Factores de Mayor Impacto Clínico
El análisis de selección de características determinó que las variables con mayor peso matemático y correlación directa con el riesgo cardíaco a largo plazo son:
1. **Edad (Age):** Correlación de +0.23.
2. **Presión Arterial Sistólica (sysBP):** Correlación de +0.22.
3. **Hipertensión Prevalente (prevalentHyp):** Correlación de +0.18.

## 🧠 Evaluación del Modelo Predictivo y Criterio de Sostenibilidad

Para la toma de decisiones médicas, se implementó un algoritmo de Regresión Logística con pesos balanceados (`class_weight='balanced'`) para corregir el desbalance de la población. El modelo alcanzó una Exactitud Global (Accuracy) del 67.92% y una Sensibilidad (Recall) del 68%.

### Justificación de la Métrica de Negocio (Recall vs. Precisión)
En un entorno clínico y de gestión de recursos de salud, maximizar la **Exactitud Global** de forma ciega es un error crítico, ya que un algoritmo básico podría predecir que "todos los pacientes están sanos" y acertar el 85% de las veces, dejando morir a la totalidad de los pacientes de riesgo. 

Por ello, priorizamos la métrica de **Recall (Sensibilidad)**:
- **Detección Prioritaria (Vidas Salvadas):** El modelo detecta correctamente a casi 7 de cada 10 pacientes con riesgo real (88 alertas clínicas correctas emitidas en el entorno de validación).
- **Costo de Oportunidad Controlado:** Esta configuración genera una tasa controlada de Falsos Positivos (231 pacientes sanos alertados de forma preventiva). Clínicamente, preferimos asumir el costo de realizar pruebas adicionales a un paciente sano antes que dar de alta erróneamente a un paciente en riesgo inminente (principio de precaución médica).
- **Sostenibilidad Sanitaria:** Mantener el umbral de decisión estándar protege la economía de los pacientes humildes e impide la saturación de los laboratorios de salud con falsas alarmas masivas innecesarias, logrando el equilibrio perfecto entre ética médica y viabilidad financiera.

## 🛠️ Estructura del Repositorio
- `Practica2_Josue_Diaz_Contreras.ipynb`: Jupyter Notebook que contiene el pipeline de desarrollo completo (Extracción, Limpieza mediante Pandas, Visualización con Seaborn/Matplotlib y modelado con Scikit-Learn).
- `heart_disease.csv`: Conjunto de datos original del estudio Framingham.
- `README.md`: Informe ejecutivo actual para la alta dirección.