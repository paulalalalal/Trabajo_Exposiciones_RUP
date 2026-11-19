# Artefacto 4 · Eslabón de trazabilidad

  -----------------------------------------------------------------------
  Campo                               Valor
  ----------------------------------- -----------------------------------
  **Equipo**                          E2 · Requisitos

  **Módulo**                          Inventario y equipamiento (RPG
                                      Manager)

  **Rol RUP**                         Especificador de requisitos

  **Fase**                            Elaboración

  **Versión**                         1.0 (borrador para iteración 1)

  **Responsable**                     Persona 4

  **Insumos principales**             E1 · Visión y glosario; Artefacto 5
                                      · Requisitos; Artefacto 6 · Modelo
                                      de casos de uso; Artefacto 7 ·
                                      Especificación del CU «Equipar
                                      ítem»

  **Artefactos relacionados**         E3 · Modelo de casos de uso; E4 ·
                                      Diseño/diagrama de secuencia; E6 ·
                                      Casos de prueba (confirmar
                                      nomenclatura exacta con el equipo)
  -----------------------------------------------------------------------

> **Nota de alcance:** este documento se construye con la información
> disponible de los artefactos 5 y 7 y con las referencias al artefacto
> 6 contenidas en ellos. Los detalles específicos de E1, del diagrama
> completo de casos de uso, de E4 y de E6 deben cotejarse con los
> archivos de sus responsables antes de cerrar la versión definitiva.

------------------------------------------------------------------------

## 1. Objetivo

Establecer y documentar la relación entre las necesidades y conceptos
del módulo de Inventario y Equipamiento, los requisitos funcionales y no
funcionales, los casos de uso, sus especificaciones, los elementos de
diseño y las pruebas.

La trazabilidad permite comprobar de dónde surge cada requisito, en qué
funcionalidad del sistema se implementa, qué comportamiento lo
desarrolla y cómo se verificará. También ayuda a detectar requisitos sin
caso de uso o prueba asociada, así como diferencias entre los
artefactos.

## 2. Alcance

Este eslabón cubre los requisitos del módulo **Inventario y
equipamiento** de RPG Manager:

-   Agregar y consultar ítems.
-   Equipar y desequipar ítems.
-   Descartar ítems.
-   Usar pociones.
-   Aplicar límites de espacios y peso.
-   Controlar el acceso al inventario.
-   Guardar los cambios y realizar respaldos.

El caso de uso detallado disponible en esta versión es **CU-05 Gestionar
Inventario**, específicamente su operación **«Equipar ítem»**. También
se referencia **CU-09 Usar poción**, mencionado en el artefacto 5. No se
afirma que todas las operaciones tengan ya una especificación textual
completa.

## 3. Insumos y conceptos de E1

El artefacto 5 indica que los requisitos vienen de la **Visión del
sistema y el Glosario (E1)**. En los requisitos se utilizan los
siguientes conceptos:

  -----------------------------------------------------------------------
  Concepto                            Uso dentro del módulo
  ----------------------------------- -----------------------------------
  **Jugador**                         Actor que consulta y modifica el
                                      inventario de su Personaje.

  **Game Master**                     Actor con acceso de solo lectura;
                                      no puede modificar el inventario.

  **Personaje**                       Entidad del juego a la que
                                      pertenece el inventario.

  **Clase**                           Define compatibilidad de equipo y
                                      límite de peso: Guerrero, Arquero o
                                      Mago.

  **Ítem**                            Elemento almacenado en el
                                      inventario que puede tener tipo,
                                      peso, cantidad y estado de
                                      equipado.

  **Inventario**                      Contenedor de ítems del Personaje,
                                      con un máximo de 30 espacios.

  **Poción**                          Ítem consumible que restaura vida
                                      según RF-INV-05.

  **Ranura**                          Espacio de equipamiento: arma,
                                      armadura o accesorio.
  -----------------------------------------------------------------------

**Reglas de dominio identificadas en los requisitos:**

-   El inventario admite como máximo 30 espacios.
-   El peso máximo depende de la clase: Guerrero 80 kg, Arquero 60 kg y
    Mago 40 kg.
-   Las ranuras de equipo son arma, armadura y accesorio.
-   Un Personaje puede tener como máximo un ítem equipado por ranura.
-   Las clases contempladas son Guerrero, Mago y Arquero.

