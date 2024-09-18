
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

### 1. DecisionTreeClassifie con balanceo tipo undersampling

![Captura de pantalla 2024-09-18 170403](https://github.com/user-attachments/assets/600b03ae-c0f6-4fac-b330-d49c98d72235)


###  Evaluar la Eficiencia del Modelo `DecisionTreeClassifier`
Observamos métricas muy favorables en el conjunto de prueba, pero es crucial verificar si el modelo está sobreajustado a los datos. El objetivo de este análisis es garantizar que el modelo no solo funcione bien en los datos de entrenamiento, sino que también tenga la capacidad de generalizar a datos nuevos y desconocidos en escenarios reales. Si el modelo está sobreajustado, su desempeño en producción podría ser deficiente, lo que conllevaría a decisiones inadecuadas o predicciones poco confiables, afectando negativamente los resultados y la toma de decisiones basadas en esos datos


| Métrica                           | Valor                                           |
|------------------------------------|-------------------------------------------------|
| Exactitud en los datos de entrenamiento | 1.00                                            |
| Exactitud en los datos de prueba   | 0.87                                            |
| Profundidad del árbol              | 17                                              |
| Número de divisiones               | 214                                             |
| Número de hojas                    | 215                                             |
| Puntuaciones de validación cruzada | [0.89122807 0.89473684 0.91197183 0.9084507  0.88380282] |
| Exactitud media de validación cruzada | 0.90                                            |

Observamos una precisión del 100 % en el conjunto de entrenamiento y un 87 % en el conjunto de prueba, lo que sugiere que el modelo podría estar sobreajustado. Aunque las métricas en el conjunto de prueba siguen siendo relativamente buenas, la presencia de sobreajuste es motivo de preocupación por varias razones:

### Posibles problemas con el conjunto de prueba:
El hecho de que el modelo tenga un desempeño tan alto en el conjunto de entrenamiento y menor en el conjunto de prueba podría significar que el conjunto de prueba no es lo suficientemente diverso o representativo. Esto implica que el modelo podría fallar drásticamente cuando se enfrente a datos nuevos y más variados en producción, afectando su capacidad de generalización.

### Rendimiento inestable:
El sobreajuste puede hacer que el modelo tenga un comportamiento inconsistente en datos nuevos. Un modelo que se ajusta demasiado a los datos de entrenamiento se vuelve menos flexible, y su desempeño en entornos reales o conjuntos de datos no vistos puede ser impredecible. Esto genera incertidumbre sobre cómo reaccionará el modelo en la práctica frente a datos no etiquetados.

### Parámetros del árbol:
En nuestro modelo, la profundidad del árbol es 21, el número de divisiones es 193 y el número de hojas es 194. Estos parámetros indican que el árbol es bastante complejo, lo que puede contribuir al sobreajuste. Un árbol con una profundidad elevada y un alto número de divisiones y hojas puede ajustarse demasiado a los datos de entrenamiento, capturando ruido y patrones específicos en lugar de generalizar.

### Validación cruzada:
Para abordar este problema, utilizamos la validación cruzada, una técnica que divide los datos en múltiples subconjuntos y entrena el modelo en distintas combinaciones de estos subconjuntos, evaluando su rendimiento en los datos restantes. En nuestro caso, las puntuaciones de validación cruzada fueron consistentes, con una precisión promedio de aproximadamente 90 %. Esto indica que, aunque el modelo muestra señales de sobreajuste, tiene una buena capacidad de generalización en otras particiones de los datos. Sin embargo, la diferencia entre la precisión en el conjunto de prueba y las puntuaciones de validación cruzada sugiere que el sobreajuste aún debe ser monitoreado.

### En resumen:
Aunque el modelo parece funcionar bien en algunos casos, el riesgo de sobreajuste puede limitar su desempeño en situaciones del mundo real, lo que podría llevar a predicciones inexactas o inestables.

## 2. DecisionTreeClassifie con balanceo tipo undersampling con parámetros del arbol ajustados

![Captura de pantalla 2024-09-18 170902](https://github.com/user-attachments/assets/40e6f2a9-6e73-41c9-9728-9801b15171b7)



Tras ajustar los parámetros del árbol de decisión, los resultados obtenidos son los siguientes:

| **Métrica**                             | **Valor** |
|-----------------------------------------|-----------|
| **Profundidad del árbol**                | 10        |
| **Número de divisiones**                 | 127       |
| **Número de hojas**                     | 128       |
| **Exactitud en los datos de entrenamiento** | 0.86      |
| **Exactitud en el conjunto de prueba**   | 0.73     |
| **Exactitud media de validación cruzada** | 0.71      |
| **Puntuaciones de validación cruzada**   | [0.71078431 0.67980296 0.69950739 0.75862069 0.69458128 0.71921182
 0.71428571] |

#### Análisis del Modelo

1. **Reducción del Sobreajuste:**
   - **Exactitud en Entrenamiento vs. Prueba:** La exactitud en el conjunto de entrenamiento ha disminuido a 0.86, mientras que en el conjunto de prueba es 0.73. Aunque esto indica una reducción en el sobreajuste comparado con el modelo anterior, donde la exactitud de entrenamiento era del 100%, la diferencia aún es notable. El modelo sigue teniendo un desempeño mucho mejor en los datos de entrenamiento que en los de prueba.

2. **Desempeño en el Conjunto de Prueba:**
   - **Exactitud y Métricas:** La exactitud de 0.73 en el conjunto de prueba muestra una mejora en comparación con el modelo anterior, pero sigue siendo una señal de que el modelo podría no estar generalizando de manera óptima. Las métricas de precisión y recall para ambas clases están relativamente equilibradas, pero no sobresalientes, lo que sugiere que el modelo podría no ser suficientemente robusto.

3. **Validación Cruzada:**
   - **Consistencia del Modelo:** Las puntuaciones de validación cruzada varían entre 0.69 y 0.71, con una media de 0.71. Aunque esto indica cierta consistencia en el rendimiento, la diferencia con la exactitud en el conjunto de prueba muestra que aún podría haber problemas con la capacidad de generalización del modelo.

4. **Evaluación General:**
   - **Generalización:** Aunque hemos reducido el sobreajuste, el modelo todavía muestra un desempeño inferior en datos no vistos. Esto sugiere que el modelo puede tener dificultades para generalizar adecuadamente a datos nuevos, y su desempeño en un entorno real podría no ser confiable.


### 3. DecisionTreeClassifie Balanceando el conjunto de datos con Smote con parámetros del arbol ajustados


![Captura de pantalla 2024-09-18 171551](https://github.com/user-attachments/assets/e12ff75d-23d4-4b19-9fe7-8a9013bb7ae8)



| Métrica                           | Valor                                                                 |
|-----------------------------------|-----------------------------------------------------------------------|
| Exactitud en el conjunto de entrenamiento | 0.89                                                                |
| Exactitud en el conjunto de prueba        | 0.76                                                                  |
| Puntuaciones de validación cruzada        |[0.80947776 0.86266925 0.86073501 0.84607938 0.86737657]|
| Exactitud media de validación cruzada     | 0.85                                                                  |


**Desempeño del Modelo:**

- **Exactitud en Entrenamiento vs. Prueba:** La exactitud en el conjunto de entrenamiento es del 89%, mientras que en el conjunto de prueba es del 76%. Esta diferencia significativa indica que el modelo puede estar sobreajustado a los datos de entrenamiento, mostrando un buen desempeño en esos datos pero no generalizando tan bien a nuevos datos.

**Precision y Recall:**

- **Clase Mayoritaria (0):** La precisión para la clase mayoritaria (0) es alta (0.93), y el recall es de 0.78. Esto indica que el modelo está haciendo un buen trabajo en identificar correctamente la clase mayoritaria.
- **Clase Minoritaria (1):** La precisión para la clase minoritaria (1) es baja (0.36), junto con el recall  (0.67). Esto sugiere que,  el modelo sigue teniendo dificultades para identificar correctamente los casos de la clase minoritaria e inclusive más que el modelo anterior 

**Validación Cruzada:**

- Las puntuaciones de validación cruzada son consistentemente altas (promedio de 0.87). Sin embargo, estas puntuaciones pueden estar influenciadas por la clase mayoritaria, lo que puede no reflejar con precisión el rendimiento del modelo en la clase minoritaria.



## Modelos de Regresión Logística: Análisis y Resultados

### 4. `LogisticRegression` con Undersampling


![Captura de pantalla 2024-09-18 172748](https://github.com/user-attachments/assets/7b183156-e8a4-4602-a6dd-563361342b5f)

.**Exactitud del Modelo:**
- Conjunto de entrenamiento: **0.74**
- Conjunto de prueba: **0.65**

**Análisis del Desempeño del Modelo:**
Este modelo sigue presentando problemas de sobreajuste, lo que indica que el modelo no se ajusta bien a los datos de prueba. Aunque el conjunto de entrenamiento alcanza una exactitud del 74%, en el conjunto de prueba la precisión baja al 65%. Esto sugiere que el modelo podría no estar generalizando bien y podría estar sobreentrenado para los datos balanceados con undersampling.

---

### 5. LogisticRegression con balanceo tipo undersampling con variables seleccionadas  de DecisionTreeClassifie


![Captura de pantalla](https://github.com/user-attachments/assets/c0521eb5-57d3-4015-aaf3-b75b97201deb)

**Puntuaciones de Validación Cruzada:**
- [0.63926499, 0.84526112, 0.86363636, 0.83639884, 0.84511133]
- **Exactitud media de validación cruzada:** 0.81
  
**Análisis del Desempeño del Modelo:**
Este modelo muestra una exactitud consistente del **81%** tanto en el conjunto de entrenamiento como en el conjunto de prueba, lo que indica que no está sobreajustado y generaliza bien. Sin embargo, aunque el modelo tiene un buen rendimiento global, sigue presentando dificultades para predecir correctamente la clase minoritaria (empleados que han renunciado).

- **Precisión para la clase 1:** 0.41
- **Recall para la clase 1:** 0.46

Esto significa que, aunque el modelo tiene buen rendimiento global, no es efectivo para identificar empleados que han renunciado (clase 1). Solo el **41%** de las predicciones de renuncia son correctas, y de todos los empleados que efectivamente renunciaron, solo el **46%** fueron identificados correctamente.

**Conclusión:**
A pesar de que la técnica SMOTE ha mejorado la capacidad del modelo para generalizar, todavía queda margen para mejorar la identificación de la clase minoritaria.
