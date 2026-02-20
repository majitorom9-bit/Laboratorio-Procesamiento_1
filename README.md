# Laboratorio-Procesamiento_1

## Objetivo de la práctica
Analizar estadísticamente una señal fisiológica, calcular sus principales parámetros descriptivos, y comparar los resultados entre señales capturadas con hardware, aplicando también el concepto de relación señal-ruido.

## Procedimiento 
### PARTE A 
1. **Obtener la señal**
Se ingreso a la base de datos physionet y se descargo una señal fisiologica ECG, se utilizo la señal del registro: https://physionet.org/content/pwave/1.0.0/#files-panel el cual contiene registros de electrocardiograma (ECG) provenientes de la "MIT-BIH Arrhythmia Database". Este conjunto se caracteriza por incluir anotaciones detalladas de la onda P, que representa la despolarización auricular, lo que permite un análisis más preciso de la actividad eléctrica del corazón y facilita el estudio de alteraciones del ritmo cardíaco. Finalmente se graficó la señal en el dominio del tiempo.

**Gráfico de la señal descargada**

<img width="884" height="386" alt="image" src="https://github.com/user-attachments/assets/96484553-f12d-457f-94bc-e6902dffa283" />


2. **Cálculos estadísticos descriptivos**
Se calcularon los datos estadisticos de dos maneras diferentes, la primera vez que se dessarrolló programando las formulas  haciendo uso de las funciones predefinidas con python y la segunda vez programando las funciones desde cero.

**PARTE 1**

   Para la elaboración de esta primera parte se hizo uso de las funciones predeterminadas de python para estadisticos y el código utilizado fue:

   
   ```python
print(f"Datos con funciones")

#media
media=np.mean(ecg_1)
print (f"Media: {media} ")

#mediana
mediana=np.median(ecg_1)
print (f"Mediana: {mediana} ")

#desviación estandar
desviacion_muestra=np.std(ecg_1, ddof=1)
print (f"Desviacion estandar: {desviacion_muestra} ")

# asimetría (skewness)
asimetria = skew(ecg_1, bias=False)
print(f"Asimetria (skewness): {asimetria}")

#coeficiente de variacion
coef_var = (desviacion_muestra / abs(media)) * 100
print(f"Coeficiente de variacion: {coef_var:.2f}%") 

#curtosis
n=len(ecg_1)
curtosis=np.sum(((ecg_1-media)/desviacion_muestra)**4)/n
print(f"Curtosis: {curtosis}")
   ```
Dandonos como resultados los siguientes valores para cada estadístico calculado:


- Media: -0.3062989769230769 
- Mediana: -0.335 
- Desviacion estandar: 0.19319969075242077 
- Asimetria (skewness): 4.4261478025110375
- Coeficiente de variacion: 63.08%
- Curtosis: 28.413018422958583

Y también se graficó su histograma que se muestra a continuación:

<img width="570" height="425" alt="image" src="https://github.com/user-attachments/assets/c782b76f-2f18-4148-8859-a82a704da931" />


   
**PARTE 2**


Ahora bien, para estos cálculos se realizó la elaboración de los estadísticos desde cero y se utilizó el siguiente código:
 ```python
print("Datos sin funciones")

n = len(ecg_1)


# MEDIA

suma = 0
for valor in ecg_1:
    suma += valor

media = suma / n
print(f"Media: {media}")


# MEDIANA

datos_ordenados = sorted(ecg_1)

if n % 2 == 0:
    mediana = (datos_ordenados[n//2 - 1] + datos_ordenados[n//2]) / 2
else:
    mediana = datos_ordenados[n//2]

print(f"Mediana: {mediana}")


# DESVIACIÓN ESTÁNDAR

suma_cuadrados = 0
for valor in ecg_1:
    suma_cuadrados += (valor - media) ** 2

varianza = suma_cuadrados / (n - 1)
desviacion = varianza ** 0.5

print(f"Desviacion estandar: {desviacion}")

# ASIMETRÍA (SKEWNESS)
suma_cubo = 0
for valor in ecg_1:
    suma_cubo += ((valor - media) / desviacion) ** 3

asimetria = (n / ((n - 1) * (n - 2))) * suma_cubo

print(f"Asimetria: {asimetria}")

# COEFICIENTE DE VARIACIÓN

coef_variacion = (desviacion / abs(media)) * 100
print(f"Coeficiente de variacion: {coef_variacion:.2f}%")


# CURTOSIS

suma_cuarta = 0
for valor in ecg_1:
    suma_cuarta += (valor - media) ** 4

curtosis = (suma_cuarta / n) / (varianza ** 2)

print(f"Curtosis: {curtosis}")

 ```
