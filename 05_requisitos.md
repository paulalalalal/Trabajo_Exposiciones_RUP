# Artefacto 5 · Requisitos funcionales y no funcionales

| Campo | Valor |
|---|---|
| **Equipo** | E2 · Requisitos |
| **Módulo** | Inventario y equipamiento (RPG Manager) |
| **Rol RUP** | Especificador de requisitos |
| **Fase** | Inicio → Elaboración |
| **Versión** | 1.0 (borrador para iteración 1) |
| **Viene de** | Visión del sistema y Glosario (E1) |
| **Alimenta a** | Modelo de casos de uso (06), Especificación de CU (07), Casos de prueba (E6) |

> Convención: cada requisito tiene un ID único, es **verificable** (contiene un número o criterio medible) y puede convertirse directamente en un caso de prueba.
> Prioridad: **Alta** = sin esto el módulo no sirve · **Media** = importante, puede entrar en la iteración 2 · **Baja** = deseable.

---

## 1. Requisitos funcionales (RF)

| ID | Descripción | Tipo | Prioridad | Caso de uso relacionado |
|---|---|---|---|---|
| RF-INV-01 | El sistema debe permitir al Jugador **agregar un ítem** al inventario de su Personaje siempre que haya espacio libre (máximo **30**) y el peso total resultante no supere el límite de la clase. Si el inventario ya tiene 30 espacios ocupados, debe rechazar la acción y mostrar el mensaje "Inventario lleno" sin modificar el inventario. | Funcional | Alta | CU-05 Gestionar Inventario |
| RF-INV-02 | El sistema debe permitir **consultar el inventario** mostrando, por cada ítem: nombre, tipo, peso (kg), cantidad y si está equipado, junto con el peso total y los espacios usados (ej. "12/30"). | Funcional | Alta | CU-05 Gestionar Inventario |
| RF-INV-03 | El sistema debe permitir **equipar un ítem** del inventario solo si es compatible con la clase del Personaje (Guerrero, Mago o Arquero). Si no es compatible, debe rechazar la acción e informar el motivo (ej. "Un Mago no puede equipar Espada pesada"). Un Personaje puede tener equipado **máximo 1 ítem por ranura** (arma, armadura, accesorio). | Funcional | Alta | CU-05 Gestionar Inventario |
| RF-INV-04 | El sistema debe permitir **descartar un ítem** previa confirmación del Jugador. Al confirmar, el ítem desaparece del inventario y se liberan sus espacios y su peso. Si el Jugador cancela, el inventario no cambia. | Funcional | Media | CU-05 Gestionar Inventario |
| RF-INV-05 | El sistema debe permitir **usar una poción** desde el inventario: consume **1 unidad**, restaura **50 puntos de vida** al Personaje sin superar su vida máxima y descuenta 1 a la cantidad de pociones. Si la cantidad es 0, no debe permitir la acción e informar "No quedan pociones". | Funcional | Alta | CU-09 Usar poción (extiende CU-07) |
| RF-INV-06 | El sistema debe permitir **desequipar un ítem**, devolviéndolo al inventario. Si el inventario tiene 30/30 espacios ocupados, debe rechazar la acción y mantener el ítem equipado. | Funcional | Media | CU-05 Gestionar Inventario |

---

## 2. Requisitos no funcionales (RNF)

| ID | Descripción | Categoría | Prioridad |
|---|---|---|---|
| RNF-INV-01 | **Rendimiento:** consultar el inventario (con 30 ítems) debe responder en **≤ 2 segundos** en el **95 %** de las solicitudes; equipar o descartar un ítem debe confirmarse en **≤ 1 segundo**. | Rendimiento | Alta |
| RNF-INV-02 | **Restricción de capacidad:** el inventario tiene un máximo de **30 espacios** y un peso máximo según la clase: Guerrero **80 kg**, Arquero **60 kg**, Mago **40 kg**. Ninguna operación puede dejar al Personaje por encima de estos límites. | Restricción | Alta |
| RNF-INV-03 | **Seguridad:** solo el Jugador dueño del Personaje, con sesión activa, puede modificar su inventario (**100 %** de las operaciones de escritura validan la sesión). El Game Master tiene acceso de **solo lectura**. Todo intento no autorizado debe registrarse en el log con fecha, usuario y operación. | Seguridad | Alta |
| RNF-INV-04 | **Confiabilidad y persistencia:** todo cambio en el inventario debe guardarse en la base de datos en **≤ 1 segundo** y sobrevivir a un reinicio del sistema (**0 ítems perdidos**). Además, se debe generar una copia de seguridad en el Servicio de Respaldo en la Nube al menos **1 vez cada 24 horas**. | Confiabilidad | Media |

---

## 3. Trazabilidad: requisito → caso de uso → prueba

| Requisito | Caso de uso del modelo (artefacto 6/7) | Se verificará con (E6) |
|---|---|---|
| RF-INV-01 | CU-05 Gestionar Inventario | Agregar el ítem #31 → debe aparecer "Inventario lleno" |
| RF-INV-02 | CU-05 Gestionar Inventario | Inventario con 12 ítems → lista 12 filas y muestra "12/30" |
| RF-INV-03 | CU-05 Gestionar Inventario (Equipar ítem) | Mago equipa Espada pesada → rechazado con mensaje |
| RF-INV-04 | CU-05 Gestionar Inventario | Descartar y confirmar → espacios libres +1 |
| RF-INV-05 | CU-09 Usar poción | Vida 30/100 + poción → vida 80/100 y cantidad −1 |
| RF-INV-06 | CU-05 Gestionar Inventario | Desequipar con 30/30 → rechazado, ítem sigue equipado |
| RNF-INV-01 | Todos | Medir tiempos con 30 ítems, 100 repeticiones |
| RNF-INV-02 | CU-05 | Mago con 41 kg → rechazado |
| RNF-INV-03 | CU-05 | Modificar inventario sin sesión → rechazado y registrado en log |
| RNF-INV-04 | CU-05 | Reiniciar sistema → inventario idéntico; verificar respaldo diario |

---

## 4. Insumos usados y consistencia con otros artefactos

- **Del Glosario (E1):** Personaje, Clase (Guerrero, Mago, Arquero), Vida, Ítem, Inventario, Poción. Se usan con el mismo significado en todos los requisitos.
- **De los diagramas del RPG Manager:** CU-05 Gestionar Inventario, CU-09 Usar poción y el flujo F9 "copia de seguridad de partidas" hacia el Servicio de Respaldo en la Nube (origen de RNF-INV-04).
- **Hacia la Especificación de CU (07):** el caso "Equipar ítem" cubre **RF-INV-03**, y sus flujos alternativos cubren **RF-INV-01 / RNF-INV-02** (inventario lleno / peso) y **RF-INV-06**.

## 5. Supuestos

1. Los valores numéricos (30 espacios, 50 puntos de vida, límites de peso) son valores iniciales acordados para esta iteración y pueden ajustarse con el cliente.
2. Las ranuras de equipo son tres: arma, armadura y accesorio.
3. La compra de ítems exclusivos del Jugador Premium (CU-13) queda fuera de este módulo en la primera versión.