**Pendiente de cotejo:** confirmar que estos términos y definiciones
coincidan literalmente con el Glosario E1. Este documento registra los
significados utilizados por los artefactos 5 y 7, pero no sustituye el
glosario original.

## 4. Cadena de trazabilidad

La cadena documental del módulo se representa así:

``` text
E1 · Visión del sistema y Glosario
                 |
                 v
Artefacto 5 · Requisitos funcionales y no funcionales
                 |
                 v
Artefacto 6 · Modelo de casos de uso
                 |
                 v
Artefacto 7 · Especificación del CU «Equipar ítem»
                 |
          +------+------+
          |             |
          v             v
E4 · Diseño /       E6 · Casos de
diagrama de         prueba
secuencia
```

La cadena expresa la relación de dependencia y derivación entre
artefactos. El diseño detalla cómo colaboran los elementos del sistema
para realizar el comportamiento; las pruebas comprueban que los
requisitos se cumplen.

En el alcance conocido:

-   **E1 → Artefacto 5:** la visión y el glosario proporcionan el
    contexto, los actores y los conceptos utilizados para formular
    requisitos.
-   **Artefacto 5 → Artefacto 6:** los requisitos se agrupan en
    funcionalidades representadas mediante casos de uso.
-   **Artefacto 6 → Artefacto 7:** el caso de uso CU-05 se detalla
    mediante el flujo «Equipar ítem».
-   **Artefacto 7 → E4:** los pasos y alternativas del caso de uso
    sirven como insumo para representar las interacciones del diseño.
-   **Artefactos 5 y 7 → E6:** los requisitos y sus escenarios
    proporcionan las condiciones que deben convertirse en casos de
    prueba.

> La ubicación y el nombre exactos de E3, E4 y E6 deben ajustarse a la
> estructura real del repositorio. En particular, se debe confirmar si
> E3 identifica el modelo de casos de uso o un artefacto de diseño
> distinto.

## 5. Matriz de trazabilidad de requisitos funcionales

La siguiente matriz relaciona cada requisito funcional del artefacto 5
con el caso de uso, el comportamiento documentado y la verificación
indicada en ese mismo artefacto.

  ------------------------------------------------------------------------------
  ID              Requisito /     Caso de uso    Especificación o Verificación
                  funcionalidad   relacionado    escenario        propuesta en
                                                 disponible       E6
  --------------- --------------- -------------- ---------------- --------------
  **RF-INV-01**   Agregar un ítem CU-05          El artefacto 7   Intentar
                  respetando el   Gestionar      no desarrolla el agregar el
                  máximo de 30    Inventario     flujo de agregar ítem #31; el
                  espacios y el                  ítem.            sistema
                  peso permitido                                  muestra
                  por clase.                                      «Inventario
                                                                  lleno» y no
                                                                  modifica el
                                                                  inventario.

  **RF-INV-02**   Consultar       CU-05          Pasos 1 y 2 del  Con 12 ítems,
                  inventario      Gestionar      flujo básico de  mostrar 12
                  mostrando       Inventario     «Equipar ítem»   filas y el
                  nombre, tipo,                  muestran la      indicador
                  peso, cantidad,                apertura y       «12/30»,
                  estado de                      visualización    además de los
                  equipado, peso                 del inventario.  datos
                  total y                                         requeridos.
                  espacios                                        
                  usados.                                         

  **RF-INV-03**   Equipar un ítem CU-05          Artefacto 7:     Un Mago
                  compatible con  Gestionar      flujo básico,    intenta
                  la clase y      Inventario     pasos 3--7;      equipar una
                  mantener máximo (operación     alternativa A1;  Espada pesada:
                  un ítem por     «Equipar       alternativa A2   la operación
                  ranura.         ítem»).        para ranura      se rechaza, se
                                                 ocupada.         informa el
                                                                  motivo y el
                                                                  inventario no
                                                                  cambia.

  **RF-INV-04**   Descartar un    CU-05          No se suministró Confirmar el
                  ítem previa     Gestionar      una              descarte y
                  confirmación;   Inventario.    especificación   verificar que
                  cancelar no                    textual del      se libera el
                  debe modificar                 flujo de         espacio y el
                  el inventario.                 descarte.        peso; cancelar
                                                                  y verificar
                                                                  que no hay
                                                                  cambios.

  **RF-INV-05**   Usar una        CU-09 Usar     No se suministró Con vida
                  poción,         poción         una              30/100 y una
                  consumir una    (extiende      especificación   poción,
                  unidad y        CU-07, según   textual de este  verificar vida
                  restaurar 50    artefacto 5).  caso de uso.     80/100 y
                  puntos de vida                                  cantidad de
                  sin superar la                                  pociones
                  vida máxima.                                    reducida en
                                                                  una unidad.

  **RF-INV-06**   Desequipar un   CU-05          Artefacto 7:     Intentar
                  ítem y          Gestionar      alternativa A2   desequipar con
                  devolverlo al   Inventario.    contempla la     30/30; se
                  inventario;                    devolución del   rechaza y el
                  rechazar si                    ítem anterior al ítem permanece
                  está en 30/30                  inventario y el  equipado.
                  espacios.                      rechazo cuando   
                                                 está lleno.      
  ------------------------------------------------------------------------------

