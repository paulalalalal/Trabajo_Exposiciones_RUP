**Artefacto 7 · Especificación de caso de uso: Equipar ítem**  
  
|  |  |  
| - | - |  
| **Campo** |  **Valor** |  
| **Equipo** |  E2 · Requisitos |  
| **Módulo** |  Inventario y equipamiento (RPG Manager) |  
| **Rol RUP** |  Especificador de requisitos |  
| **Fase** |  Elaboración |  
| **Versión** |  1.0 (borrador) |  
| **Viene de** |  Requisitos (05) y Modelo de casos de uso (06) |  
| **Alimenta a** |  Diagrama de secuencia (E4), Casos de prueba (E6) |  
  
   
  
---  
**1. Identificación**  
  
|  |  |  
| - | - |  
| **Campo** |  **Valor** |  
| **Nombre** |  Equipar ítem. |  
| **Caso de uso del modelo** |  CU-05 Gestionar Inventario (operación Equipar ítem) |  
| **Actor principal** |  Jugador |  
| **Actor secundario** |  Game Master (solo lectura, no puede ejecutar este caso) |  
| **Descripción** |  El Jugador equipa un ítem de su inventario en una ranura de su Personaje (arma, armadura o accesorio), siempre que sea compatible con la clase del Personaje. |  
  
   
**2. Requisitos que cubre**  
  
|  |  |  |  
| - | - | - |  
| **ID** |  **Descripción corta** |  **Dónde se aplica** |  
| **RF-INV-03** |  Equipar ítem solo si es compatible con la clase; máximo 1 ítem por ranura |  Pasos 5, 6 y 7; flujo A1 |  
| **RF-INV-06** |  Desequipar ítem y devolverlo al inventario; si hay 30/30, rechazar |  Flujo A2 |  
| **RF-INV-02** |  Consultar inventario (muestra si el ítem está equipado) |  Pasos 1, 2 y 9 |  
| **RNF-INV-01** |  Equipar se confirma en ≤ 1 segundo |  Paso 9 |  
| **RNF-INV-02** |  Límites de 30 espacios y de peso por clase |  Flujo A2 |  
| **RNF-INV-03** |  Solo el Jugador dueño, con sesión activa, modifica el inventario |  Paso 4; flujo A3 |  
| **RNF-INV-04** |  El cambio se guarda en la base de datos en ≤ 1 segundo |  Paso 8 |  
  
   
**3. Precondiciones**  
1. El Jugador tiene una sesión activa.  
2. El Jugador tiene un Personaje seleccionado.  
3. El ítem a equipar existe en el inventario de ese Personaje.  
**4. Postcondiciones**  
**Éxito:**  
1. El ítem queda marcado como equipado en la ranura correspondiente.  
2. Si la ranura estaba ocupada, el ítem anterior vuelve al inventario como no equipado.  
3. El cambio queda guardado en la base de datos.  
**Fallo (cualquier flujo alternativo):**  
1. El inventario y el equipamiento del Personaje quedan exactamente como estaban.  
2. El Jugador recibe un mensaje con el motivo del rechazo.  
**5. Flujo básico**  
  
|  |  |  |  
| - | - | - |  
| **Paso** |  **Actor** |  **Acción** |  
| 1 |  Jugador |  Abre el inventario de su Personaje. |  
| 2 |  Sistema |  Muestra la lista de ítems con nombre, tipo, peso, cantidad, si está equipado y los espacios usados (ej. "12/30"). |  
| 3 |  Jugador |  Selecciona un ítem y elige la opción "Equipar". |  
| 4 |  Sistema |  Verifica que la sesión del Jugador esté activa y que sea el dueño del Personaje. |  
| 5 |  Sistema |  Verifica que el ítem sea compatible con la clase del Personaje (Guerrero, Mago o Arquero). |  
| 6 |  Sistema |  Verifica que la ranura del ítem (arma, armadura o accesorio) esté libre. |  
| 7 |  Sistema |  Equipa el ítem en la ranura y lo marca como equipado. |  
| 8 |  Sistema |  Guarda el cambio en la base de datos. |  
| 9 |  Sistema |  Muestra la confirmación y el inventario actualizado (en ≤ 1 s). |  
  
   
*Fin del caso de uso.*  
**6. Flujos alternativos**  
**A1. Ítem no compatible con la clase (se activa en el paso 5)**  
**Requisito:** RF-INV-03  
1. El Sistema detecta que el ítem no es compatible con la clase del Personaje.  
2. El Sistema rechaza la acción y muestra el motivo, ej. "Un Mago no puede equipar Espada pesada".  
3. El inventario no se modifica.  
4. El caso de uso termina (fallo). El Jugador puede volver al paso 3 y elegir otro ítem.  
**A2. Ranura ocupada (se activa en el paso 6)**  
**Requisitos:** RF-INV-06, RNF-INV-02  
1. El Sistema detecta que la ranura ya tiene un ítem equipado (máximo 1 por ranura).  
2. El Sistema desequipa el ítem anterior para devolverlo al inventario.  
3. **Si el inventario tiene 30/30 espacios ocupados:** el Sistema rechaza la acción con el mensaje "Inventario lleno", mantiene el ítem anterior equipado y el caso termina (fallo).  
4. **Si hay espacio:** el ítem anterior vuelve al inventario y el flujo continúa en el paso 7.  
**A3. Sesión no válida o jugador no autorizado (se activa en el paso 4)**  
**Requisito:** RNF-INV-03  
1. El Sistema detecta que no hay sesión activa o que el usuario no es el dueño del Personaje.  
2. El Sistema rechaza la acción y registra el intento en el log con fecha, usuario y operación.  
3. El inventario no se modifica.  
4. El caso de uso termina (fallo).  
**7. Reglas de negocio**  
- Un Personaje puede tener equipado **máximo 1 ítem por ranura** (arma, armadura, accesorio).  
- Clases válidas: Guerrero, Mago, Arquero (según el Glosario de E1).  
- Límites del inventario: 30 espacios; peso máximo Guerrero 80 kg, Arquero 60 kg, Mago 40 kg.  
**8. Trazabilidad hacia pruebas (E6)**  
  
|  |  |  
| - | - |  
| **Flujo** |  **Prueba que lo verificará** |  
| Básico |  Guerrero equipa Espada pesada → queda equipada y se confirma en ≤ 1 s |  
| A1 |  Mago equipa Espada pesada → rechazado con mensaje, inventario sin cambios |  
| A2 |  Ranura de arma ocupada y inventario 30/30 → rechazado, ítem anterior sigue equipado |  
| A3 |  Equipar sin sesión → rechazado y registrado en el log |  
  
   
