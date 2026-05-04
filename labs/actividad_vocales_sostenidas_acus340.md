# Actividad complementaria: adquisición y análisis de vocales sostenidas

## ACUS340 - Procesamiento de Señales

Esta actividad propone construir una pequeña base de datos acústica durante la clase, usando grabaciones de vocales sostenidas. El objetivo es aplicar las herramientas vistas en la Unidad 2: análisis temporal, DFT, PSD, estimación espectral y Cepstrum.

La actividad tiene fines exclusivamente docentes. No busca identificar personas ni realizar inferencias biométricas. Las grabaciones serán usadas sólo durante la clase para analizar propiedades generales de señales de voz.

---

## 1. Objetivo de la actividad

Construir una pequeña base de datos de vocales sostenidas y analizar sus características acústicas usando herramientas de procesamiento digital de señales.

Al finalizar la actividad, las y los estudiantes deberían ser capaces de:

- Grabar señales de voz siguiendo un protocolo simple.
- Organizar archivos de audio de manera reproducible.
- Visualizar la forma de onda de una vocal sostenida.
- Calcular la DFT de una señal de voz.
- Estimar la PSD usando el método de Welch.
- Observar estructura armónica en señales de voz.
- Calcular e interpretar el Cepstrum de manera exploratoria.
- Comparar vocales y registros vocales desde una perspectiva acústica.

---

## 2. Contexto conceptual

Las vocales sostenidas son señales especialmente útiles para una clase de procesamiento de señales, porque suelen presentar una estructura relativamente estable durante algunos segundos.

En una vocal sostenida podemos observar:

- una señal periódica o cuasi-periódica en el tiempo,
- una frecuencia fundamental aproximada,
- una estructura armónica,
- diferencias espectrales entre vocales,
- regiones de mayor energía asociadas a la resonancia del tracto vocal.

En esta actividad no profundizaremos formalmente en fonética acústica, pero introduciremos una idea importante: las vocales no se diferencian sólo por la frecuencia fundamental, sino también por la forma del espectro.

---

## 3. Protocolo de grabación

### Organización

1. Formar grupos de 2 a 3 estudiantes.
2. Buscar personas voluntarias que acepten colaborar con la actividad.
3. Explicar brevemente el objetivo de la grabación.
4. Solicitar consentimiento verbal antes de grabar.
5. Grabar las cinco vocales: /a/, /e/, /i/, /o/, /u/.

### Mensaje sugerido para solicitar colaboración

> Estamos realizando una actividad docente de procesamiento de señales. Queremos grabar vocales sostenidas para analizarlas en frecuencia durante la clase. La grabación será usada sólo con fines educativos y no será publicada. ¿Nos podría ayudar pronunciando las vocales /a/, /e/, /i/, /o/, /u/ durante unos segundos cada una?

### Condiciones recomendadas

- Grabar en un lugar relativamente silencioso.
- Mantener el celular o grabadora a unos 20–30 cm de la boca.
- Evitar mover el dispositivo durante la grabación.
- Pedir que cada vocal sea pronunciada de forma clara y sostenida.
- Cada vocal debería durar entre 2 y 3 segundos.
- Evitar gritos o niveles excesivos que puedan saturar la grabación.

---

## 4. Registro de voces

Para evitar clasificaciones personales rígidas, se recomienda describir las voces desde una perspectiva acústica, por ejemplo:

- registro grave,
- registro medio,
- registro agudo.

También se puede usar una identificación anónima:

- voice01,
- voice02,
- voice03.

No es necesario registrar nombres, edad, género ni información personal de las personas voluntarias.

---

## 5. Nombres de archivo recomendados

Para facilitar el análisis posterior, cada archivo debe tener un nombre ordenado.

Ejemplo simple:

```text
group01_voice01_a.wav
group01_voice01_e.wav
group01_voice01_i.wav
group01_voice01_o.wav
group01_voice01_u.wav
```

Si el grupo graba más de una voz:

```text
group01_voice01_a.wav
group01_voice01_e.wav
group01_voice01_i.wav
group01_voice01_o.wav
group01_voice01_u.wav

group01_voice02_a.wav
group01_voice02_e.wav
group01_voice02_i.wav
group01_voice02_o.wav
group01_voice02_u.wav
```

---

## 6. Estructura sugerida de carpetas

Dentro del proyecto del curso, se recomienda crear una carpeta local para estas grabaciones:

```text
data/
└── class_voice_vowels/
    ├── group01/
    │   ├── group01_voice01_a.wav
    │   ├── group01_voice01_e.wav
    │   ├── group01_voice01_i.wav
    │   ├── group01_voice01_o.wav
    │   └── group01_voice01_u.wav
    ├── group02/
    │   ├── group02_voice01_a.wav
    │   └── ...
    └── group03/
        └── ...
```

La carpeta `data/` no debe subirse a GitHub si contiene audios pesados o grabaciones tomadas durante la clase.

---

## 7. Análisis propuesto

Al regresar a la sala, cada grupo deberá seleccionar al menos una voz y analizar sus cinco vocales.