### 5.1. Lectura de la matriz

La matriz muestra que los seis requisitos funcionales están asociados a
un caso de uso y a una verificación descrita en el artefacto 5. Sin
embargo, la profundidad de la especificación no es igual para todos:

-   RF-INV-03 está desarrollado directamente en el artefacto 7.
-   RF-INV-02 aparece en los pasos iniciales del flujo de «Equipar
    ítem».
-   RF-INV-06 se relaciona con la alternativa A2.
-   RF-INV-01, RF-INV-04 y RF-INV-05 tienen pruebas indicadas en el
    artefacto 5, pero sus flujos detallados no están incluidos en el
    artefacto 7 compartido.

Por tanto, no debe interpretarse que el artefacto 7 especifica por
completo todas las operaciones del inventario.

## 6. Matriz de trazabilidad de requisitos no funcionales

  ---------------------------------------------------------------------------------
  ID               Requisito no    Caso de uso /  Relación con la   Verificación
                   funcional       ámbito         especificación    indicada
                                                  disponible        
  ---------------- --------------- -------------- ----------------- ---------------
  **RNF-INV-01**   Rendimiento:    Operaciones    El artefacto 7    Medir los
                   consulta en ≤ 2 del            indica            tiempos con 30
                   s en el 95 % de inventario.    confirmación de   ítems y 100
                   solicitudes con                equipamiento en ≤ repeticiones;
                   30 ítems;                      1 s en el paso 9. comprobar los
                   equipar o                                        umbrales
                   descartar en ≤                                   definidos.
                   1 s.                                             

  **RNF-INV-02**   Capacidad       CU-05          El artefacto 7    Intentar
                   máxima de 30    Gestionar      contempla el      superar el
                   espacios y      Inventario.    límite de 30      límite de peso;
                   límite de peso                 espacios en A2.   por ejemplo,
                   por clase:                     Los límites de    Mago con 41 kg,
                   Guerrero 80 kg,                peso no aparecen  y verificar el
                   Arquero 60 kg y                desarrollados en  rechazo.
                   Mago 40 kg.                    los flujos        
                                                  compartidos.      

  **RNF-INV-03**   Seguridad: solo Operaciones de Artefacto 7: paso Intentar
                   el Jugador      escritura de   4 y alternativa   modificar el
                   dueño, con      CU-05.         A3.               inventario sin
                   sesión activa,                                   sesión;
                   puede                                            comprobar
                   modificar; el                                    rechazo y
                   Game Master es                                   registro en el
                   de solo lectura                                  log.
                   y los intentos                                   
                   no autorizados                                   
                   se registran.                                    

  **RNF-INV-04**   Persistencia:   Operaciones    Artefacto 7: paso Reiniciar el
                   guardar cambios que modifican  8 guarda el       sistema y
                   en ≤ 1 s,       el inventario  cambio en la base comparar el
                   conservarlos    y servicio de  de datos. El      inventario;
                   tras reinicio y respaldo.      respaldo          verificar que
                   generar                        periódico no se   el respaldo se
                   respaldo en la                 desarrolla en esa genere dentro
                   nube al menos                  especificación.   del periodo
                   cada 24 horas.                                   establecido.
  ---------------------------------------------------------------------------------

### 6.1. Observaciones sobre los RNF

Los requisitos no funcionales establecen condiciones de calidad y
restricciones que también deben comprobarse. No basta con que una
operación exista: debe respetar los tiempos, límites, controles de
acceso y condiciones de persistencia definidos.

