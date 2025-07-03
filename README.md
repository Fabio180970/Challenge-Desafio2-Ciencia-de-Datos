# Challenge-Desafio2-Ciencia-de-Datos
Detectar las causas, patrones y factores asociados a la cancelacion del servicio por parte de los clientes 
📋 Informe Final
Análisis de Evasión de Clientes – Alura Telecom
🎯 Objetivo del Análisis:
El propósito de este proyecto fue identificar patrones y factores asociados a la cancelación del servicio por parte de los clientes, utilizando un enfoque exploratorio y visual apoyado en técnicas de análisis de datos con Python, Pandas, Seaborn y Plotly.

El objetivo principal de este análisis fue identificar los factores más relevantes que explican la evasión de clientes en una empresa de telecomunicaciones. A partir de datos reales de comportamiento y facturación.

🗂️ 2. Extracción y estructuración de datos
✅ Extraccion del archivo
De acuerdo a la informacion suministrada por el cliente se utilizó un archivo en formato .json, que contenía (7.267)datos información anidada sobre cada cliente, organizada en (6) columnas:

Cancelacion (Churn)
Información personal (customer)
Datos telefónicos (phone)
Datos de internet (internet)
Información de facturación (account)
✅ Proceso de transformación
Inicialmente con los datos suministrados se crea un DataFrame de Pandas Datos_clientes() para facilitar su manipulación y exploracion.

Se utiliza pandas.json_normalize() con el fin de desanidar los campos y convertirlos en un DataFrame plano.

Una vez desanidada la informacion se procede a revisarla y evaluar con type() con el fin de detectar posibles categorias mal tipadas, columnas con valores nulos y columnas con valores unicos.

Se eliminaron (22) filas duplicadas y se elimino la columna (Customer ID) ya que esta columna no afectaba el analisis.

🧹 3. Limpieza y transformación de datos
✔️ Conversión de variables:
Se mapearon columnas categóricas binarias (Yes/No, Male/Female) a valores binarios (1 y 0).

Se aplicó get_dummies() para variables con múltiples categorías (como InternetService, PaymentMethod, etc.).

Se renombraron algunas columnas a nombres más comprensibles en español (ej. tenure → Meses_Conectado, Charges.Monthly → Cargos_Mensuales).

Se creó una nueva columna: Cargos_Diarios, calculada a partir de los cargos mensuales (Cargos_Mensuales / 30), para tener una visión más granular del gasto diario por cliente.

📊 4. Análisis exploratorio de cancelación (Churn)
📌 Analisis Descriptivo Calculando Metricas
Se realiza, un análisis descriptivo de los datos, calculando métricas como media, mediana, desviación estándar y otras medidas que ayuden a comprender mejor la distribución y el comportamiento de los clientes.
✅ 1. Cancelación (Churn) Media = 0.2649, lo que indica que el 26.5% de los clientes han cancelado. Moda = 0, es decir, la mayoría no canceló.

📌 Conclusión: Aunque la mayoría de clientes permanece, más de 1 de cada 4 se va, lo que es significativo y requiere acciones de retención.

✅ 2. Meses_Conectado (Tenure) Media = 32.49 meses, mediana = 29, máximo = 72. Moda = 1: muchos clientes llevan muy poco tiempo. Rango = 71 meses (gran dispersión).

📌 Conclusión: Hay una alta variabilidad en la antigüedad de los clientes. Muchos clientes se van en los primeros meses (confirmado por la moda en 1), lo que sugiere que el onboarding y la experiencia inicial son críticos para la retención.

✅ 3. Cargos_Mensuales (Monthly Charges) Media = 64.84, mediana = 70.35, pero la moda = 20.05. Máximo = 118.75, lo que sugiere servicios premium. Alta desviación estándar = 30.1, lo que indica variabilidad fuerte.

📌 Conclusión: Aunque muchos clientes pagan montos altos, existe un grupo grande que paga poco (20.05). Los clientes que pagan más podrían ser más exigentes y más propensos a cancelar si no se cumple su expectativa.

✅ 4. Cargos_Totales (Total Charges) Media = 2.287 USD, pero la mediana = 1.397 USD y la moda = 19.75 USD (muy baja). Desviación estándar = 2268, máximo = 8684.

Clientes con bajo gasto total → podrían ser los que se dan de baja rápido.

📌 Conclusión: Clientes con bajo gasto total tienden a cancelar antes. El valor de vida del cliente (CLTV) es bajo en un grupo importante, lo que representa una oportunidad para trabajar retención desde el primer mes.

📌 Calculo de Frecuencia de Categorias Nuemericas
📊 Frecuencia en 'OnlineSecurity': OnlineSecurity No 3599 Yes 2074 No internet service 1561 Name: count, dtype: int64

📊 Frecuencia en 'OnlineBackup': OnlineBackup No 3173 Yes 2500 No internet service 1561 Name: count, dtype: int64

📊 Frecuencia en 'DeviceProtection': DeviceProtection No 3186 Yes 2487 No internet service 1561 Name: count, dtype: int64

