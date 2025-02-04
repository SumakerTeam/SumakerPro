# Sumaker Team

# Sumaker Pro - Robot de Mini Sumo Competitivo

**Sumaker Pro** es la versión mejorada del robot Sumaker, el cual fue diseñado inicialmente para la feria Maker de Lleida como un robot radiocontrolado (RC) accesible, con el propósito de que los niños pudieran interactuar y jugar con él. En esta versión "Pro", mi objetivo ha sido llevar la tecnología al siguiente nivel, construyendo un robot competitivo que pueda desafiar a otros participantes en la Oshwdem 2024.

En este proyecto, el enfoque ha sido maximizar la potencia y la adherencia dentro de las limitaciones de peso y tamaño del robot, que no puede superar los **500 gramos** y debe medir **10x10 cm**.

## Objetivos de Diseño
El robot cuenta con un **eje basculante** entre la pieza que sujeta el conjunto de motores, reductoras, llantas y la base del robot. Esta característica permite que tanto las ruedas como la cuña destinada a levantar a los robots rivales siempre permanezcan en contacto con el suelo, optimizando la tracción y efectividad durante la competencia.
El objetivo principal fue crear un robot potente y compacto, con un enfoque en maximizar la adherencia al dohyo (el área de combate) y lograr una configuración mecánica eficiente. Para conseguirlo, hemos implementado las siguientes estrategias:

- **Potencia con un Tamaño Limitado**: El robot está motorizado con motores **brushless** pequeños que han sido modificados para ajustarse al espacio disponible. Cada motor, junto con una reductora 100:1 y el eje, ocupa menos de **5 cm**, considerando que el ancho total del robot es de 10 cm.
- **Eficiencia en la Reducción**: Se han utilizado motores **inrunner** para reducir el desgaste en las reductoras y asegurar un funcionamiento suave. Esta configuración permite menos vibración y mayor eficiencia.
- **Maximizar la Adherencia**: Las ruedas cubren casi todo el ancho del robot. Cada rueda mide **45 mm** de largo, por lo que entre ambas ocupan **90 mm** del ancho disponible. Esto deja solo **8 mm** para la pieza central que soporta los dos motores, incluyendo 1 mm de holgura por lado. Esta pieza se fabricó en aluminio para asegurar la rigidez y resistencia necesaria, ya que el plástico impreso no sería suficiente estructuralmente.
- **Reducción del Peso en el Eje**: Para evitar que el eje de la reductora soporte el peso completo de la rueda, se ha añadido un **rodamiento de agujas** entre la llanta y el motor, que actúa como soporte adicional.

## Proceso de Fabricación
Los motores **brushless** fueron modificados, recortándolos **6 mm** usando un mini torno para ajustarse a las dimensiones requeridas. Las piezas CNC y las PCB fueron fabricadas por **JLCPCB**, lo cual ayudó a obtener una alta calidad y precisión en los componentes mecánicos y electrónicos.

## Componentes Utilizados
- **Microcontrolador**: STM32F730. Este microcontrolador fue elegido por su excelente relación calidad-precio y por contar con una amplia variedad de periféricos, temporizadores y otras características que permiten una gestión eficiente del robot.
- **Motores**: SURPASS JOBBY KK 2030 4500KV
- **Reductoras**: JGA20-180 93RPM
- **ESC**: Emax Bullet 20A BLheli_S DSHOT
- **Sensores de Distancia**: GP2Y0A21YK0F
- **Sensores de Límite del Dojo**: QRE1113
- **Batería**: LiPo TATTU 3s 450mAh 75C - Alargada

## Sensores y Desafíos en la Detección
Inicialmente, la PCB fue diseñada para integrar los sensores **Sharp GP2Y0E03**, que en pruebas preliminares parecían funcionar bien. Sin embargo, pronto se descubrió que no detectaban de manera confiable al robot adversario, lo cual llevó a reemplazarlos por los **GP2Y0A21YK0F**, que aunque funcionan bien, resultan ser bastante lentos.

Uno de los mayores retos al diseñar un robot de sumo es encontrar sensores que puedan detectar adecuadamente objetos con superficies negras mate a suficiente distancia. Los sensores ópticos comunes tienden a tener dificultades, ya sea por falta de velocidad o por incapacidad de detectar colores oscuros.

Para mejorar la respuesta de los sensores, también se añadieron **comparadores en la PCB**, los cuales disparan una señal digital cuando el valor de tensión supera un umbral definido. Sin embargo, en la práctica, se descubrió que los ADC (convertidores analógico-digital) eran lo suficientemente rápidos, lo que hizo que esta optimización no fuera tan necesaria como se pensó al principio.

## Lógica de Control del Robot
El corazón del robot es el **STM32F730**, un microcontrolador que ofrece la potencia y la versatilidad necesarias para gestionar todas las tareas críticas, desde el control de motores hasta el procesamiento de datos de los sensores.El robot está controlado mediante una **máquina de estados**. Los cambios de estado son gestionados por **interrupciones externas** que responden a las lecturas de los sensores. Por ejemplo, si los sensores detectan que el robot está siendo levantado, el sistema puede cambiar a un estado defensivo.

La configuración diferencial de los motores permite ajustar la respuesta del robot según la distancia del oponente. Cuanto más lejos está el adversario, menor es la corrección en la velocidad de cada rueda, para evitar perder al oponente de vista y mantener un enfoque efectivo.

## Conclusión
**Sumaker Pro** es un intento ambicioso de llevar las capacidades de un robot de sumo hasta el límite de las restricciones de tamaño y peso. La combinación de un diseño mecánico compacto, componentes de alta calidad y un sistema de control robusto nos permite enfrentar los desafíos de la competencia con una cierta confianza.
Es importante mencionar que no estamos ante un robot 100% confiable, ya que durante las pruebas se rompieron 4 reductoras. Es fundamental implementar rampas de aceleración y frenado cuando se requiere mucha aceleración o desaceleración, ya que las reductoras están diseñadas para trabajar con motores de 15.000 rpm y los motores brushless a 12V alcanzan aproximadamente 54.000 rpm.
Por otra parte creo que los sensores de distancia no estan a la altura de lo que seria un robot de competición. No se puede actualizar las lecturas cada 20 o 30ms, esto hace que el robot no pueda moverse con soltura porque los motores podrian hacer las maniobras con mucha mas velocidad y el micro va sobrado. Claramente el cuello de embudo son los sensores.

## Licencia
Este proyecto está bajo la Licencia MIT. Consulta el archivo `LICENSE` para más detalles.

## Contacto
Para más información, puedes contactarnos en sumakerteam@gmail.com.




