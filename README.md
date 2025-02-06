# Análisis estadístico de la señal 
## Introducción

En el primer laboratorio de procesamiento de señales digitales se pretende caracterizar una señal biomédica a través de variables estadísticas. Para iniciar con el código, se seleccionó libremente de la plataforma PhysioNet, un estudio que contiene un conjunto de datos de acceso abierto de unos registros de (EMG), obtenidos de los músculos de la muñeca y el antebrazo durante la ejecución de diferentes movimientos; este estudio fue realizado para poder desarrollar aplicaciones en áreas como la biometría. Los datos fueron recopilados a partir de 43 individuos sanos con edades entre los 24 y 35 años, en tres días distintos. Cada participante realizó 16 gestos con las manos y los dedos en condiciones experimentales idénticas durante cada sesión.

Para llevar a cabo el análisis del laboratorio, se tomaron los datos correspondientes al primer sujeto del estudio. La señal seleccionada mostrada a continuación, fue procesada e ilustrada en Python. Cabe resaltar que tanto el desarrollo del código como la generación y visualización de las gráficas fueron compilados en Google Colab. 

Para la implementación del código, se usaron cinco librerías esenciales:

##### •	wfdb: Útil para trabajar con bases de datos de señales fisiológicas.
##### •	numpy: Una biblioteca fundamental para la computación matemática, que proporciona soporte para arreglos y matrices.
##### •	math: Útil para realizar una amplia variedad de operaciones matemáticas.
##### •	matplotlib.pyplot: Utilizada para crear gráficos y visualizaciones de datos.
##### •	scipy.stats: Parte del paquete SciPy, proporciona una amplia variedad de funciones y herramientas para realizar análisis estadísticos en Python.

## Análisis

<img src="https://github.com/user-attachments/assets/9ef60924-a6d6-4739-bba5-cc36425562c0" width="60%" />

>*Señal EMG.*

### Cálculo de estadísticos descriptivos.
Luego se procedió a calcular los estadísticos descriptivos de dos diferentes maneras: la primera fue usando los comandos y librerías que proporciona python, que en el código se estableció como el Cálculo 1, y la segunda fue usando fórmulas de manera manual, establecida igualmente como Cálculo 2, los parámetros evaluados se muestran a continuación:

• **Media:** Suma de un conjunto de números divididos por la cantidad de números que forman el conjunto.

• **Desviación estándar:** Medida de dispersión más común, que indica qué tan dispersos están los datos con respecto a la media.

• **Coeficiente de variación (CV):** Medida de dispersión que permite el análisis de las desviaciones de los datos con respecto a la media y al mismo tiempo las dispersiones que tienen los datos entre sí. 