📊 Frecuencia en 'TechSupport': TechSupport No 3573 Yes 2100 No internet service 1561 Name: count, dtype: int64

📊 Frecuencia en 'StreamingTV': StreamingTV No 2887 Yes 2786 No internet service 1561 Name: count, dtype: int64

📊 Frecuencia en 'StreamingMovies': StreamingMovies No 2858 Yes 2815 No internet service 1561 Name: count, dtype: int64

📊 Frecuencia en 'Contract': Contract Month-to-month 3983 Two year 1733 One year 1518 Name: count, dtype: int64

📊 Frecuencia en 'PaymentMethod': PaymentMethod Electronic check 2439 Mailed check 1641 Bank transfer (automatic) 1587 Credit card (automatic) 1567 Name: count, dtype: int64

📌 Matriz de Correlacion Entre Variables Numericas
Se graficó una matriz de correlacion entre variables numericas que indica el comportamiento general.

📌 Distribución general de cancelación
Se identificó que aproximadamente el 26.6% de los clientes cancelaron el servicio.

Esto se visualizó con gráficos de barras y circulares (Seaborn y Plotly), mostrando un equilibrio visual entre evasión y permanencia.

📈 5. Variables categóricas relacionadas con la evasión
Se evaluó la tasa de cancelación promedio por categoría, y se identificaron los factores más influyentes:

Variable Categoría con mayor tasa de cancelación
Tasa de cancelación

Contract Month-to-month 42.6%
InternetService Fiber optic 41.8%
PaymentMethod Electronic check 45.1%
TechSupport No 41.5%
OnlineSecurity No 41.6%
🎯 Interpretación clave:
Contratos mensuales y servicios costosos sin soporte o seguridad online aumentan la probabilidad de evasión.
Los métodos de pago automáticos (como tarjeta de crédito) están asociados a menor evasión.
📊 6. Variables numéricas vs cancelación
Variables analizadas:

Meses_Conectado
Cargos_Mensuales
Cargos_Totales
Hallazgos:

Clientes que cancelan tienen significativamente menos tiempo con la empresa.
Los que cancelan también han gastado menos en total, indicando falta de fidelización.
Algunos que pagan más por mes tienen una mayor tasa de cancelación, lo que podría sugerir insatisfacción con el valor percibido.
Gráficos interactivos (Plotly) con histogramas y boxplots ayudaron a visualizar claramente estas diferencias.
📌 7. Conclusiones y recomendaciones
🧠 Insights principales:
La flexibilidad del contrato mensual aumenta la probabilidad de cancelación.
Falta de soporte técnico o seguridad online está altamente correlacionada con la evasión.
Clientes nuevos y con menor gasto acumulado tienen más probabilidad de cancelar.
El método de pago electrónico manual (cheque) es el más riesgoso en términos de permanencia.
✅ Recomendaciones estratégicas:
Incentivar contratos anuales: descuentos o beneficios para contratos más largos.
Agregar servicios de valor (seguridad, soporte) sin costo a clientes en riesgo.
Migrar clientes a métodos de pago automáticos.
Diseñar campañas de retención para nuevos clientes en los primeros 3 meses.
Principales Causas de Cancelacion de Clientes
Estas causas son basadas en la interaccion del trabajo realizado:

🗓️ Tipo de contrato mensual (Month-to-month) Tasa de cancelación: 42.6%. Es el doble o más alta que la de contratos de un año (11.2%) o dos años (2.8%).
📌 Por qué importa:

La falta de compromiso a largo plazo facilita la salida.
Clientes en este modelo tienen menos barreras para cancelar en cualquier momento.
📉 Tiempo de conexión bajo (tenure). La moda de Meses_Conectado es 1 mes → muchos cancelan en el primer mes.
Clientes nuevos son altamente volátiles.
📌 Interpretación:

Hay problemas con la experiencia inicial del cliente.
El servicio no logra fidelizar rápidamente.
❌ Ausencia de servicios complementarios.
Sin soporte técnico: la Cancelacion sera del 41.5%
Sin seguridad online: la Cancelacion sera del 41.6%
📌 Por qué importa:

Clientes sin valor agregado no perciben diferenciación.
Esto genera falta de lealtad y más cancelaciones ante cualquier problema.
💳 Método de pago (cheque electrónico)
Clientes que pagan manualmente tienen una de las tasas más altas de cancelación (45.1%).
Refleja perfiles menos digitalizados o con menor compromiso financiero.
🎯 Conclusión general La principal causa de cancelación de clientes es una combinación de baja fidelización temprana, contratos altamente flexibles, y falta de servicios de valor añadido.

🧠 Recomendación 👉 Para reducir la cancelación, la empresa debe:

Incentivar contratos de mayor duración con beneficios tangibles.
Mejorar la experiencia del cliente en los primeros 2 meses.
Incluir soporte técnico y seguridad como parte de los planes básicos.
Fomentar métodos de pago automáticos y evitar el cheque manual.
