# Fundamentos de FFT y PSD

## Transformada Discreta de Fourier (DFT)

La Transformada Discreta de Fourier (DFT) permite representar una señal
en el dominio de la frecuencia. Es decir, transforma una señal en el
tiempo en una combinación de componentes sinusoidales de distintas
frecuencias.

### Expresión matemática

$X[k] = \sum_{n=0}^{N-1} x[n] e^{-j 2\pi kn/N}$

### Interpretación

-   $x[n]$: señal en el dominio del tiempo
-   $X[k]$: representación en frecuencia
-   $k$: índice de frecuencia

Cada valor de la DFT indica cuánto de una frecuencia específica está
presente en la señal.

------------------------------------------------------------------------

## Transformada Rápida de Fourier (FFT)

La FFT es un algoritmo eficiente para calcular la DFT.

-   Reduce el costo computacional de O(N²) a O(N log N)
-   Permite analizar señales de gran tamaño en tiempo razonable

------------------------------------------------------------------------

## Densidad Espectral de Potencia (PSD)

La PSD describe cómo se distribuye la energía de una señal en el dominio
de la frecuencia.

### Expresión conceptual

$PSD(f) = |X(f)|²$

### Interpretación

-   Representa la energía de la señal en cada frecuencia
-   Es más estable que la FFT
-   Reduce la variabilidad mediante promediado (por ejemplo, método de
    Welch)

### Método de Welch

La PSD puede estimarse utilizando el método de Welch, que mejora la estabilidad del espectro.

En lugar de calcular una única FFT sobre toda la señal, el método:

- divide la señal en segmentos
- calcula la FFT de cada uno
- promedia los resultados

Esto reduce la variabilidad y produce una estimación más robusta de la distribución de energía en frecuencia.

------------------------------------------------------------------------

## Diferencias clave

  FFT                      PSD
  ------------------------ --------------------
  Amplitud                 Energía
  Más ruidosa              Más suave
  Representación directa   Promedio espectral

------------------------------------------------------------------------

## Aplicaciones

-   Identificación de frecuencias dominantes
-   Análisis de señales acústicas
-   Detección de patrones en vibraciones
-   Caracterización de señales biológicas

------------------------------------------------------------------------

## Preguntas para reflexión

1.  ¿Qué significa que una frecuencia tenga mayor amplitud?
2.  ¿Por qué la PSD es más estable que la FFT?
3.  ¿En qué situaciones preferirías usar PSD en lugar de FFT?
