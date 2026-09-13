# Asistencia de Inteligencia Artificial

- **Prompts utilizados**:
    - "¿Por qué una señal PWM puede utilizarse para producir sonido mediante un zumbador piezoeléctrico?"
    - "¿Cuál es la diferencia entre el efecto piezoeléctrico directo y el efecto piezoeléctrico inverso?"
    - "¿Cuál es la diferencia entre un zumbador piezoeléctrico activo y uno pasivo, cómo funciona cada uno y cuál permite generar diferentes tonos?"
    - "¿El ciclo de trabajo de una señal PWM modifica el tono de un zumbador piezoeléctrico, el volumen, la forma de onda o alguna otra característica del sonido?"
    - "¿Cómo funciona el PWM en el microcontrolador RP2040 utilizado por la Raspberry Pi Pico?"
    - "¿Qué relación existe entre la frecuencia del reloj del microcontrolador y las frecuencias PWM que puede generar?"
    - "¿Qué aplicaciones tiene la generación de tonos y melodías mediante PWM en un zumbador piezoeléctrico dentro de los sistemas embebidos?"

- **Herramientas utilizadas**:
    - ChatGPT
    - Claude Code
    - Copilot

- **Cambios y validación**:
    - Sobre el mapeo del GPIO en el slice/canal y la fórmula de frecuencia PWM del RP2040, confirmé los valores en el datasheet oficial de Raspberry Pi.
    - El cálculo de TOP y CC para 440 Hz que dio la IA lo repetí por mi cuenta para confirmar los valores.
    - La IA dijo que el duty cycle afecta el volumen, pero no el tono. Comprobé esto revisando cómo funciona el efecto piezoeléctrico inverso.
    - Las frecuencias de las notas La, Do y Mi en diferentes octavas las comparé con una tabla estándar y también hice los cálculos por mi cuenta para comprobar que fueran correctas.
    - La IA me mencionó otros usos del PWM, como motores y LEDs, pero como no eran específicos de los zumbadores piezoeléctricos, decidí no incluirlos.

- **Reflexión personal**:
La IA a veces me mezcló información general de PWM con información específica del zumbador piezoeléctrico, sin ver realmente cuál aplicaba al tema que le preguntaba. Esto me enseñó a revisar cada respuesta contra una fuente confiable antes de usar el dato, en lugar de aceptarlo solo porque sonaba coherente.

- **Fecha**: 12-09-2026
- **Plataforma utilizada**: Raspberry Pi Pico (RP2040), como referencia conceptual de hardware.
