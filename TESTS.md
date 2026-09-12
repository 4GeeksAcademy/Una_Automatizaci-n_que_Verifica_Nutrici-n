# Pruebas que se hicieron

| ID | Tipo | Qué se probó | Qué se mandó | Qué se esperaba | Qué pasó | Veredicto |
|---|---|---|---|---|---|---|
| TC-001 | Que funcione | Un código que si existe y tiene todos los datos | `{"barcode": "3017620422003"}` (Nutella) | Que diga "no saludable" | Salió bien | Funciona |
| TC-002 | Que funcione | Un código donde el semáforo dice una cosa pero el Nutri-Score dice otra | `{"barcode": "5449000000996"}` (Coca-cola) | Que se quede con la peor de las dos | Salió bien | Funciona |
| TC-003 | Que funcione | Un código con solo algunos datos, que sale sano | `{"barcode": "3274080005003"}` (agua) | Que diga "saludable" aunque le falten datos | Salió bien | Funciona |
| TC-004 | Que la API funcione de verdad | Coca-cola | Que traiga datos reales de la página de Open Food Facts | Trajo los datos reales | Funciona |
| TC-005 | Error | Un código que no existe | `{"barcode": "3068320123456"}` | Que diga que no lo encontró | Salió bien | Funciona |
| TC-006 | Error | Un código mal escrito | `{"barcode": "abc123"}` | Que diga que está mal escrito | Salió bien | Funciona |
| TC-007 | Error | Cuerpo vacio | `{}` | Que explique cómo se usa | Salió bien | Funciona |
| TC-008 | Error | Un producto sin datos de nutrición | Sidi Ali | Que diga que no hay datos suficientes | Respondió con “insufficient data” | Funciona |

## Rapidez

- La IA tarda medio segundo más o menos.
- Todo el proceso tarda cerca de 3 segundos
- No probé peticiones a la vez, las fui probando una por una.
