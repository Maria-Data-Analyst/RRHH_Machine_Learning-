# Procesamiento y Preparación de la Base de Datos

En esta sección, nos familiarizaremos con las  variables disponibles para entender con qué datos contamos.
aquí puedes descargar el dataset que se uso para el proyecto: [Dataset](https://drive.google.com/file/d/1sbNpmhSZ6AtknqU4kJs18_ls91UThNBX/view)

## Descripción de Variables

A continuación se detalla la información contenida en la tabla:

| **Variable**               | **Descripción**                                                                                   |
|----------------------------|---------------------------------------------------------------------------------------------------|
| Age                        | Edad del empleado                                                                                 |
| Attrition                  | Empleado que abandona la empresa (0 = no, 1 = sí)                                                  |
| BusinessTravel             | Describe la frecuencia de los viajes de negocio                                                  |
| Department                 | Indica el departamento en que el empleado trabaja                                                  |
| DistanceFromHome           | Distancia desde la casa del empleado hasta la empresa                                              |
| Education                  | Nivel de educación (1 = 'Debajo de la universidad', 2 = 'Universidad', 3 = 'Licenciatura', 4 = 'Maestría', 5 = 'Doctor') |
| EducationField             | Área de estudio del empleado                                                                       |
| EmployeeCount              | Contaje de empleados                                                                               |
| EmployeeID                 | Número identificador del empleado                                                                  |
| Gender                     | Género del empleado                                                                                |
| JobLevel                   | Nivel del rol del empleado en la empresa                                                           |
| JobRole                    | Nombre del rol del empleado                                                                        |
| MaritalStatus              | Estado civil del empleado                                                                          |
| MonthlyIncome              | Ingreso mensual del empleado                                                                       |
| NumCompaniesWorked         | Número de empresas en las que el empleado ha trabajado                                             |
| Over18                     | Si el empleado es mayor de 18 años (true/false)                                                    |
| PercentSalaryHike          | Aumento porcentual del salario                                                                     |
| StandardHours              | Horas de trabajo estándar                                                                          |
| StockOptionLevel           | Participación en acciones (cuanto mayor sea el número, más opciones sobre acciones tiene un empleado) |
| TotalWorkingYears          | Años trabajados                                                                                    |
| TrainingTimesLastYear      | Total de horas dedicadas a entrenamientos el último año                                             |
| YearsAtCompany             | Años trabajados en esta empresa                                                                    |
| YearsSinceLastPromotion    | Años pasados desde la última promoción                                                             |
| YearsWithCurrManag         | Años trabajando con el actual gerente                                                              |

* La variable **EmployeeCount** ha sido eliminada del análisis porque siempre tiene un valor constante de 1 en todas las filas. Esto sugiere que la columna se utiliza simplemente para indicar que cada registro corresponde a un empleado individual, sin proporcionar información diferenciadora o útil. Dado que esta variable no varía entre los registros y no contribuye al entendimiento o interpretación de los datos, su eliminación simplifica el conjunto de datos y evita confusiones.
  

  ## Identificar y manejar los valores nulos
  
| **Columna**                | **Valores nulos** |
|----------------------------|-------------------|
| Age                        | 0                 |
| Attrition                  | 0                 |
| BusinessTravel             | 0                 |
| Department                 | 0                 |
| DistanceFromHome           | 0                 |
| Education                  | 0                 |
| EducationField             | 0                 |
| EmployeeID                 | 0                 |
| Gender                     | 0                 |
| JobLevel                   | 0                 |
| JobRole                    | 0                 |
| MaritalStatus              | 0                 |
| MonthlyIncome              | 0                 |
| NumCompaniesWorked         | 19                |
| Over18                     | 0                 |
| PercentSalaryHike          | 0                 |
| StandardHours              | 0                 |
| StockOptionLevel           | 0                 |
| TotalWorkingYears          | 9                 |
| TrainingTimesLastYear      | 0                 |
| YearsAtCompany             | 0                 |
| YearsSinceLastPromotion    | 0                 |
| YearsWithCurrManager       | 0                 |

Se segmenta la variable TotalWorkingYears y NumCompaniesWorke por Attrition para imputar los valores nulos de manera que reflejen con mayor precisión las características de los empleados que permanecen en la empresa frente a aquellos que abandonan. Esta segmentación asegura que la imputación sea relevante para cada grupo, manteniendo la integridad de las diferencias potenciales en la frecuencia de entrenamientos entre empleados que permanecen y aquellos que se van, lo que ayuda a mejorar la precisión del modelo de predicción de deserción.

### Nulos NumCompaniesWorke
Para manejar los valores nulos dentro de NumCompaniesWorked primero vamos a visualizar su distribucion y medidas de tendencia central separando los datos mediante la variable Attrition 

  ![image](https://github.com/user-attachments/assets/ee0eaf80-cede-4eaf-b0c6-f63bd9c47836)

  ![image](https://github.com/user-attachments/assets/e5a8f13a-94f5-48ce-9f13-9abf08624bca)

  En este análisis, decidimos imputar los valores nulos en la columna NumCompaniesWorked utilizando la moda (valor más frecuente) para ambos grupos de Attrition (Yes y No). Esta decisión se basa en los siguientes puntos:

* **Representatividad del Valor Más Común:** La moda es el valor más frecuente en nuestros datos, lo que asegura que la imputación sea representativa del comportamiento típico de cada grupo. Dado que la moda en ambos casos es 1, esto refleja que la mayoría de los empleados tienen un historial de trabajo de 1 empresa.

* **Simplicidad y Coherencia:** La moda proporciona una forma sencilla de imputar datos faltantes sin introducir sesgos adicionales. Al usar la moda, mantenemos la coherencia con el valor observado más común en nuestros datos, evitando posibles distorsiones que podrían surgir al usar la media o la mediana en una distribución sesgada.

* **Impacto Mínimo en el Modelo:** Con una gran cantidad de datos (más de 4,000 empleados) y solo 19 valores nulos, la imputación con la moda asegura que los valores faltantes se ajusten a la tendencia general sin afectar significativamente el rendimiento del modelo.

  ### Nulos TotalWorkingYears

  ![image](https://github.com/user-attachments/assets/10c7b5b3-e46c-4364-a9b5-7c5e1aafbee0)


 ![image](https://github.com/user-attachments/assets/bad85a27-10a3-4e3c-915a-aaa0d4211b84)

La moda que representa el valor más frecuente en cada grupo de Attrition, lo cual es adecuado para preservar la distribución general de los datos sin introducir sesgo significativo. Además, dado el bajo número de valores nulos en comparación con el tamaño total del conjunto  de datos (más de 4,000 empleados), esta imputación tiene un impacto mínimo en el rendimiento del modelo, asegurando que la integridad de los datos se mantenga mientras se minimiza la pérdida de información.

## Identificación y Manejo de Valores Duplicados

Se realizó una búsqueda de valores duplicados en la columna `employee_id`, ya que cada ID de empleado debe ser único. A continuación se presentan los resultados:

| Métrica                      | Valor |
|------------------------------|-------|
| Número total de registros    | 4.410  |
| Número de registros duplicados | 0     |

No se encontraron registros duplicados en la columna `employee_id`, lo que confirma que cada ID de empleado es único en el conjunto de datos.

## Identificar inconsistencias y correlaciones

![image](https://github.com/user-attachments/assets/e988c65a-2fc5-4cc9-b164-5a60603141a5)

La variable standard_hours tiene un valor constante de 8 horas en todas las filas del DataFrame. Esto indica que la variable no aporta variabilidad a los datos. Como resultado, la correlación con otras variables será indefinida (o nula) debido a que la desviación estándar de standard_hours es cero. Por esta razón, se excluirá esta variable del análisis.

**Correlación**

![Captura de pantalla 2024-09-11 093339](https://github.com/user-attachments/assets/5d4c6585-7291-47fd-9544-83accbe4ee4b)

## Análisis de la Matriz de Correlación

Observando la matriz de correlación, se destacan algunos puntos interesantes:

1. **Edad y años totales de experiencia laboral (0.68)**: La correlación positiva alta entre la edad y los años de experiencia total es lógica, ya que a medida que las personas envejecen, suelen tener más años acumulados de trabajo.

2. **Edad y número de empresas en las que ha trabajado (0.30)**: Existe una correlación moderada entre la edad y el número de empresas, lo que sugiere que, a medida que los empleados envejecen, es más probable que hayan cambiado de empleo varias veces.

3. **Años en la empresa y años con el mismo gerente (0.77)**: Hay una correlación muy alta entre el tiempo en la empresa y el tiempo con el mismo gerente, lo que indica que, en general, los empleados tienden a permanecer con el mismo gerente a lo largo de su permanencia en la empresa.

4. **Años en la empresa y años desde la última promoción (0.62)**: Una correlación significativa indica que los empleados que llevan más tiempo en la empresa también han pasado más tiempo desde su última promoción.

5. **Años totales de experiencia y años en la empresa (0.63)**: Muestra que los empleados con más años de experiencia tienden a haber pasado más tiempo en la empresa actual.

6. **Sin correlaciones fuertes con el salario mensual**: El salario mensual no muestra correlaciones significativas con otras variables como la experiencia, educación o nivel de trabajo, lo que podría ser un punto a investigar si se espera que el salario esté relacionado con estas características.

7. **Variable sin variabilidad significativa**: La variable **"distance_from_home"** muestra correlaciones muy bajas con otras variables, lo que sugiere que no tiene mucho impacto en las demás características del conjunto de datos.

### Conclusión
En general, algunas de estas correlaciones son esperables (como la relación entre la edad y la experiencia laboral), pero la falta de correlación con el salario es un hallazgo que podría requerir una revisión más profunda, especialmente si se espera que el salario refleje la experiencia o la educación.


## Verificación y Conversión de Tipos de Datos

Para entrenar el modelo, es esencial que todas las variables sean de tipo numérico. Por lo tanto, primero debemos revisar los tipos de datos actuales en nuestro conjunto de datos y determinar cuáles necesitan ser convertidos o procesados para cumplir con los requisitos del modelo.

| Variables                      | Dtype   | Status |
|-------------------------------|---------|--------|
| age                           | int64   | ✅     |
| attrition                     | object  | ❌     |
| business_travel               | object  | ❌     |
| department                    | object  | ❌     |
| distance_from_home            | int64   | ✅     |
| education                     | int64   | ❌     |
| education_field               | object  | ❌     |
| employee_id                   | int64   | ❌     |
| gender                        | object  | ❌     |
| job_level                     | int64   | ✅     |
| job_role                      | object  | ❌     |
| marital_status                | object  | ❌     |
| monthly_income                | int64   | ✅     |
| num_companies_worked          | float64 | ✅     |
| over18                        | object  | ❌     |
| percent_salary_hike           | int64   | ✅     |
| standard_hours                | int64   | ✅     |
| stock_option_level            | int64   | ✅     |
| total_working_years           | float64 | ✅     |
| training_times_last_year      | int64   | ✅     |
| years_at_company              | int64   | ✅     |
| years_since_last_promotion    | int64   | ✅     |
| years_with_curr_manager       | int64   | ✅     |

Podemos observar todas las variables disponibles. Las que están marcadas con ❌ indican que se necesita realizar una conversión de tipo de dato.

### Variables que requieren conversión de tipo de dato

| Variable           | Dtype  |
|--------------------|--------|
| attrition          | object |
| business_travel    | object |
| department         | object |
| education_field    | object |
| employee_id        | int64  |
| gender             | object |
| job_role           | object |
| marital_status     | object |
| over18             | object |
| education          | int64  | 

#### Detalles de las variables

- **attrition**: Indica si el empleado ha abandonado la empresa. En la base de datos, esta variable contiene valores como "Yes" y "No".
  
- **business_travel**: Describe la frecuencia de los viajes de negocio. Los posibles valores son:
  - Travel_Rarely
  - Travel_Frequently
  - Non-Travel
    
- **department**: Indica el departamento en el que trabaja el empleado. Los valores posibles son:
  - Sales
  - Research & Development
  - Human Resources
    
- **education_field**: Muestra el área de estudio del empleado. Los valores posibles son:
  - Life Sciences
  - Medical
  - Marketing
  - Technical Degree
  - Human Resources
  - Other
    
- **gender**: Indica el género del empleado. Los posibles valores son:
  - Female
  - Male
    
- **job_role**: Describe el rol del empleado en la empresa. Los valores posibles son:
  - Healthcare Representative
  - Research Scientist
  - Sales Executive
  - Human Resources
  - Research Director
  - Laboratory Technician
  - Manufacturing Director
  - Sales Representative
  - Manager
    
- **marital_status**: Indica el estado civil del empleado. Los valores posibles son:
  - Married
  - Single
  - Divorced
    
- **over18**: Esta variable indica si el empleado es mayor de 18 años, con el único valor posible siendo "Y". Dado que todos los empleados en el conjunto de datos son mayores de 18 años y no existe variabilidad en esta variable, no aporta información útil para el análisis. Por esta razón, se excluirá del análisis.
- **employee_id**: Es un identificador único del empleado. Aunque actualmente es de tipo entero (`int64`), es mejor manejarlo como `String` para evitar confusiones
  
-  **education**: Nivel de educación (1 = 'Debajo de la universidad', 2 = 'Universidad', 3 = 'Licenciatura', 4 = 'Maestría', 5 = 'Doctorado'). Aunque está codificada numéricamente, esta variable representa categorías ordinales, no valores continuos. Mantenerla así puede llevar a que el modelo asuma una relación lineal entre los niveles educativos, lo cual no es adecuado. Esto podría generar interpretaciones incorrectas, ya que el modelo podría considerar que la diferencia entre los niveles es constante. Para evitar estos problemas, es mejor convertir los niveles educativos en variables dummy, donde cada nivel se represente con un valor binario (0 o 1), facilitando una interpretación más precisa

# Estructura de las Columnas del DataFrame

Se han creado variables dummy para las variables categóricas tipo `object`, omitiendo una categoría por cada variable para evitar la multicolinealidad. A continuación se muestra la estructura de las columnas del DataFrame resultante y las categorías omitidas:

## Columnas del DataFrame Resultante

| No. | Column                              | Non-Null Count | Dtype   |
|-----|-------------------------------------|----------------|---------|
| 0   | age                                 | 4410 non-null   | int64   |
| 1   | distance_from_home                  | 4410 non-null   | int64   |
| 2   | employee_id                         | 4410 non-null   | object  |
| 3   | job_level                           | 4410 non-null   | int64   |
| 4   | monthly_income                      | 4410 non-null   | int64   |
| 5   | num_companies_worked                | 4410 non-null   | float64 |
| 6   | percent_salary_hike                 | 4410 non-null   | int64   |
| 7   | stock_option_level                  | 4410 non-null   | int64   |
| 8   | total_working_years                 | 4410 non-null   | float64 |
| 9   | training_times_last_year            | 4410 non-null   | int64   |
| 10  | years_at_company                    | 4410 non-null   | int64   |
| 11  | years_since_last_promotion          | 4410 non-null   | int64   |
| 12  | years_with_curr_manager             | 4410 non-null   | int64   |
| 13  | business_Travel_Frequently          | 4410 non-null   | int64   |
| 14  | business_Travel_Rarely              | 4410 non-null   | int64   |
| 15  | department_Research & Development   | 4410 non-null   | int64   |
| 16  | department_Sales                    | 4410 non-null   | int64   |
| 17  | education_field_Human Resources     | 4410 non-null   | int64   |
| 18  | education_field_Life Sciences       | 4410 non-null   | int64   |
| 19  | education_field_Marketing           | 4410 non-null   | int64   |
| 20  | education_field_Medical             | 4410 non-null   | int64   |
| 21  | education_field_Technical Degree    | 4410 non-null   | int64   |
| 22  | job_role_Healthcare Representative  | 4410 non-null   | int64   |
| 23  | job_role_Laboratory Technician      | 4410 non-null   | int64   |
| 24  | job_role_Manager                    | 4410 non-null   | int64   |
| 25  | job_role_Manufacturing Director     | 4410 non-null   | int64   |
| 26  | job_role_Research Director          | 4410 non-null   | int64   |
| 27  | job_role_Research Scientist         | 4410 non-null   | int64   |
| 28  | job_role_Sales Executive            | 4410 non-null   | int64   |
| 29  | job_role_Sales Representative       | 4410 non-null   | int64   |
| 30  | marital_status_Married              | 4410 non-null   | int64   |
| 31  | marital_status_Single               | 4410 non-null   | int64   |
| 32  | gender_Male                         | 4410 non-null   | int64   |
| 33  | attrition_Yes                       | 4410 non-null   | int64   |
| 34  | education_Doctorado                 | 4410 non-null   | int64   |
| 35  | education_Licenciatura              | 4410 non-null   | int64   |
| 36  | education_Maestría                  | 4410 non-null   | int64   |
| 37  | education_Universidad               | 4410 non-null   | int64   |

## Categorías Omitidas

- **business_travel**: 'Non-Travel'
- **department**: 'Human Resources'
- **education_field**: 'Other'
- **job_role**: 'Human Resources'
- **marital_status**: 'Divorced'
- **gender**: 'Female'
- **attrition**: 'No'

Estas categorías han sido omitidas para evitar la multicolinealidad, ya que su presencia puede ser inferida a partir de las demás variables dummy.

## Crear nuevas variables

He convertido a formato dummy las variables categóricas, pero aún quedan las variables numéricas continuas que no han sido transformadas. Esto puede generar un sesgo en los modelos, ya que las variables continuas pueden tener más peso debido a sus rangos más amplios, en comparación con las variables dummy, que solo toman valores de 0 y 1.

Además, al no segmentar estas variables continuas, no podemos identificar con precisión qué rangos de valores están más relacionados con la probabilidad de que los empleados renuncien. Para abordar este problema, utilizaremos boxplots para analizar la distribución de cada variable continua y establecer límites de segmentos, que luego transformaremos en variables dummy.
Los segmentos que se convertiran a dummy son los siguientes 
:
 **`age`**
- **18 - 25**: 486 empleados
- **26 - 35**: 1908 empleados
- **36 - 48**: 1497 empleados
- **49 - 60**: 519 empleados

**`distance_from_home`**
- **Cerca**: 3078 empleados
- **Intermedio**: 720 empleados
- **Lejos**: 612 empleados

**`years_at_company`**
- **0 - 3**: 1.410 empleados
- **4 - 10**: 2.262 empleados
- **11 - 20**: 540 empleados
- **20+**: 198 empleados

**`monthly_income`**
- **10k - 40k**: 1.629 empleados
- **40k - 70k**: 1.476 empleados
- **70k - 120k**: 720 empleados
- **120k - 200k**: 585 empleados

**`percent_salary_hike`**
- **11 - 14**: 2.454 empleados
- **15 - 18**: 1.050 empleados
- **19 - 21**: 537 empleados
- **22 - 25**: 369 empleados

**`num_companies_worked`**
- **0 - 2**: 2601 empleados
- **3 - 5**: 1076 empleados
- **6 - 8**: 577 empleados
- **9**: 156 empleados

**`total_working_years`**
- **0 - 7**: 1565 empleados
- **17 - 30**: 817 empleados
- **31 - 40**: 138 empleados
- **8 - 16**: 1890 empleados

**years_with_curr_manager**
- **0 - 4**:      2769 empleados
- **13 - 17**:      99 empleados
- **5 - 8**:     1149 empleados
- **9 - 12**:      393 empleados
            
| No. | Variable                                    | Non-null Count | Dtype |
|-----|---------------------------------------------|----------------|-------|
| 1  | rango_num_companies_0_2                    | 4410           | int64 |
| 2  | rango_num_companies_3_5                    | 4410           | int64 |
| 3  | rango_num_companies_6_8                    | 4410           | int64 |
| 4  | rango_num_companies_9                      | 4410           | int64 |
| 5  | rango_experiencia_0_7                      | 4410           | int64 |
| 6  | rango_experiencia_17_30                    | 4410           | int64 |
| 7  | rango_experiencia_31_40                    | 4410           | int64 |
| 8  | rango_experiencia_8_16                     | 4410           | int64 |
| 9  | rango_age_18_25                           | 4410           | int64 |
| 10  | rango_age_26_35                           | 4410           | int64 |
| 11  | rango_age_36_48                           | 4410           | int64 |
| 12  | rango_age_49_60                           | 4410           | int64 |
| 13  | rango_ultimo_ascenso_0_3                   | 4410           | int64 |
| 14  | rango_ultimo_ascenso_12_15                 | 4410           | int64 |
| 15  | rango_ultimo_ascenso_4_7                   | 4410           | int64 |
| 16  | rango_ultimo_ascenso_8_11                  | 4410           | int64 |
| 17  | rango_mismo_jefe_0_4                       | 4410           | int64 |
| 18  | rango_mismo_jefe_13_17                     | 4410           | int64 |
| 19  | rango_mismo_jefe_5_8                       | 4410           | int64 |
| 20  | rango_mismo_jefe_9_12                      | 4410           | int64 |
| 21  | rango_años_en_la_empresa_0_3               | 4410           | int64 |
| 22  | rango_años_en_la_empresa_11_20             | 4410           | int64 |
| 23  | rango_años_en_la_empresa_20+               | 4410           | int64 |
| 24  | rango_años_en_la_empresa_4_10              | 4410           | int64 |
| 25  | rango_ingresos_10k_40k                    | 4410           | int64 |
| 26  | rango_ingresos_120k_200k                  | 4410           | int64 |
| 27  | rango_ingresos_40k_70k                    | 4410           | int64 |
| 28  | rango_ingresos_70k_120k                   | 4410           | int64 |
| 29  | rango_distancia_cerca                     | 4410           | int64 |
| 30  | rango_distancia_intermedio                | 4410           | int64 |
| 31  | rango_distancia_lejos                     | 4410           | int64 |
| 32  | rango_percent_salary_11_14                | 4410           | int64 |
| 33  | rango_percent_salary_15_18                | 4410           | int64 |
| 34  | rango_percent_salary_19_21                | 4410           | int64 |
| 35  | rango_percent_salary_22_25                | 4410           | int64 |

Se omitieron para el analisis las siguientes variables debido a su debil correlación con la varibale attrition la cual es la que intentaremos predecir en los modelos 
     
| No.| Variable                        | Punto-Biserial Correlation | 
|----|---------------------------------|----------------|
| 1  |job_level                        |-0.010290          |
| 2  | stock_option_level              |  -0.006839        | 
| 3  | years_since_last_promotion      | -0.033019         |




Con las variables listas empezaremos la [Técnicas de análisis](https://github.com/Maria-Data-Analyst/RRHH_Machine_Learning-/blob/main/Tecnica_analisis/machine_learning.md)

Para ver todo el procesamiento y gráficas puede consultar el siguiente [NoteBook](https://github.com/Maria-Data-Analyst/RRHH_Machine_Learning-/blob/main/procesamiento/procesamiento_rrhh.ipynb)


    
     
        
       
      

