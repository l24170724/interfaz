# Generación de tonos y melodías con PWM en un zumbador piezoeléctrico

## Introducción

## Desarrollo Técnico

**Conceptos acústicos**

El sonido es, en su forma más simple, una vibración mecánica que se propaga por el aire y llega al oído como una sensación audible. Tres conceptos bastan para describir esa vibración.

- Frecuencia (f) - número de vibraciones completas por segundo (se mide en hertz).
- Periodo (T) - duración de una sola vibración completa (una vibración más corta implica más vibraciones por segundo, de ahí que f = 1/T).
- Tono - forma en que el oído percibe la frecuencia; una frecuencia alta se percibe como un tono agudo y una frecuencia baja como un tono grave, la misma relación que un microcontrolador aprovecha para controlar el tono de un zumbador cambiando la frecuencia de su señal PWM [1].

| Magnitud | Qué es | Relación |
|---|---|---|
| Frecuencia (f) | Vibraciones completas por segundo | f = 1/T |
| Periodo (T) | Duración de una vibración completa | T = 1/f |
| Tono | Percepción subjetiva de la frecuencia | A mayor f, tono más agudo |

*Tabla 1. Vocabulario acústico.*

**Piezoelectricidad**

La piezoelectricidad tiene dos manifestaciones opuestas, y conviene distinguirlas antes de centrarse en la que realmente hace sonar un zumbador.

- Efecto directo - al deformar mecánicamente el material (aplicarle presión o esfuerzo), este genera un voltaje medible en su superficie; es la base de sensores de presión, vibración y micrófonos piezoeléctricos.
- Efecto inverso (o converso) - al aplicar un voltaje al material, este se deforma mecánicamente; es el efecto que usan los actuadores y, en particular, el disco cerámico de un zumbador [2].

El zumbador emplea únicamente el efecto inverso (el microcontrolador aplica el voltaje y el disco responde deformándose), de modo que el efecto directo no vuelve a mencionarse más adelante. Cada vez que se aplica un voltaje al disco, este se deforma un poco (la carga eléctrica se transforma en movimiento); al retirarlo o invertirlo, el disco regresa o se deforma en sentido contrario, y repetir este ciclo muchas veces por segundo produce la vibración mecánica que después se convierte en sonido.

**Zumbador piezoeléctrico**

Un zumbador piezoeléctrico es, físicamente, un disco metálico delgado con una lámina cerámica piezoeléctrica adherida encima (el diafragma); no requiere partes móviles adicionales ni bobinas, a diferencia de un altavoz convencional. Existen dos tipos, según la presencia o ausencia de un oscilador interno; esta diferencia determina cuál de los dos permite variar el tono desde el microcontrolador (el otro solo puede encenderse o apagarse, a una frecuencia fija de fábrica).

| Tipo | Oscilador interno | Señal que necesita | Permite variar el tono |
|---|---|---|---|
| Activo | Sí | Voltaje constante (encendido/apagado) | No, tono fijo de fábrica |
| Pasivo | No | Señal PWM de frecuencia variable | Sí |

*Tabla 2. Zumbador activo y pasivo [3].*

La cadena completa de conversión de energía puede resumirse en una sola frase, el microcontrolador entrega energía eléctrica variable (PWM), el disco piezoeléctrico la convierte en energía mecánica (flexión, por el efecto inverso), y esa flexión repetida convierte la energía mecánica en energía acústica (la onda de sonido que llega al oído) [4].

**PWM (señal que controla el zumbador)**

El PWM (modulación por ancho de pulso) es una señal que se prende y se apaga muy rápido, una y otra vez, dentro de un tiempo fijo llamado período (T). La parte de ese período en la que la señal se queda "prendida" se llama "duty cycle". En un zumbador piezoeléctrico, el período es el que controla el tono (qué tan agudo o grave suena), mientras que el duty cycle solo controla el volumen (qué tan fuerte suena), sin afectar el tono [1]. Por eso normalmente se usa un duty cycle bajo, hasta un 50%. Dentro de un microcontrolador real, un contador automático genera esta señal usando dos valores que se programan. El primer valor le dice al contador cuándo reiniciarse, y eso define el período. El segundo valor le dice hasta dónde contar antes de apagar la señal, y eso define el duty cycle.

