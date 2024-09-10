# Procesamiento y Preparación de la Base de Datos

En esta sección, nos familiarizaremos con las  variables disponibles para entender con qué datos contamos.

## Descripción de Variables

A continuación se detalla la información contenida en la tabla:

| **Variable**               | **Descripción**                                                                                   |
|----------------------------|---------------------------------------------------------------------------------------------------|
| Age                        | Edad del empleado                                                                                 |
| Attrition                  | Empleado que abandona la empresa (0 = no, 1 = sí)                                                  |
| BusinessTravel             | Indica la frecuencia con la que el empleado viaja                                                  |
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