Para cada vocal se recomienda realizar:

1. Escucha del audio.
2. Visualización de la forma de onda.
3. Cálculo de la DFT.
4. Estimación de la PSD usando Welch.
5. Comparación de la PSD para distintos valores de `nperseg`.
6. Cálculo del Cepstrum.
7. Estimación aproximada de la frecuencia fundamental usando el Cepstrum.
8. Interpretación breve.

---

## 8. Código base sugerido

### 8.1. Cargar archivos de voz

```python
from pathlib import Path

VOICE_DATA_DIR = PROJECT_ROOT / "data" / "class_voice_vowels"

voice_files = sorted(VOICE_DATA_DIR.rglob("*.wav"))

print(f"Number of voice files found: {len(voice_files)}")

for i, file_path in enumerate(voice_files[:20], start=1):
    print(f"{i}. {file_path.relative_to(VOICE_DATA_DIR)}")
```

### 8.2. Seleccionar y escuchar un archivo

```python
selected_voice_file = voice_files[0]

y_voice, sr_voice = librosa.load(selected_voice_file, sr=None, mono=True)

print("Selected file:", selected_voice_file.name)
print("Sampling rate:", sr_voice)
print("Duration:", len(y_voice) / sr_voice)

display(Audio(y_voice, rate=sr_voice))
```

### 8.3. Visualizar forma de onda

```python
plot_waveform(
    y_voice,
    sr_voice,
    title=f"Waveform - {selected_voice_file.name}"
)
```

### 8.4. Calcular PSD

```python
plot_psd_audio(
    y_voice,
    sr_voice,
    title=f"PSD - {selected_voice_file.name}",
    max_freq=5000,
    nperseg=4096
)
```

### 8.5. Calcular Cepstrum

Para señales de voz, un rango de quefrency entre 2 ms y 20 ms puede ser útil, porque corresponde aproximadamente a frecuencias entre 500 Hz y 50 Hz.

```python
plot_cepstrum(
    y_voice,
    sr_voice,
    title=f"Cepstrum - {selected_voice_file.name}",
    min_quefrency_ms=2.0,
    max_quefrency_ms=20.0
)
```

### 8.6. Estimar peak cepstral dominante

```python
q_ms, f_equiv = dominant_cepstral_peak(
    y_voice,
    sr_voice,
    min_quefrency_ms=2.0,
    max_quefrency_ms=20.0
)

print("Dominant cepstral peak:")
print(f"Dominant quefrency: {q_ms:.2f} ms")
print(f"Equivalent frequency: {f_equiv:.1f} Hz")
```

---

## 9. Interpretación esperada

La PSD permite observar la distribución de energía en frecuencia. En señales de voz sostenida, es común observar una estructura armónica: peaks aproximadamente separados por una frecuencia fundamental.

El Cepstrum puede ayudar a detectar esa separación regular entre armónicos. Si aparece un peak cepstral en una quefrency `q`, se puede calcular una frecuencia equivalente aproximada mediante:

```text
f = 1 / q
```

Si `q` está en milisegundos:

```text
f [Hz] = 1000 / q [ms]
```

Ejemplos:

```text
2 ms  -> 500 Hz
4 ms  -> 250 Hz
5 ms  -> 200 Hz
10 ms -> 100 Hz
20 ms -> 50 Hz
```

Esta frecuencia equivalente puede relacionarse con la periodicidad de la señal o con la separación entre armónicos, pero debe interpretarse con cuidado.

---

## 10. Preguntas de interpretación

Cada grupo debe responder brevemente:

1. ¿Qué vocales fueron grabadas?
2. ¿Qué archivo analizaron en detalle?
3. ¿La vocal seleccionada se percibe como estable, ruidosa o variable?
4. ¿Qué se observa en la forma de onda?
5. ¿La PSD muestra una estructura armónica clara?
6. ¿En qué rango de frecuencias se concentra la mayor energía?
7. ¿Qué frecuencia dominante o fundamental aproximada se estimó?
8. ¿El Cepstrum muestra un peak claro? ¿En qué quefrency?
9. ¿La frecuencia equivalente del peak cepstral tiene sentido al compararla con la PSD?
10. ¿Qué diferencias observaron entre las vocales /a/, /e/, /i/, /o/, /u/? 

---

## 11. Cierre conceptual

Esta actividad muestra que las herramientas de análisis en frecuencia son generales. Las mismas ideas que usamos para estudiar señales de anfibios y aves también pueden aplicarse a señales de voz humana.

En todos los casos, buscamos responder preguntas como:

- ¿Cómo cambia la señal en el tiempo?
- ¿Qué frecuencias están presentes?
- ¿Dónde se concentra la energía?
- ¿Hay estructura armónica?
- ¿Existen periodicidades en el espectro?
- ¿Qué método de estimación espectral entrega una representación más clara?

La DFT, la PSD, Welch y el Cepstrum no son herramientas exclusivas de un tipo de señal: son herramientas fundamentales para estudiar señales acústicas, biológicas, musicales, ambientales y experimentales.
