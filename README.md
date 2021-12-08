# Fuente para electroforesis de IORODEO

Documentación original: https://sites.google.com/iorodeo.com/electrophoresis-power-supply

* Diseño del PCB: https://sites.google.com/iorodeo.com/electrophoresis-power-supply/pcb-design
  * KiCAD: https://github.com/iorodeo/hv_switching_psu
* Lista de componentes: https://sites.google.com/iorodeo.com/electrophoresis-power-supply/pcb-components

Componentes clave:

* Fuente step-up: Maxim high efficiency MAX1771 step-up DC-DC controller (link [ML](https://articulo.mercadolibre.com.ar/MLA-674196971-regulador-step-up-alta-tension-max1771-csa-soic8-itytarg-_JM)).
* Mosfet.
* Voltage divider.
* KiCad design files: https://bitbucket.org/iorodeo/hv_switching_psu

## Teoría

El controlador MAX1771 está para controlar el MOSFET solamente, no es el generador de alto voltaje _en sí_.

El alto voltaje se genera en realidad a través de la inductancia [L1](https://github.com/iorodeo/hv_switching_psu/blob/master/original/hv_switching_psu.pdf). Cuando el MAX1771 activa al MOSFET, se acumula campo magnético en la inductancia, y al desactivar el MOSFET rápidamente, la inductancia genera alto voltaje.

Luego, ese alto voltaje va a los capacitores del lado de la salida, y este ciclo se repite muchas veces, cargando el capacitor con alto voltaje.

La regulación del voltaje a través de los capacitores depende de un divisor de voltaje, que lee la salida, y provee el feedback al MAX1771. Con ese feedback, asumimos que el MAX1771 "decide" si mandarle más o menos señal al MOSFET: si el voltaje es alto lo activa menos, y si es bajo lo activará más.

Martin tiene dudas sobre el voltaje y amperaje en el output: el integrado solo manda 12V como mucho. Que corriente de salida se puede generar?

# Cuba

Ver: https://github.com/tecsci/electrophoresis-cell
