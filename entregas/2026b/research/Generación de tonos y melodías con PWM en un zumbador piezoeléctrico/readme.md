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

## Conclusiones

## Bibliografía

[1] mbedded.ninja, "Piezoelectric Speakers," *mbedded.ninja Electronics Notes*, 2012 (actualizado). [En línea]. Disponible: https://blog.mbedded.ninja/electronics/components/piezoelectric-speakers/

[2] Y. Meng, G. Chen, y M. Huang, "Piezoelectric Materials: Properties, Advancements, and Design Strategies for High-Temperature Applications," *Nanomaterials*, vol. 12, n.° 7, art. 1171, abr. 2022. [En línea]. Disponible: https://pmc.ncbi.nlm.nih.gov/articles/PMC9000841/

[3] K. Magdy, "Active Buzzer vs Passive Buzzer," *DeepBlueMbedded*, ago. 2023. [En línea]. Disponible: https://deepbluembedded.com/active-buzzer-vs-passive-buzzer/

[4] TDA Buzzer, "Piezoelectric Buzzer Guide: How It Works, Types & Drive Circuits," *TDA Buzzer Industry News*, 2025. [En línea]. Disponible: https://www.tda-buzzer.com/news/industry-news/piezoelectric-buzzer-guide-how-it-works-types-drive-circuits.html


### (Opcional) código, diagramas, esquemas y PDF de papers de referencia