El artefacto 7 permite observar directamente el control de sesión, la
persistencia del cambio y el tiempo de confirmación de equipamiento.
Para completar la trazabilidad, los diseños y pruebas deben contemplar
también los límites de peso, el rendimiento de consulta y el respaldo
diario.

## 7. Trazabilidad detallada del caso de uso «Equipar ítem»

**Caso de uso:** CU-05 Gestionar Inventario (operación «Equipar ítem»).\
**Actor principal:** Jugador.\
**Actor secundario:** Game Master, solo lectura.\
**Artefacto fuente:** Artefacto 7 · Especificación de caso de uso:
Equipar ítem.

  -----------------------------------------------------------------------
  Elemento de la          Requisito relacionado   Resultado esperado
  especificación                                  
  ----------------------- ----------------------- -----------------------
  Paso 1: el Jugador abre RF-INV-02               El Jugador accede a la
  el inventario.                                  consulta de su
                                                  inventario.

  Paso 2: el Sistema      RF-INV-02               Se visualiza la
  muestra los datos de                            información requerida
  los ítems y espacios                            del inventario.
  usados.                                         

  Paso 3: el Jugador      RF-INV-03               Se inicia la operación
  selecciona un ítem y                            de equipamiento.
  elige «Equipar».                                

  Paso 4: el Sistema      RNF-INV-03              Solo el propietario
  valida sesión y                                 autorizado puede
  propiedad del                                   modificar el
  Personaje.                                      inventario.

  Paso 5: el Sistema      RF-INV-03               Solo se permite equipar
  verifica compatibilidad                         ítems compatibles.
  de clase.                                       

  Paso 6: el Sistema      RF-INV-03               Se respeta el máximo de
  verifica la ranura.                             un ítem por ranura.

  Paso 7: el Sistema      RF-INV-03               El ítem queda marcado
  equipa el ítem.                                 como equipado.

  Paso 8: el Sistema      RNF-INV-04              El cambio se persiste
  guarda el cambio.                               en la base de datos.

  Paso 9: el Sistema      RNF-INV-01              La operación se
  confirma y muestra el                           confirma dentro del
  inventario actualizado.                         tiempo establecido para
                                                  equipar.
  -----------------------------------------------------------------------

### 7.1. Trazabilidad de flujos alternativos

  -----------------------------------------------------------------------
  Flujo             Condición         Requisito         Respuesta
                                      relacionado       esperada
  ----------------- ----------------- ----------------- -----------------
  **A1 · Ítem       El ítem no        RF-INV-03         Rechazar,
  incompatible**    corresponde a la                    informar el
                    clase del                           motivo y
                    Personaje.                          conservar el
                                                        inventario sin
                                                        cambios.

  **A2 · Ranura     La ranura ya      RF-INV-03 y       Si hay espacio,
  ocupada**         tiene un ítem     RF-INV-06;        devolver el
                    equipado.         RNF-INV-02 por el anterior al
                                      límite de         inventario y
                                      espacios.         continuar; si
                                                        está lleno,
                                                        rechazar y
                                                        conservar el
                                                        equipamiento
                                                        anterior.

  **A3 · Sesión no  No existe sesión  RNF-INV-03        Rechazar,
  válida o usuario  activa o el                         registrar el
  no autorizado**   Jugador no es                       intento y no
                    dueño del                           modificar el
                    Personaje.                          inventario.
  -----------------------------------------------------------------------

## 8. Relación con diseño y pruebas

### 8.1. Hacia E4 · Diseño / diagrama de secuencia

La especificación del caso de uso proporciona los eventos que pueden
representarse en un diagrama de secuencia. Para «Equipar ítem», la
interacción debe reflejar, como mínimo, las responsabilidades descritas
en el flujo:

1.  El Jugador solicita equipar un ítem.
2.  El sistema valida la sesión y la propiedad del Personaje.
3.  El sistema comprueba la compatibilidad entre ítem y clase.
4.  El sistema verifica la disponibilidad de la ranura.
5.  El sistema actualiza el equipamiento y guarda el cambio.
6.  El sistema devuelve una confirmación o el mensaje de rechazo
    correspondiente.