Finalmente los resultados obtenidos fueron: 

- Media: -0.30629897692306546
- Mediana: -0.335
- Desviacion estandar: 0.1931996907525729
- Asimetria: 4.426147802499588
- Coeficiente de variacion: 63.08%
- Curtosis: 28.413018422874092
   
3. **Diagrama de flujo parte A**
   
   ![DIAGRAMA 1](https://github.com/user-attachments/assets/a5d50f62-9afa-4b1f-afad-5badc50feef4)

   
### PARTE B
1. **Generacion de una señal** 
Se generó una señal Electrocardiográfica (ECG), utilizando el  generador de señales biologicas.
2. **Captura de la señal**
Se capturo la señal utilizando el microcontrolador STM32 Black Pill, usando su módulo ADC, para lograr convertir la señal análoga en  digital que luego se importo a Python mediante el puerto serial, donde luego los valores fueron convertidos a voltaje para que pudieran ser graficados por medio de una interfaz gráfica en tiempo real mediante matplotlib y  finalmente se guardaron  en un archivo CSV para su posterior análisis.

**Gráfico de la señal capturada**

<img width="432" height="341" alt="REGISTRO 2" src="https://github.com/user-attachments/assets/ed557871-705f-4540-aae1-da917e3de724" />


4. **Calculos estadisticos**
Se repitieron los cálculos de la parte A y los resultados para esta señal fueron:
-Media: 0.8804996336996334
-Mediana: 0.8356776556776556
-Desviacion estandar: 0.47581916796037166
-Asimetria: 1.9102376871657396
-Coeficiente de variacion: 54.04%
-Curtosis: 9.784939579218957
 - Histograma obtenido:

 <img width="826" height="597" alt="image" src="https://github.com/user-attachments/assets/657ecce0-629a-4833-9be9-9d6270f4d392" />

                     
4. **Diagrama de Flujo parte B**

![DIAGRAMA 2](https://github.com/user-attachments/assets/6f98a869-dc68-4e3e-9e9b-35ce3ea394c7)

### PARTE C
1.**Relacion Señal Ruido**

La señal fue contaminada con programación en python donde se implementaron funciones para  añadir los tres diferentes tipos de ruido.
- Gaussiano: Para simular el ruido aleatorio común
- Por impulso: Representando picos repentinos de alta amplitud
- Tipo artefacto: Emulando distorsiones producidas por interferencias externas

  El resultado de las gráficas con respecto a los ruidos fue:

  <img width="1178" height="562" alt="image" src="https://github.com/user-attachments/assets/e3069f5d-c2f4-4e88-ae1f-38d88d6af0e6" />

2. **Calculos del SNR**
  SNR: Signal-to-Noise Ratio o relación señal-ruido es una medida que indica qué tan fuerte es una señal útil en comparación con el ruido que la afecta, se calcula como el cociente entre la potencia de la señal y la potencia del ruido, y normalmente se expresa en decibeles (dB). Un SNR alto significa que la señal es clara y tiene poca interferencia, mientras que un SNR bajo indica que el ruido está afectando significativamente la calidad de la señal.
Se calculo la relacion señal ruido para cada caso de contaminacion con los ruidos antes mencionados
  - SNR Ruido Gaussiano: 8.39 dB
  - SNR Ruido Impulso: 2.49 dB
  - SNR Ruido Tipo Artefacto: 0.57 dB
    
Código utilizado para el cálculo de los SNR:

 ```python

import numpy as np

print("SNR (sin componente DC)")


# RMS quitando el promedio

def rms_ac(x):
    x = np.asarray(x, dtype=float)
    x = x - np.mean(x)   # quitar componente DC
    return np.sqrt(np.mean(x**2))


# SNR en dB

def snr_db_from_pair(y_clean, y_noisy):
    y_clean = np.asarray(y_clean, dtype=float)
    y_noisy = np.asarray(y_noisy, dtype=float)

    ruido = y_noisy - y_clean

    rc = rms_ac(y_clean)
    rr = rms_ac(ruido)

    if rr == 0:
        return np.inf

    return 20 * np.log10(rc / rr)


# Cálculo SNR

snr_gauss   = snr_db_from_pair(adc_v, G_v)
snr_art     = snr_db_from_pair(adc_v, A_v)
snr_impulso = snr_db_from_pair(adc_v, I_v)

print(f"SNR Ruido Gaussiano: {snr_gauss:.2f} dB")
print(f"SNR Ruido tipo artefacto: {snr_art:.2f} dB")
print(f"SNR Ruido de impulso: {snr_impulso:.2f} dB")

 ```


3. **Diagramas de flujo**

   ![DIAGRAMA 3](https://github.com/user-attachments/assets/fe6979c8-5176-42cc-820e-dbb16568b354)

## Resultados 

**Comparacion entre la parte A y la parte B**

Se compararon los resultados obtenidos en la Parte A y la Parte B en la cual se evidenciaron diferencias importantes en los parámetros estadísticos calculados, lo que permite analizar el comportamiento de una señal descargada de una base de datos frente a una señal generada y capturada mediante hardware.
En primer lugar, **la media de la señal** en la Parte A fue de -0.3063, mientras que en la Parte B fue de 0.8805. Esta diferencia indico que las señales no estaban centradas en el mismo nivel de referencia. En la señal capturada se observo un valor promedio positivo mayor, ya que el equipo con el que se midió la señal agregó un pequeño desplazamiento en el valor promedio, en cambio, la señal descargada ya había sido ajustada o filtrada antes de publicarse.
Respecto a la **desviación estándar**, la Parte A presentó un valor de 0.1932, mientras que la Parte B obtuvo 0.4758. Esto indica que la señal capturada presenta mayor variabilidad en amplitud. Esta diferencia puede deberse al ruido electrónico, interferencias externas o limitaciones propias del sistema de adquisición utilizado.
**El coeficiente de variación** fue de 63.08 % en la Parte A y 54.04 % en la Parte B. Aunque la señal de la Parte B tiene mayor desviación estándar, su coeficiente de variación es menor debido a que su media es mayor. Esto indica que, la señal capturada cambia un poco menos si la comparamos con su propio valor promedio. Es decir, en proporción, es un poco más estable.
En cuanto a **la asimetría**, ambas señales presentan valores positivos (4.43 en la Parte A y 1.91 en la Parte B), lo cual es coherente con la naturaleza del ECG, que contiene picos R de alta amplitud. Sin embargo, la señal descargada muestra una asimetría considerablemente mayor, lo que indica una distribución más inclinada hacia valores altos y una presencia más marcada de valores extremos.
Finalmente, **la curtosis** fue de 28.41 en la Parte A y 9.78 en la Parte B. Ambos valores indican distribuciones leptocúrticas, es decir, con picos pronunciados. No obstante, la señal de la Parte A presenta una curtosis mucho más elevada, lo que sugiere picos más definidos y marcados. Esto puede deberse a que la señal proveniente de la base de datos conserva características fisiológicas más complejas y mejor definidas que la señal generada artificialmente.

**Analisis de la Parte C**

En la Parte C se evaluó la calidad de la señal capturada en la Parte B mediante el cálculo de la relación señal-ruido (SNR), luego de contaminarla con tres tipos diferentes de ruido: gaussiano, por impulso y tipo artefacto. El SNR permite cuantificar qué tan dominante es la señal útil frente al ruido que la afecta; valores altos indican mejor calidad de señal, mientras que valores bajos reflejan una mayor degradación.

Para el caso del ruido gaussiano se obtuvo un SNR de 8.39 dB. Este valor indica que la potencia de la señal aún es mayor que la del ruido, por lo que, aunque existe contaminación, la morfología general del ECG puede distinguirse. El ruido gaussiano introduce variaciones aleatorias distribuidas de manera uniforme, afectando la amplitud pero sin generar distorsiones significativas.

En el caso del ruido por impulso, el SNR fue de 2.49 dB, lo que representa una degradación considerablemente mayor. Este tipo de ruido genera picos repentinos de alta amplitud que alteran de forma significativa la señal original, pudiendo confundirse con eventos fisiológicos reales como los complejos QRS. Por esta razón, el ruido impulsivo afecta de manera más crítica la interpretación clínica y el análisis automático.

Finalmente, al contaminar la señal con ruido tipo artefacto se obtuvo un SNR de 0.57 dB, siendo el valor más bajo de los tres casos. Un SNR cercano a 0 dB indica que la potencia del ruido es prácticamente equivalente a la potencia de la señal útil, lo que implica una fuerte distorsión y una pérdida considerable de información fisiológica. Este tipo de ruido simula interferencias externas o movimientos del paciente, los cuales son comunes en señales biomédicas reales y representan uno de los mayores desafíos en su procesamiento.

En conclusión, los resultados demuestran que el tipo de ruido influye directamente en la calidad de la señal y en el valor del SNR obtenido. El ruido gaussiano es el menos perjudicial en este caso, mientras que el ruido tipo artefacto genera la mayor degradación. Esto evidencia la importancia de aplicar técnicas de filtrado y acondicionamiento antes de realizar análisis clínicos o diagnósticos, ya que una baja relación señal-ruido puede comprometer la confiabilidad de los resultados.


## Analisis General

En el desarrollo de esta práctica se logró caracterizar estadísticamente una señal biomédica tipo ECG, cumpliendo con el objetivo de analizar sus principales parámetros descriptivos y comparar señales provenientes de distintas fuentes. A lo largo del laboratorio se evidenció cómo las magnitudes estadísticas permiten describir el comportamiento global de una señal sin necesidad de analizar detalladamente cada uno de sus componentes morfológicos.

En la Parte A, el análisis de una señal descargada de una base de datos clínica permitió identificar valores elevados de asimetría y curtosis, lo que refleja la presencia de picos pronunciados característicos del complejo QRS del ECG. Además, se comprobó que los resultados obtenidos mediante la programación manual de las fórmulas coincidieron con los calculados usando funciones predefinidas, validando la correcta implementación de los algoritmos.

En la Parte B, al generar y capturar una señal utilizando hardware, se evidenciaron diferencias en la media, dispersión y forma de la distribución. Esto permitió comprender que los sistemas de adquisición pueden introducir offset, mayor variabilidad y ruido adicional. La comparación demostró que una señal experimental puede diferir de una señal clínica real debido a factores técnicos y condiciones del entorno.

En la Parte C, el análisis de la relación señal-ruido (SNR) confirmó que el tipo de ruido influye directamente en la calidad de la señal. El ruido tipo artefacto produjo la mayor degradación, mientras que el ruido gaussiano tuvo un impacto menor. Esto evidenció la importancia del filtrado y acondicionamiento para garantizar análisis confiables.

En cuanto al alcance de los parámetros estadísticos para detectar patologías, estos permiten identificar cambios globales en la señal, como aumentos en la variabilidad, alteraciones en la dispersión o presencia de valores extremos que podrían estar asociados a ciertas condiciones fisiológicas. Son útiles como herramientas de apoyo en sistemas automáticos de clasificación y monitoreo, ya que resumen información relevante de forma cuantificable.

Sin embargo, presentan limitaciones importantes. Los parámetros estadísticos no analizan directamente la morfología específica de las ondas (P, QRS, T), por lo que no permiten diagnosticar una patología de manera concluyente. Dos señales con diferentes alteraciones clínicas podrían presentar valores estadísticos similares, lo que limita su capacidad diagnóstica cuando se utilizan de forma aislada.

Respecto a la evaluación de la calidad de una señal biomédica, los parámetros estadísticos y el SNR permiten detectar presencia de ruido, variabilidad excesiva o distorsiones. Son herramientas eficaces para cuantificar el nivel de contaminación y decidir si la señal es adecuada para análisis posteriores. No obstante, también tienen limitaciones, ya que no siempre distinguen entre cambios fisiológicos reales y artefactos, especialmente cuando ambos afectan de manera similar la distribución de los datos.

En conjunto, el laboratorio permitió comprender que los parámetros estadísticos son herramientas fundamentales para la caracterización y evaluación inicial de señales biomédicas. Sin embargo, para aplicaciones clínicas más precisas y detección confiable de patologías, deben complementarse con análisis morfológicos, espectrales y técnicas avanzadas de procesamiento digital de señales.

## Preguntas para la discusión

**¿Los valores estadísticos calculados sobre la señal sintética son exactamente iguales a los obtenidos a partir de la señal real? ¿Por qué?**

No, los valores no son exactamente iguales. Esto pasa porque la señal real viene de un registro clínico y tiene variaciones naturales del corazón que son más complejas. En cambio, la señal sintética es generada por un equipo y suele ser más “ideal” o simplificada.

Además, al capturar la señal pueden aparecer pequeños errores, ruido o desplazamientos en el valor promedio que cambian los resultados. Por eso, aunque ambas sean señales ECG, sus valores estadísticos no coinciden exactamente.

**¿Afecta el tipo de ruido el valor de la SNR calculado? ¿Cuáles podrían ser las razones?** 

Sí, el tipo de ruido afecta el valor de la SNR porque cada uno altera la señal de forma diferente.

El ruido gaussiano introduce pequeñas variaciones aleatorias, por eso la señal todavía se puede reconocer. El ruido por impulso agrega picos fuertes y repentinos que cambian bastante la señal. El ruido tipo artefacto produce distorsiones más grandes y constantes, afectando aún más su forma original.

Como la SNR compara qué tan fuerte es la señal frente al ruido, cuando el ruido es más intenso o distorsiona más, el valor de la SNR disminuye.

## Conclusiones

A partir del desarrollo de esta práctica se logró caracterizar una señal biomédica tipo ECG mediante parámetros estadísticos como la media, desviación estándar, coeficiente de variación, asimetría y curtosis. Estos indicadores permitieron describir el comportamiento general de la señal.

La comparación entre la señal descargada de una base de datos y la señal generada y capturada evidenció que los sistemas de adquisición pueden introducir variaciones y ruido adicional, lo que modifica los valores estadísticos obtenidos. Esto demuestra la importancia del acondicionamiento y procesamiento previo de las señales biomédicas.

Asimismo, el cálculo de la relación señal-ruido (SNR) permitió comprobar que la calidad de la señal depende directamente del tipo de ruido presente. Se observó que el ruido tipo artefacto generó la mayor degradación, mientras que el ruido gaussiano fue el menos perjudicial en comparación. 

Finalmente, se concluye que los parámetros estadísticos son herramientas fundamentales para la evaluación de señales biomédicas y pueden servir como apoyo en la detección de alteraciones fisiológicas. Sin embargo, para aplicaciones clínicas más precisas, deben complementarse con análisis morfológicos y técnicas avanzadas de procesamiento digital de señales.



