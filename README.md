# Laboratorio-Procesamiento_1

## Objetivo de la practica 
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

**Comparacion entre los datos estadisticos**

| Parámetro              | PARTE A | PARTE B | Comparación                      
| ---------------------- | ------- | ------- | --------------------------------
| **Media**              | -0.3063 | 0.8805  | D1 centrado en valores negativos; D2 en valores positivos|
| **Desviación estándar**| 0.1932  | 0.4758  | D2 tiene mayor dispersión absoluta|
| **Coef. de variación**|63.08% | 54.04% | D1 presenta mayor variabilidad relativa|
| **Asimetría**          | Negativa| Positiva| D1 cola hacia la izquierda; D2 hacia la derecha|
| **Curtosis**           | 28.41   | 9.78   | D1 tiene más valores extremos que D2 