![Captura](https://github.com/user-attachments/assets/8a2d2ff7-e1ce-4184-a1a8-e059dd84aa8c)
>*Datos calculados.*

• **Histograma:** Representación gráfica de cómo se distribuyen los datos.

<p float="left">
  <img src="https://github.com/user-attachments/assets/7d5c9cb5-1598-4960-a31c-0898c3d8b489" width="30%" style="vertical-align: middle;" />
  <img src="https://github.com/user-attachments/assets/e6a8006b-6c6d-46f9-8de9-312178fec9de" width="30%" style="vertical-align: middle;" />
</p>

>*Histograma de la señal.*

• **Función de probabilidad:** Devuelve la probabilidad de que una variable aleatoria sea exactamente igual a algún valor o tome un valor específico.


<p float="left">
  <img src="https://github.com/user-attachments/assets/63a0c9ed-cdb0-427e-9197-0fdb8ddfc305" width="30%" />
  <img src="https://github.com/user-attachments/assets/c0cd5d65-e0af-4224-a590-7b57b0c090a8" width="30%" />
</p>

>*Función de probabilidad con distribución simétrica.*

### Contaminación de la señal y SNR.

[^1^] Para esta parte del laboratorio, se debe contaminar la señal con tres tipos de ruido y hacer el cálculo del SNR (Signal-to-Noise Ratio) de cada uno, teniendo en cuenta que éste se define como la relación entre la potencia de la señal que se quiere recibir o procesar (la señal útil) y la potencia del ruido no deseado (el ruido que interfiere con esa señal).

[^1^]: MENDOZA REYES, Miguel A; LORENZO GINORI, Juan V  y  TABOADA CRISPI, Alberto. Clasificación de señales electrocardiográficas contaminadas con ruido mediante representaciones tiempofrecuencia. uct [online]. 2005, vol.9, n.35 [citado  2025-02-06], pp.125-131. Disponible en: <http://ve.scielo.org/scielo.php?script=sci_arttext&pid=S1316-48212005000300003&lng=es&nrm=iso>. ISSN 1316-4821.

En otras palabras, compara cuánta "información útil" (la señal) se tiene frente a cuánta "interferencia" (el ruido) está presente. El **Signal-to-Noise Ratio (SNR)** se mide en decibeles y se calcula usando la siguiente fórmula: [^2^]

[^2^]: Arnder LL, Shattuck MD, Black RD. Signal-to-noise ratio comparison between surface coils and implanted coils. Magn Reson Med. 1996 May;35(5):727-33. doi: 10.1002/mrm.1910350514. PMID: 8722824.

$$
SNR = 10 \times \log_{10} \left(\frac{P_{\text{señal}}}{P_{\text{ruido}}}\right)
$$

Un SNR más alto indica una mejor calidad de la señal, ya que significa que la potencia de la señal es mucho mayor que la del ruido.


![Captura14](https://github.com/user-attachments/assets/45896508-db5a-462e-8031-3aefc916e82f)

>*Cálculo de SNR para posterior análisis*

### Gráficas y análisis de la señal contaminada.

• **Ruido Gaussiano:**  Es un tipo de interferencia que sigue una distribución estadística normal. Se caracteriza por su forma de curva simétrica en torno a la media, similar a una campana. Al analizar las gráficas adjuntas, se observa cómo el ruido se superpone a la señal original y, en un segundo caso, cómo el ruido amplificado domina completamente a la señal.

<p float="left">
  <img src="https://github.com/user-attachments/assets/bdb29faf-ec3c-4555-a47b-817e3d276ed8" width="30%" />
  <img src="https://github.com/user-attachments/assets/c0ea8bbc-a2a4-4273-befc-93f15b165ff3" width="30%" />
</p>

>*Señal contaminada con ruido Gaussiano*

A partir de estos ejemplos, se calcula la relación entre la señal y el ruido (SNR). En el primer caso, un SNR positivo el cual tiene un valor de 7.4328 dB indica que la señal es claramente perceptible, aunque el ruido gaussiano afecta su calidad. Por otro lado, un SNR negativo el cual tiene un valor de -26.8917 dB en el segundo caso revela que la señal está extremadamente degradada por el ruido gaussiano, siendo apenas distinguible entre la interferencia.

• **Ruido de Impulso:** Es un tipo de perturbación que se caracteriza por la aparición repentina de eventos de alta energía que se superponen a la señal original.

<p float="left">
  <img src="https://github.com/user-attachments/assets/5d9e81a4-3c1f-4e43-98ad-5fcf6aa32c6a" width="30%" style="vertical-align: middle;" />
  <img src="https://github.com/user-attachments/assets/daba41d3-cb84-43d8-bc6b-fcb6845f74e1" width="30%" style="vertical-align: middle;" />
</p>

>*Señal contaminada con ruido de impulso*

Al analizar la relación señal-ruido (SNR), se observa que el valor positivo de sobresalto (27.734 dB) es significativamente mayor que el valor negativo (16.038 dB). Esto indica que las interferencias positivas tienen un menor impacto en la señal en condiciones favorables, aunque todavía alteran la señal. En cambio, las interferencias negativas tienden a causar una mayor distorsión en la señal original, afectando más su calidad.

• **Ruido de Artefacto:** El ruido de artefacto se refiere a alteraciones indeseadas en los datos que pueden ser causadas por fallas en el equipo de medición o interferencias electromagnéticas.
<p float="left">
  <img src="https://github.com/user-attachments/assets/2b9cf546-f2ca-475b-b172-4effc4de963b" width="30%" />
  <img src="https://github.com/user-attachments/assets/2d38b045-350d-467a-b16b-5745774d93cd" width="30%" />
</p>

>*Señal contaminada con ruido de Artefacto*

En la primera representación gráfica, se observa la interferencia de origen instrumental, que presenta una relación señal-ruido (SNR) positiva de aproximadamente 19.769 dB. Esto indica que la interferencia tiene un impacto mínimo en la señal, lo que permite que esta se mantenga nítida y clara en comparación con el ruido. Sin embargo, en la segunda representación gráfica, la interferencia se vuelve más intensa que la señal original, con una SNR de -5.905 dB. Este valor negativo sugiere que la interferencia es tan fuerte que distorsiona significativamente la señal, dificultando su reconocimiento y mostrando una calidad mucho más baja que en la primera gráfica.

## Instrucciones

**1. Extracción de datos:**

• Se extrajeron dos conjuntos de datos desde la unidad: .dat y .hea
•Los datos fueron descargados de la fuente original (Physionet) y transferidos a Google Colab.

**2. Proceso de análisis:**

• La señal se descargó y se llevó a Colab para su procesamiento.
• Todo el análisis se realizó mediante código, lo que permitió evaluar los datos de manera precisa.

***Nota importante: Cada vez que abras el archivo en Google Colab, será necesario cargar nuevamente el archivo de datos. Una vez cargado, podrás acceder al análisis estadístico realizado de dos maneras diferentes, según lo detallado en el código.***


**3. Parámetros clave:**

• Se utilizó la fórmula del SNR (Signal-to-Noise Ratio), que es un parámetro esencial en este análisis.

**4. Herramientas y librerías necesarias:**

• Se usó Python y un compilador (en este caso, Google Colab).

## Requisitos

• Tener Python 3.9 instalado y utilizar Google Colab (o cualquier compilador compatible).
• Tener acceso a los archivos .dat y .hea para cargar en Google Colab o el compilador elegido.
• Contar con las librerías necesarias instaladas para ejecutar el código correctamente (especificadas en el inicio del artículo).

## Usar

Por favor, cite este artículo:

Huertas, V.; Ramírez, P.; Delgado, A. Análisis estadístico de la señal. 6 de febrero de 2025.

## Información de contacto

• est.laurav.huertas@unimilitar.edu.co
• est.deisy.aramirez@unimilitar.edu.co
• est.paulav.gomez@unimilitar.edu.co

