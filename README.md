# Challenge Telecom X Latam: Análisis Predictivo de Cancelación (Churn)

## Descripción del Proyecto

Este proyecto tiene como objetivo analizar los factores que influyen en la cancelación de clientes (Churn) en una empresa de telecomunicaciones en Latinoamérica y desarrollar modelos predictivos para identificar a los clientes en riesgo. El análisis se basa en un conjunto de datos que contiene información sobre los servicios contratados, datos demográficos, información de facturación y estado de cancelación de los clientes.

## Estructura del Cuaderno (Workflow)

El análisis y modelado se llevaron a cabo siguiendo los siguientes pasos principales:

1.  **Preparación de los Datos:**
    *   Extracción y carga de los datos tratados.
    *   Eliminación de columnas no relevantes para el análisis.
    *   Codificación de variables categóricas a formato numérico (One-Hot Encoding) utilizando `ColumnTransformer`.
    *   Manejo de valores faltantes mediante imputación (Imputer).
    *   Estandarización de variables numéricas utilizando `StandardScaler` para preparar los datos para modelos sensibles a la escala.
    *   Verificación de la proporción de la variable objetivo (Churn) para evaluar el desbalance de clases.

2.  **Correlación y Selección de Variables:**
    *   Análisis de la matriz de correlación para identificar relaciones entre las variables y la variable objetivo (`Churn`).
    *   Análisis dirigido de variables específicas (ej. `tenure`, `Cuenta_Total`, `Cuenta_Mensual`) en relación con `Churn` mediante visualizaciones (boxplots, scatter plots).

3.  **Modelado Predictivo:**
    *   Separación del conjunto de datos preprocesado en conjuntos de entrenamiento y prueba (`train_test_split`).
    *   Creación y entrenamiento de dos modelos de clasificación:
        *   K-Nearest Neighbors (KNN) - Modelo sensible a la escala.
        *   Random Forest - Modelo no sensible a la escala.
    *   Realización de predicciones en el conjunto de prueba con ambos modelos.

4.  **Evaluación de los Modelos:**
    *   Evaluación del rendimiento de cada modelo utilizando métricas clave: Exactitud, Precisión, Recall, F1-score.
    *   Análisis de la Matriz de Confusión para comprender los tipos de errores de predicción de cada modelo.
    *   Comparación crítica del desempeño de los modelos.

5.  **Interpretación y Conclusiones:**
    *   Análisis de la importancia de las variables, principalmente utilizando la importancia de características proporcionada por el modelo Random Forest, para identificar los principales impulsores del Churn.
    *   Elaboración de una conclusión estratégica que resuma los factores clave de cancelación y proponga estrategias de retención basadas en los hallazgos.

## Informe General de Resultados

### Rendimiento de los Modelos (en el Conjunto de Prueba)

Se evaluaron dos modelos, KNN y Random Forest, utilizando datos preprocesados. Las métricas clave obtenidas fueron:

Modelo         | Exactitud | Precisión | Recall    | F1-score
---------------|-----------|-----------|-----------|-----------
KNN            | 0.7565  | 0.5309  | 0.4599  | 0.4928
Random Forest  | 0.7950  | 0.6624  | 0.4144  | 0.5099

El modelo **Random Forest** mostró una Exactitud y Precisión ligeramente superiores, lo que indica una mejor capacidad general para clasificar correctamente y una mayor confiabilidad cuando predice un caso de Churn. El modelo **KNN** tuvo un Recall ligeramente mayor, siendo un poco mejor en identificar clientes que sí cancelaron, aunque con más falsos positivos. La elección del "mejor" modelo dependerá de los objetivos específicos del negocio (ej. minimizar pérdidas por Churn vs. minimizar costos de campañas de retención en Falsos Positivos).

### Factores Clave que Influyen en la Cancelación

El análisis de la importancia de las variables (principalmente del modelo Random Forest) reveló que los siguientes factores son los más influyentes en la decisión de un cliente de cancelar el servicio:

*   **Tiempo de Contrato (`tenure`):** Los clientes con menor antigüedad son más propensos a cancelar.
*   **Tipo de Contrato (`Month-to-month` vs. `Two year`):** Los contratos mes a mes tienen una asociación fuerte y positiva con la cancelación.
*   **Servicio de Internet (`Fiber optic` vs. `No`):** Tener fibra óptica se asocia con mayor Churn, mientras que no tener internet se asocia con menor Churn.
*   **Método de Pago (`Electronic check`):** El cheque electrónico parece ser un método de pago asociado a una mayor probabilidad de cancelación.
*   **Gasto Total (`Cuenta_Total`) y Gasto Mensual (`Cuenta_Mensual`):** El gasto total se correlaciona negativamente con el Churn (clientes con más gasto total cancelan menos), mientras que el gasto mensual tiene una correlación positiva.

## Estrategias de Retención Propuestas

Basado en los factores clave identificados, se proponen las siguientes estrategias para reducir la tasa de cancelación:

*   **Programas de Onboarding y Retención Temprana:** Enfocarse en la satisfacción del cliente durante los primeros meses de servicio.
*   **Incentivos para Contratos a Largo Plazo:** Promover la migración de contratos mes a mes a contratos de mayor duración mediante ofertas y beneficios.
*   **Mejora del Servicio de Fibra Óptica:** Investigar y abordar las posibles causas de insatisfacción de los usuarios de fibra óptica.
*   **Análisis y Optimización de Métodos de Pago:** Entender la relación entre el método de pago de cheque electrónico y el Churn, y considerar alternativas o mejoras.
*   **Programas de Fidelización:** Recompensar a los clientes de mayor antigüedad y con mayor gasto total.
*   **Promoción y Mejora de Servicios de Valor Añadido:** Destacar los beneficios de servicios como seguridad online y soporte técnico de calidad.

## Consideraciones Futuras

*   Explorar otras técnicas de balanceo de clases (como SMOTE en el conjunto de entrenamiento) y evaluar su impacto en el rendimiento del modelo.
*   Optimizar los hiperparámetros de los modelos utilizando técnicas como Grid Search o Random Search con validación cruzada.
*   Evaluar otros modelos de clasificación relevantes para problemas de Churn.
*   Considerar métricas adicionales como el Área bajo la Curva ROC (AUC).
