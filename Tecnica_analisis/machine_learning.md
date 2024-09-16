
# Modelos de Machine Learning

El objetivo de este proyecto es entrenar varios modelos de machine learning para clasificar a los empleados de una empresa. El propósito es identificar los grupos en los que se deben enfocar los esfuerzos para reducir la tasa de renuncias.

## Dataset

El dataset utilizado contiene información de:
- **3.699 empleados** que aún están en la compañía.
- **711 empleados** que ya han renunciado.

## Balanceo del Conjunto de Datos

Dado que el número de empleados que han renunciado es significativamente menor que el de los empleados que aún permanecen en la compañía, es esencial balancear el conjunto de datos para mejorar la precisión y eficacia de los modelos. Aplicaremos las siguientes técnicas de preprocesamiento para lograr este balanceo:

1. **Undersampling:**
   - **Descripción:** Implementaremos un procedimiento de undersampling para equilibrar las clases en el conjunto de datos. En este caso, la clase mayoritaria (empleados que aún están en la compañía) tiene muchas más instancias que la clase minoritaria (empleados que han renunciado).
   - **Objetivo:** Reducir el número de instancias en la clase mayoritaria para igualar el número de instancias en ambas clases. Este enfoque busca mitigar el desbalanceo de clases, garantizando que el número de instancias en cada clase sea equivalente.
   - **Beneficio:** Mejora el rendimiento de los modelos de aprendizaje automático al evitar que el modelo se sesgue hacia la clase mayoritaria, resultando en una clasificación más justa y precisa.

2. **Oversampling con SMOTE:**
   - **Descripción:** Utilizaremos la técnica de oversampling con SMOTE (Synthetic Minority Over-sampling Technique) para abordar el desbalanceo de clases. SMOTE genera nuevas instancias sintéticas para la clase minoritaria, creando un conjunto de datos más equilibrado.
   - **Objetivo:** Aumentar el número de instancias en la clase minoritaria mediante la creación de nuevos ejemplos sintéticos. Esto ayuda al modelo a aprender mejor los patrones asociados con la clase minoritaria.
   - **Beneficio:** Mejora la capacidad del modelo para identificar y aprender de la clase minoritaria, reduciendo el sesgo hacia la clase mayoritaria y proporcionando una clasificación más equilibrada y efectiva.

La aplicación de estas técnicas de balanceo permitirá que los modelos sean más efectivos y proporcionen resultados más precisos en la predicción de la renuncia de empleados.

## Proceso de Modelado

Una vez balanceado el conjunto de datos utilizando undersampling, aplicaremos el modelo `DecisionTreeClassifier` para:
- **Visualizar la Importancia de las Variables:** Este modelo nos ayudará a identificar qué características tienen mayor impacto en la decisión de un empleado de abandonar la empresa.
- **Evaluar la Eficiencia del Modelo:** Determinaremos qué tan bien se desempeña el modelo en la predicción de la renuncia de empleados.

Este enfoque nos proporcionará una base sólida para analizar la relevancia de las variables y optimizar nuestros modelos de machine learning para obtener predicciones más precisas.