Las alternativas A1, A2 y A3 deben quedar representadas en el diseño
cuando corresponda. La secuencia concreta de objetos, componentes,
servicios o mensajes debe tomarse del diagrama E4 elaborado por el
equipo; no se define aquí una arquitectura que no haya sido
proporcionada.

### 8.2. Hacia E6 · Casos de prueba

Los casos de prueba deben conservar el vínculo con el ID del requisito
que verifican. Los escenarios definidos en el artefacto 5 y en el
artefacto 7 sirven como base:

  -----------------------------------------------------------------------
  ID de prueba      Requisito         Escenario         Resultado
  sugerido                                              esperado
  ----------------- ----------------- ----------------- -----------------
  **CP-INV-01**     RF-INV-01         Agregar el ítem   Se muestra
                                      #31.              «Inventario
                                                        lleno» y no
                                                        cambia el
                                                        inventario.

  **CP-INV-02**     RF-INV-02         Consultar         Se muestran 12
                                      inventario con 12 filas y «12/30»,
                                      ítems.            junto con los
                                                        datos
                                                        solicitados.

  **CP-INV-03**     RF-INV-03         Guerrero equipa   La espada queda
                                      Espada pesada.    equipada y se
                                                        confirma dentro
                                                        del tiempo
                                                        establecido.

  **CP-INV-04**     RF-INV-03         Mago intenta      Se rechaza con
                                      equipar Espada    mensaje y el
                                      pesada.           inventario no
                                                        cambia.

  **CP-INV-05**     RF-INV-04         Descartar un ítem El ítem
                                      y confirmar.      desaparece y se
                                                        liberan espacio y
                                                        peso.

  **CP-INV-06**     RF-INV-05         Usar poción con   La vida pasa a
                                      vida 30/100.      80/100 y se
                                                        consume una
                                                        poción.

  **CP-INV-07**     RF-INV-06         Desequipar con    Se rechaza y el
                                      inventario 30/30. ítem continúa
                                                        equipado.

  **CP-INV-08**     RNF-INV-01        Medir consulta,   Se cumplen los
                                      equipamiento y    tiempos y el
                                      descarte.         porcentaje
                                                        definidos en el
                                                        requisito.

  **CP-INV-09**     RNF-INV-02        Mago intenta      La operación que
                                      superar 40 kg.    excede el límite
                                                        es rechazada.

  **CP-INV-10**     RNF-INV-03        Modificar         Se rechaza la
                                      inventario sin    operación y se
                                      sesión.           registra el
                                                        intento.

  **CP-INV-11**     RNF-INV-04        Reiniciar el      Los datos
                                      sistema y revisar persisten y se
                                      respaldo.         verifica el
                                                        respaldo dentro
                                                        de 24 horas.
  -----------------------------------------------------------------------

> Los códigos CP-INV-01 a CP-INV-11 son identificadores sugeridos para
> organizar las pruebas; deben reemplazarse si E6 ya tiene una
> convención de identificación establecida.

## 9. Ejemplo completo de trazabilidad

**Escenario:** un Mago intenta equipar una Espada pesada.

  -----------------------------------------------------------------------
  Nivel                   Elemento                Descripción
  ----------------------- ----------------------- -----------------------
  Necesidad / regla       E1 · Glosario y reglas  La clase del Personaje
                          del dominio             determina qué ítems
                                                  puede equipar.
                                                  Confirmar la
                                                  formulación exacta en
                                                  E1.

  Requisito               RF-INV-03               El sistema solo permite
                                                  equipar ítems
                                                  compatibles con la
                                                  clase.

  Caso de uso             CU-05 Gestionar         El Jugador ejecuta la
                          Inventario              operación «Equipar
                                                  ítem».

  Especificación          Artefacto 7 · Flujo A1  El sistema detecta
                                                  incompatibilidad,
                                                  rechaza la acción e
                                                  informa el motivo.

  Diseño                  E4                      Debe mostrar la
                                                  validación y la
                                                  respuesta de rechazo,
                                                  según el diagrama del
                                                  equipo.

  Prueba                  E6 / CP-INV-04 sugerida Se ejecuta el escenario
                                                  Mago + Espada pesada.

  Resultado esperado      Verificación            Mensaje de
                                                  incompatibilidad y el
                                                  inventario permanece
                                                  sin modificaciones.
  -----------------------------------------------------------------------

