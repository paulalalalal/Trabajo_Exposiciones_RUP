# Preguntas de la dinámica · E2 · Inventario y equipamiento

|Campo|Valor|
|-|-|
|**Equipo**|E2 · Requisitos|
|**Módulo**|Inventario y equipamiento (RPG Manager)|
|**Responsable**|Emily Sofia Castillo Preciado|
|**Versión**|1.0|
|**Formato sugerido**|Tarjetas A / B / C levantadas por filas (5 min en total)|
|**Basada en**|`05\_requisitos.md`, `07\_especificaciones\_cu\_equipar.md`, `00\_eslabon\_trazabilidad.md`|

> Cumplimiento de las reglas: P1 y P2 son de tipo «¿qué artefacto usarías?»; P3 y P4 son de tipo «encuentra el error»; P5 es de aplicación (impacto de un cambio). Ninguna es de memoria.

\---

## Pregunta 1 · ¿Qué artefacto usarías?

Eres del equipo E6 y vas a escribir el caso de prueba de rendimiento de **Consultar inventario** con 30 ítems. Necesitas saber en cuánto tiempo debe responder el sistema y en qué porcentaje de las solicitudes. ¿Qué artefacto de E2 abres?

* a) Especificación del CU «Equipar ítem» (artefacto 7)
* b) Requisitos funcionales y no funcionales (artefacto 5)
* c) Modelo de casos de uso (artefacto 6)

**Respuesta correcta: b)**

**Explicación:** el criterio medible está en **RNF-INV-01**: la consulta con 30 ítems debe responder en ≤ 2 s en el 95 % de las solicitudes. Ese número se convierte directamente en la prueba (100 repeticiones).

* **a) falla:** el artefacto 7 solo fija ≤ 1 s para confirmar el *equipamiento* (paso 9). Si el tester lo usara, probaría la consulta contra el umbral equivocado (1 s en vez de 2 s).
* **c) falla:** el modelo de casos de uso muestra actores y funcionalidades, no criterios numéricos de calidad.

\---

## Pregunta 2 · ¿Qué artefacto usarías?

El profesor (cliente) pregunta: «¿Qué puede hacer cada actor, el Jugador y el Game Master, dentro del módulo de inventario?». Quieres responderle de un vistazo, con un mapa de toda la funcionalidad. ¿Qué artefacto muestras?

* a) Modelo de casos de uso (artefacto 6)
* b) Glosario (E1)
* c) Diagrama de secuencia (E4)

**Respuesta correcta: a)**

**Explicación:** el modelo de casos de uso es el mapa de quién usa el sistema y para qué: el Jugador administra el inventario (CU-05 Gestionar Inventario, CU-09 Usar poción) y el Game Master solo consulta (solo lectura).

* **b) falla:** el glosario define cada término con un único significado (Personaje, Ítem, Ranura…), pero no dice qué hace cada actor.
* **c) falla:** el diagrama de secuencia (E4) detalla la colaboración de objetos para *un* caso de uso, no ofrece el panorama completo del módulo.

\---

## Pregunta 3 · Encuentra el error

Este es un fragmento del flujo alternativo A2 de la especificación del CU «Equipar ítem». Tiene **un** defecto plantado:

> **A2. Ranura ocupada (se activa en el paso 6)**
> 1. El Sistema detecta que la ranura ya tiene un ítem equipado (máximo 1 por ranura).
> 2. El Sistema desequipa el ítem anterior para devolverlo al inventario.
> 3. **Si el inventario tiene 30/30 espacios ocupados:** el Sistema rechaza la acción con el mensaje "Inventario lleno", mantiene el ítem anterior equipado y el caso termina (fallo).
> 4. **Si hay espacio:** el ítem anterior vuelve al inventario y el flujo continúa en el **paso 9.**

¿Dónde está el error?