**Puente entre PWM y el sonido percibido**

La frecuencia que se programa en el periférico PWM se convierte, por efecto piezoeléctrico inverso, en la frecuencia de flexión mecánica del disco; esa flexión mecánica empuja el aire a la misma frecuencia, generando una onda sonora; y esa onda sonora, al llegar al oído, se percibe como un tono correspondiente exactamente a la frecuencia programada. El duty cycle, en cambio, no participa en esta cadena de frecuencia sino en el volumen o intensidad sonora que se percibe [1], [4].

```mermaid
flowchart LR
    A["Frecuencia PWM (registro del microcontrolador)"] --> B["Vibracion del disco piezoelectrico"]
    B --> C["Onda de sonido en el aire"]
    C --> D["Tono percibido por el oido"]
```
*Diagrama 1. Cadena completa entre la señal PWM y el tono percibido.*

**Notas y melodías**

Para convertir una frecuencia en una nota musical basta un solo punto de referencia, normalmente se usa "La4" que equivale a 440 Hz [5]. Se usa esta nota como referencia porque es el estándar internacional de afinación musical (establecido formalmente en 1955 por la ISO) [6], de modo que prácticamente todos los instrumentos, equipos de audio y ejemplos de código parten de este mismo valor.

A partir de La4, el resto de las notas se puede obtener de dos formas:

- Si la nota está a una octava completa de distancia, basta con duplicar la frecuencia (si es una octava arriba) o dividirla entre dos (si es una octava abajo).
- Si la nota está a cualquier otra distancia, se necesita contar cuántos semitonos la separan de La4 y aplicar la fórmula general:

                                                        f = 440 × 2^(n/12)

    Donde `n` es el número de semitonos de distancia (positivo si la nota es más aguda que La4, negativo si es más grave), y 12 es la cantidad de semitonos que tiene una octava completa.

## Conclusiones

## Bibliografía

[1] mbedded.ninja, "Piezoelectric Speakers," *mbedded.ninja Electronics Notes*, 2012 (actualizado). [En línea]. Disponible: https://blog.mbedded.ninja/electronics/components/piezoelectric-speakers/

[2] Y. Meng, G. Chen, y M. Huang, "Piezoelectric Materials: Properties, Advancements, and Design Strategies for High-Temperature Applications," *Nanomaterials*, vol. 12, n.° 7, art. 1171, abr. 2022. [En línea]. Disponible: https://pmc.ncbi.nlm.nih.gov/articles/PMC9000841/

[3] K. Magdy, "Active Buzzer vs Passive Buzzer," *DeepBlueMbedded*, ago. 2023. [En línea]. Disponible: https://deepbluembedded.com/active-buzzer-vs-passive-buzzer/

[4] TDA Buzzer, "Piezoelectric Buzzer Guide: How It Works, Types & Drive Circuits," *TDA Buzzer Industry News*, 2025. [En línea]. Disponible: https://www.tda-buzzer.com/news/industry-news/piezoelectric-buzzer-guide-how-it-works-types-drive-circuits.html

[5] Dept. of Psychology, University of Washington, "Chapter 11: Sound and Pitch," notas del curso PSY 333, Seattle, WA, USA. [En línea]. Disponible: https://courses.washington.edu/psy333/lecture_pdfs/chapter11_SoundPitch.pdf

[6] F. Gribenski, "Plenty of pitches," *Nature Physics*, vol. 16, p. 232, 2020. [En línea]. Disponible: https://www.nature.com/articles/s41567-019-0707-1


### (Opcional) código, diagramas, esquemas y PDF de papers de referencia
