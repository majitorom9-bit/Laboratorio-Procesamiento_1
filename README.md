# Laboratorio-Procesamiento_1

## Objetivo de la practica 
Analizar estadísticamente una señal fisiológica, calcular sus principales parámetros descriptivos, y comparar los resultados entre señales capturadas con hardware, aplicando también el concepto de relación señal-ruido.

## Procedimiento 
Para el desarrollo de la práctica, se realizó la descarga de una señal fisiológica desde el sitio de physionet (https://physionet.org/content/pwave/1.0.0/100.dat) muestreadas a 360 Hz, con el objetivo de calcular los parámetros estadísticos que permiten describirla cuantitativamente, explicando la utilidad y el significado de cada uno de ellos dentro del análisis de las señales.
Las señales obtenidas en un entorno real, como es el caso de las señales biomédicas, se caracterizan por contener información relevante asociada a parámetros como la amplitud y la frecuencia. No obstante, también pueden incluir componentes no deseados que alteran su comportamiento, conocidos como ruido, los cuales pueden afectar la interpretación adecuada de la señal. 
### PARTE A 
1. **Obtener la señal**
Se ingreso a la base de datos physionet y se descargo una señal fisiologica ECG, se utilizo la señal del registro: https://physionet.org/content/pwave/1.0.0/#files-panel el cual contiene registros de electrocardiograma (ECG) provenientes de la "MIT-BIH Arrhythmia Database". Este conjunto se caracteriza por incluir anotaciones detalladas de la onda P, que representa la despolarización auricular, lo que permite un análisis más preciso de la actividad eléctrica del corazón y facilita el estudio de alteraciones del ritmo cardíaco. Finalmente se graficó la señal en el dominio del tiempo.

2. **Calculos estadisticos descriptivos**
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
Finalemnte los resultados obtenidos fueron: 

- Media: -0.30629897692306546
- Mediana: -0.335
- Desviacion estandar: 0.1931996907525729
- Asimetria: 4.426147802499588
- Coeficiente de variacion: 63.08%
- Curtosis: 28.413018422874092
   
3. **Diagrama de flujo**
   
   ![DIAGRAMA 1](https://github.com/user-attachments/assets/a5d50f62-9afa-4b1f-afad-5badc50feef4)

   
### PARTE B
1. **Generacion de una señal** 
Se genero una señal fisiologica ECG, similar a la utilizada por el generador de señales biologica.
2. **Captura de la señal**
Se capturo una señal utilizando la STM 32 Black Pill usando un modulo ADC, para lograr convertir la señal analoga en una señal digital, y luego se importo la señal a Python y la graficamos.
3. **Calculos estadisticos**
Se calcularon los datos estadisticos encontrados en la parte y A y se compararon entre ellos.
 - Media de la señal: 0.8804996336996337 
 - Desviacion estandar: 0.4758191679603716 
 - Coeficeinte de variacion: 54.04%
 - Asimetria (Skewness): Positiva
 - Curtosis: 9.784939579218962
 - Histograma

   <img width="432" height="335" alt="Histograma 2" src="https://github.com/user-attachments/assets/b303bf62-a2e3-473b-a829-0104b55ea7a7" />
                     
4. **Diagrama de Flujo**

![DIAGRAMA 2](https://github.com/user-attachments/assets/6f98a869-dc68-4e3e-9e9b-35ce3ea394c7)

### PARTE C
1.**Relacion Señal Ruido**
La señal fue contaminada con funciones diferentes añadiendo 3 distintos tipos de ruido.
- Ruido Gaussiano
- Ruido Impulso
- Ruido Tipo Artefacto
2. **Calculos del SNR**
Se calculo la relacion señal ruido para cada caso de contaminacion con lso ruidos antes mencionados
  - SNR Ruido Gaussiano: 8.39 dB
  - SNR Ruido Impulso: 2.49 dB
  - SNR Ruido Tipo Artefacto: 0.57 dB

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

## Graficas

**ECG DESCARGADO**

<img width="533" height="238" alt="REGISTRO 1" src="https://github.com/user-attachments/assets/ed2412df-e38a-48cf-98b6-9d69cdb2146f" />

**ECG CAPTURADO**

<img width="432" height="341" alt="REGISTRO 2" src="https://github.com/user-attachments/assets/ed557871-705f-4540-aae1-da917e3de724" />

**RUIDOS EN LA SEÑAL ECG**

<img width="537" height="271" alt="REGISTRO 3" src="https://github.com/user-attachments/assets/be3bea48-8241-4eda-89ce-95bbcbcdd120" />