Este recorrido demuestra cómo una regla del dominio se convierte en un
requisito, se incorpora a un caso de uso, se especifica como un flujo
alternativo, se representa en el diseño y finalmente se comprueba
mediante una prueba.

## 10. Observaciones de consistencia y pendientes

Antes de considerar cerrada la trazabilidad, el equipo debe revisar los
siguientes puntos:

1.  **RNF-INV-01 y el paso 9 del artefacto 7:** el RNF establece ≤ 1
    segundo para equipar o descartar y ≤ 2 segundos para consultar en el
    95 % de las solicitudes. El paso 9 del caso de uso menciona ≤ 1
    segundo para la confirmación de equipamiento. Conviene conservar
    explícitos ambos criterios y no aplicar el tiempo de equipamiento a
    la consulta.
2.  **RNF-INV-02 y peso máximo:** la especificación del caso de uso
    «Equipar ítem» menciona el límite de 30 espacios en A2, pero no
    describe una validación del peso máximo por clase. Debe verificarse
    dónde se especificará y probará ese control.
3.  **A2 y RF-INV-06:** A2 describe qué sucede cuando una ranura está
    ocupada y se debe devolver el ítem anterior al inventario. Debe
    confirmarse que el comportamiento de desequipar por separado también
    esté contemplado en el modelo y en su especificación.
4.  **RF-INV-01, RF-INV-04 y RF-INV-05:** el artefacto 5 define sus
    escenarios de prueba, pero no se proporcionó aquí una especificación
    detallada de sus flujos. Se deben localizar o elaborar los detalles
    correspondientes en los artefactos del equipo.
5.  **RNF-INV-04:** el paso 8 del artefacto 7 contempla guardar el
    cambio en la base de datos, pero el respaldo en la nube cada 24
    horas requiere una verificación adicional.
6.  **Identificadores E3, E4 y E6:** confirmar los nombres exactos de
    los archivos y artefactos en el repositorio para que las referencias
    de este documento coincidan con la organización del equipo.
7.  **E1:** revisar el glosario original para asegurar que los actores,
    conceptos y reglas de negocio se nombran de la misma manera en todos
    los documentos.

Estas observaciones no cambian los requisitos acordados: identifican
relaciones que deben quedar explícitas para que la documentación sea
consistente y verificable.

## 11. Conclusiones

-   La trazabilidad conecta las necesidades y conceptos del RPG Manager
    con requisitos, casos de uso, diseño y pruebas.
-   Los identificadores RF-INV y RNF-INV permiten localizar cada
    requisito y seguir su cumplimiento a través de los artefactos.
-   El caso de uso «Equipar ítem» muestra cómo un flujo básico y sus
    alternativas permiten especificar y verificar el comportamiento del
    sistema.
-   Las pruebas deben comprobar tanto las operaciones exitosas como los
    rechazos por incompatibilidad, capacidad, falta de sesión y demás
    restricciones.
-   Mantener actualizados los vínculos entre artefactos facilita
    detectar omisiones, inconsistencias y cambios durante el desarrollo.

------------------------------------------------------------------------

## 12. Referencias a los artefactos del repositorio

  -----------------------------------------------------------------------------------
  Artefacto               Archivo / referencia                Relación con este
                                                              documento
  ----------------------- ----------------------------------- -----------------------
  E1 · Visión y glosario  Confirmar nombre del archivo en el  Fuente de necesidades y
                          repositorio.                        conceptos del dominio.

  Artefacto 5 ·           `05_requisitos.md`                  Define RF-INV-01 a
  Requisitos                                                  RF-INV-06 y RNF-INV-01
                                                              a RNF-INV-04.

  Artefacto 6 · Modelo de `06_modelo_casos_uso.puml` y su     Representa actores y
  casos de uso            imagen `.png` (según la             casos de uso
                          distribución compartida).           relacionados.

  Artefacto 7 ·           `07_especificacion_cu_equipar.md`   Detalla «Equipar ítem»,
  Especificación de CU                                        sus pasos y
                                                              alternativas.

  E4 · Diseño / secuencia Confirmar nombre del archivo.       Debe representar las
                                                              interacciones derivadas
                                                              de la especificación.

  E6 · Casos de prueba    Confirmar nombre del archivo.       Debe verificar los
                                                              requisitos y escenarios
                                                              trazados.
  -----------------------------------------------------------------------------------

**Fin del Artefacto 4 · Eslabón de trazabilidad.**