* a) En el punto 2: no debería desequipar antes de verificar el espacio
* b) En el punto 4: el flujo debe continuar en otro paso
* c) En el punto 3: el mensaje de rechazo no coincide con los requisitos

**Respuesta correcta: b)** El flujo debe continuar en el **paso 7** («Equipa el ítem en la ranura y lo marca como equipado»).

**Explicación:** al saltar al paso 9, el sistema confirmaría la operación sin equipar el ítem nuevo (paso 7) y sin guardar el cambio (paso 8). Eso rompe las postcondiciones de éxito 1 y 3 y el requisito RNF-INV-04 de persistencia.

* **a) falla:** el punto 2 está igual que en la especificación original; el punto 3 se encarga de deshacer el efecto cuando no hay espacio, y la postcondición de fallo exige que todo quede como estaba.
* **c) falla:** "Inventario lleno" es el mensaje literal que define RF-INV-01 para el inventario con 30 espacios ocupados.

\---

## Pregunta 4 · Encuentra el error

Este fragmento de la sección de trazabilidad del artefacto 5 (requisito → prueba) tiene **una fila** que no coincide con su requisito:

|Requisito|Se verificará con (E6)|
|-|-|
|RF-INV-02|Inventario con 12 ítems → lista 12 filas y muestra "12/30"|
|RF-INV-05|Vida 30/100 + poción → vida **70/100** y cantidad −1|
|RNF-INV-02|Mago con 41 kg → rechazado|

¿Qué fila es la incorrecta y por qué?

* a) RF-INV-02: el indicador "12/30" no corresponde a 12 ítems
* b) RF-INV-05: el resultado esperado no coincide con lo que restaura la poción
* c) RNF-INV-02: 41 kg no supera el límite del Mago

**Respuesta correcta: b)** Con vida 30/100, una poción restaura **50 puntos** (RF-INV-05), así que el resultado esperado es **80/100**, no 70/100.

**Explicación:** un resultado esperado equivocado produce un «defecto» falso: la prueba fallaría con el sistema funcionando bien, y E6 registraría un error que no existe en el código sino en el artefacto.

* **a) falla:** el indicador muestra los espacios usados sobre 30, y 12 ítems ocupan 12 espacios (12/30).
* **c) falla:** el límite del Mago es 40 kg (RNF-INV-02), por lo que 41 kg lo supera y debe rechazarse.

\---

## Pregunta 5 · Aplicación: ¿Qué cambia si cambia el requisito?

El cliente decide que los Magos podrán cargar **60 kg** en lugar de 40 kg. ¿Qué debe revisar y actualizar el equipo?

* a) Solo `05\_requisitos.md`, porque ahí está el requisito
* b) El requisito (RNF-INV-02) y todo lo que repite o verifica ese valor: reglas de negocio del CU, eslabón de trazabilidad, casos de prueba y la presentación
* c) Solo el código fuente, porque el peso es un dato de implementación

**Respuesta correcta: b)**

**Explicación:** en RUP los artefactos evolucionan y están enlazados; el valor «40 kg del Mago» aparece en varios y todos deben cambiar juntos:

* Artefacto 5: RNF-INV-02 y su prueba «Mago con 41 kg».
* Artefacto 7: sección 7 · Reglas de negocio.
* Eslabón de trazabilidad: reglas de dominio y la prueba CP-INV-09 («Mago intenta superar 40 kg»).
* Presentación: diapositiva de requisitos no funcionales.

Además, la prueba actual «Mago con 41 kg → rechazado» pasaría a ser incorrecta: con el nuevo límite, 41 kg debe *aceptarse* y el caso de rechazo pasa a 61 kg.

* **a) falla:** actualizar solo el requisito deja los demás artefactos contradiciéndose entre sí (justo la inconsistencia que más cuesta en un proyecto).
* **c) falla:** el código sigue al requisito, no al revés; si no se actualizan requisitos y pruebas, no hay forma de verificar el cambio.

