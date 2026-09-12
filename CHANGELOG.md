## [1.0.1] - 2026-09-12
- Probé el caso que faltaba (producto sin datos de nutrición) con uno real.
  Ya no queda ninguna prueba pendiente.

## [1.0.0] - 2026-09-12
- Probé las 7 formas de usar el flujo y todas funcionan.
- Le puse nombre claro a cada nodo.
- Escribí notas cortas en los nodos y el README.

## [0.1.0] - 2026-09-12
**Webhook - Receive Nutrition Check**
- Primer nodo: recibe el código de barras por POST en `/nutrition-check`.

**Validate - Barcode Present**
- Revisa que venga el campo `barcode`. Si no viene, no se rompe, explica cómo usarlo.

**Format - Self Documentation Message**
- El mensaje que se ve si no mandas ningún código.

## [0.2.0] - 2026-09-12
**Validate - Barcode Is Numeric**
- Revisa que el código sean solo números.

**Respond - Invalid Barcode (400)**
- Mensaje de error si el código trae letras.

**API Call - Open Food Facts Product**
- Se conecta a la base de datos para traer los datos del producto.
- **Error que hubo:** la dirección web tenía escrito `{barcode}` a secas, sin
  ser una fórmula de verdad. Por eso siempre buscaba lo mismo, no importaba
  qué código mandara. Lo arreglé poniendo `{{ $json.body.barcode }}`.
- Configuré que si da error 404, no se rompa el flujo.

## [0.3.0] - 2026-09-12
**Validate - Product Found**
- Revisa si el producto existe o no.
- **Error 1:** me faltaba el signo `$` en la fórmula (`json.status` en vez de
  `$json.status`).
- **Error 2:** tenía puesto `0` donde debía ir `1`, así que confundía
  "encontrado" con "no encontrado". Lo cambié.

**Respond - Product Not Found (404)**
- Mensaje si el producto no existe.

## [0.4.0] - 2026-09-12
**Validate - Nutrient Data Present**
- Revisa si faltan los datos de azúcar, sal y grasa.
- **Error 1:** otra vez me faltaba el `$` en las tres condiciones.
- **Error 2:** un choque de tipos (número contra texto) daba error. Lo
  arreglé activando "Convert types where required".

**Format - Insufficient Data Message**
- Mensaje cuando no hay datos suficientes.

**Merge - Info Responses (Append)**
- Junta el mensaje de "sin código" y el de "sin datos" en una sola salida.

**Respond - Info Message (200)**
- **Error:** al principio daba "Invalid JSON" con `{{ $json }}`. Lo arreglé
  cambiando a la opción "All Incoming Items", que no necesita escribir nada.

## [0.5.0] - 2026-09-12
**Format - Flatten Product Fields**
- Saca del producto los datos que hacen falta (nombre, marca, nota, azúcar,
  sal, grasa, energía).
- **Error 1:** el campo de grasa tenía copiada por error la fórmula de la
  sal.
- **Error 2:** el campo de energía tenía el nombre mal escrito (le faltaba
  la "c" de "kcal") y la fórmula con los corchetes mal puestos.

## [0.6.0] - 2026-09-12
**Calculate - Traffic Light Level**
- Decide si el azúcar, sal y grasa son bajos, medios o altos.
- **Error 1:** una llave `}` estaba puesta en el sitio equivocado.
- **Error 2:** en la parte de la sal, usé por error la variable del azúcar.
- **Error 3:** un número de más (`17.5 5`) y una palabra mal escrita
  (`falt_level` en vez de `fat_level`).

**Calculate - Concern Levels & Verdict Readings**
- Cuenta cuántos salieron "altos" y mira también la nota del producto.

**Calculate - Final Verdict & Tone**
- Decide el veredicto final (el peor de los dos) y el tono del mensaje.
- **Error:** me faltaba una llave de cierre, así que el `return` final
  quedaba atrapado dentro de un bloque que no debía.

**AI - Health Verdict (Adaptive Tone)**
- La IA escribe el párrafo final.
- **Error:** el modelo de IA que tenía puesto ya no existía (Groq lo quitó).
  Tuve que elegir otro de la lista.

**Format - Final Verdict Message**
- Junta el título, los números y el párrafo en un solo mensaje.
- **Error:** los datos del producto llegaban vacíos (`undefined`) porque la
  IA no pasa los demás datos hacia adelante. Lo arreglé pidiéndoles
  directamente al nodo de antes.

**Respond - Verdict (Plain Text, 200)**
- Última pieza: devuelve el mensaje final como texto normal.

