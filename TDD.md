Technical Design Document (TDD)
Hecho por
Daniel Ramirez Chávez
Felix Alejandro Avalos Gama
Cristian Morales Cobian
Materia: Programación de Videojuegos
Maestro: Rodriguez Ortiz Miguel Angel
Fecha
01/10/2025
Documento de Diseño Técnico (TDD)
Proyecto: Guardián del Valle
Versión: 1.0
Fecha: 30 de Septiembre de 2025
Por:
Daniel Ramirez Chávez,
Felix Alejandro Avalos Gama,
Cristian Morales Cobian
Índice
1. Introducción y Objetivos
2. Lista de Características
3. Elección de Game Engine
4. Planeación (Diagrama de Gantt)
5. Diagramas de Alto Nivel
○ 5.1. Arquitectura de Software
○ 5.2. Diseño del Sistema de Combate
○ 5.3. Diagrama de Estados del Jugador
○ 5.4. Diagrama de Gameplay
6. Herramientas de Arte
7. Objetos 3D, Terreno y Escenas
○ 7.1. Pipeline de Creación de Assets 3D
○ 7.2. Creación de Terreno y Entornos
○ 7.3. Gestión de Escenas
8. Detección de Colisiones, Físicas e Interacciones
○ 8.1. Sistema de Colisiones
○ 8.2. Simulación Física
○ 8.3. Sistema de Interacción
9. Lógica de Juego e Inteligencia Artificial
○ 9.1. Game Manager y Lógica de Juego
○ 9.2. Inteligencia Artificial (IA) de Enemigos
10. Networking
11. Audio y Efectos Visuales
○ 11.1. Gestión de Audio
○ 11.2. Efectos Visuales (VFX)
12. Plataforma y Requerimientos
○ 12.1. Plataforma de Destino
○ 12.2. Requerimientos de Software y Hardware
1. Introducción y Objetivos
Este documento detalla la arquitectura técnica, herramientas y metodologías que se
utilizarán para desarrollar el videojuego "Guardián del Valle". El objetivo principal de este
TDD es servir como una guía central para el equipo de programación y arte, asegurando
que todas las decisiones técnicas estén alineadas con los pilares de diseño establecidos
Buscamos crear una base de código modular, escalable y optimizada para la plataforma de
destino (dispositivos móviles), garantizando una experiencia de juego fluida y de alta
calidad.
2. Lista de Características
Las siguientes características clave son la base de nuestras decisiones técnicas:
● Género: Action-RPG en un mundo semi-abierto.
○ Requisito Técnico: Necesidad de un motor capaz de renderizar entornos 3D
extensos y gestionar el streaming de assets de manera eficiente.
● Plataforma: Dispositivos móviles (iOS y Android).
○ Requisito Técnico: El motor y las herramientas deben soportar la compilación
multiplataforma. El rendimiento es crítico; se requiere una estricta gestión de
memoria y optimización de shaders y polígonos.
● Mecánicas de Exploración: Movimiento libre.
○ Requisito Técnico: Se necesita un sistema de control de personaje robusto
(Character Controller) y un motor de físicas que permita la implementación de
estas mecánicas de forma creíble.
● Sistema de Combate Táctico: Basado en estamina, con ataques rápidos/fuertes,
esquiva (dodge) y fijación de objetivo (lock-on).
○ Requisito Técnico: Implementación de una máquina de estados para el
jugador y los enemigos, un sistema de input responsivo y un gestor de
combate que maneje la lógica de daño, estamina y estados alterados.
● Sistema de Puzles Ambientales: Interacción con el entorno para resolver acertijos.
○ Requisito Técnico: Un sistema de interacciones flexible y basado en eventos
que permita al jugador afectar objetos específicos del mundo.
● Progresión del Personaje: Árbol de habilidades y mejora de equipamiento.
○ Requisito Técnico: Una arquitectura de datos para guardar y cargar el
progreso del jugador, incluyendo estadísticas, habilidades desbloqueadas e
inventario. Se usará un formato como JSON o Scriptable Objects para la
definición de datos.
● Estilo Visual: Realismo estilizado con influencias de anime.
○ Requisito Técnico: Se requiere un pipeline de renderizado personalizable
(como URP en Unity) que permita la creación de shaders específicos
(cel-shading, outlines) y efectos de post-procesado para lograr la estética
deseada.
3. Elección de Game Engine
Motor de Juego Seleccionado: Unity 2023.x LTS
Justificación:
1. Soporte Multiplataforma Superior: Unity ofrece un flujo de trabajo consolidado y
altamente probado para compilar y desplegar en iOS y Android desde una única
base de código, lo cual es fundamental para nuestro proyecto.
2. Optimización para Móviles: El Universal Render Pipeline (URP) está diseñado
específicamente para ofrecer gráficos de alta calidad de manera escalable en un
amplio rango de hardware, incluyendo dispositivos móviles. Nos permitirá alcanzar el
estilo visual deseado sin sacrificar el rendimiento.
3. Ecosistema y Asset Store: La Unity Asset Store proporciona una vasta cantidad de
herramientas, plugins y assets pre-construidos que pueden acelerar
significativamente el desarrollo, especialmente en áreas como la IA (Behavior
Designer), la creación de UI y los efectos visuales.
4. Comunidad y Documentación: Unity cuenta con una de las comunidades de
desarrolladores más grandes del mundo, lo que facilita la resolución de problemas y
el aprendizaje. La documentación oficial es extensa y de alta calidad.
5. C# como Lenguaje de Scripting: C# es un lenguaje moderno, potente y de alto
rendimiento que se adapta perfectamente a la creación de arquitecturas de software
complejas y mantenibles, como la que requiere un Action-RPG.
4. Planeación (Diagrama de Gantt)
A continuación, se presenta un cronograma estimado del proyecto, dividido en fases clave.
La duración total estimada es de 18 meses.
Fase Hito Clave Duración
Estimada
Tareas Principales
Fase 1:
Pre-Producc
ión
Documentación
Final
2 semanas - Definición final de TDD y GDD. -
Prototipado de mecánicas centrales
(combate, movimiento). -
Establecimiento del pipeline de arte.
Fase 2:
Producción
Vertical Slice 3 semanas - Desarrollo completo del Core Loop. -
Creación de la primera zona del juego
("El Refugio del Alba" y parte del
"Bosque Susurrante"). -
Implementación de sistemas base (UI,
inventario, IA básica).
Alpha 4 semanas - Implementación de todo el contenido
principal (zonas, misiones, enemigos).
- Sistemas de progresión completos. -
Primera pasada de pulido y balanceo.
Beta 3 semanas - Implementación de sistema de
monetización
- Congelación de características
(Feature Freeze). - Pruebas
exhaustivas (QA), bug fixing. -
Optimización de rendimiento en
dispositivos objetivo.
Fase 3:
Post-Produc
ción
Lanzamiento 1 semana - Preparación para tiendas (App Store,
Google Play). - Marketing y
lanzamiento final. - Monitorización y
corrección de bugs críticos
post-lanzamiento.
5. Diagramas de Alto Nivel
A continuación se mostrarán diferentes diagramas para ilustrar la estructura técnica del
proyecto.
5.1. Arquitectura de Software
El juego se estructurará en torno a un modelo de gestores (Managers) para desacoplar los
sistemas principales.
5.2. Diseño del Sistema de Combate
Este diagrama ilustra la interacción entre las entidades durante un evento de combate.
5.3. Diagrama de Estados del Jugador (FSM - Finite State Machine)
Representa los estados básicos del personaje principal para gestionar su comportamiento.
5.4. Diagrama de Gameplay
Diagrama de flujo simplificado que ilustra un ciclo de juego típico para una de sus misiones
o exploraciones principales.
6. Herramientas de Arte
El pipeline de arte utilizará una combinación de software estándar de la industria y opciones
de código abierto para maximizar la eficiencia y reducir costos.
● Modelado 3D, Rigging y Animación: Blender. Su potencia, versatilidad y
naturaleza gratuita lo hacen ideal para el proyecto. Se establecerán convenciones de
nombrado y exportación (FBX) para una integración fluida con Unity.
● Esculpido de Alta Definición: ZBrush / Blender. Para detalles finos en personajes
y assets importantes que luego serán "bakeados" en mapas de normales.
● Texturizado PBR: Adobe Substance Painter. Es el estándar de la industria para
crear texturas realistas y estilizadas de alta calidad. Se exportarán texturas
compatibles con el shader URP Lit de Unity.
● Arte 2D, Concept Art y UI: Krita / Adobe Photoshop. Para la creación de
conceptos, texturas pintadas a mano e iconos de la interfaz.
● Diseño de UI/UX: Figma. Para prototipar el flujo de pantallas y el diseño de los
menús antes de implementarlos en Unity.
7. Objetos 3D, Terreno y Escenas
7.1. Pipeline de Creación de Assets 3D
1. Modelado: Se crearán modelos Low-Poly en Blender, manteniendo un presupuesto
de polígonos estricto para optimizar el rendimiento en móviles (ej. Personajes:
15k-20k tris, Props: 100-2k tris).
2. UV Unwrapping: Se realizará un mapeo UV eficiente para maximizar la resolución
de las texturas.
3. Texturizado: Creación de texturas en Substance Painter (Albedo, Normal,
Metallic/Smoothness, Ambient Occlusion).
4. Importación a Unity: Los modelos FBX y las texturas se importarán a Unity. Se
crearán Prefabs para cada asset, configurando materiales, colliders y cualquier
script necesario. El uso de Prefabs es crucial para la reutilización y la gestión del
contenido.
7.2. Creación de Terreno y Entornos
El mundo semi-abierto "Valle de Aethel" se construirá utilizando el sistema Terrain de Unity.
● Esculpido: Se esculpirá la topografía base (montañas, valles, ríos).
● Texturizado: Se usarán Terrain Layers con múltiples texturas (hierba, roca, tierra)
para pintar el paisaje.
● Vegetación y Props: Se utilizará el sistema de pintado de árboles y detalles de
Unity para poblar el mundo de manera eficiente. Se empleará LOD (Level of Detail)
de forma agresiva en todos los assets para mantener un framerate estable.
7.3. Gestión de Escenas
El juego se dividirá en múltiples escenas para gestionar la carga de memoria.
● Escena Persistente: Una escena principal que se carga al inicio y nunca se
descarga. Contendrá los gestores (GameManager, UIManager, etc.) y la UI
persistente.
● Escenas de Nivel: Cada zona principal del juego (ej. Zona_BosqueSusurrante,
Zona_CumbresOlvidadas) será una escena independiente.
● Carga Aditiva: Para transiciones fluidas entre zonas, se utilizará la carga y
descarga aditiva de escenas (SceneManager.LoadSceneAsync(Additive)), evitando
pantallas de carga abruptas.
8. Detección de Colisiones, Físicas e Interacciones
8.1. Sistema de Colisiones
Se aprovechará el sistema de físicas 2D/3D integrado de Unity, basado en PhysX.
● Colliders: Se usarán colliders primitivos (Capsule, Box, Sphere) siempre que sea
posible por su eficiencia. Mesh Colliders se reservarán para geometrías complejas y
estáticas.
● Capas de Físicas (Physics Layers): Se configurará una matriz de capas para
definir qué objetos pueden interactuar entre sí. Por ejemplo, la capa Player
colisionará con Environment y Enemy, pero no con la capa Triggers.
● Hitboxes y Hurtboxes: Para el combate, se usarán colliders en modo Trigger en
capas específicas. Los Hitboxes (en las armas del atacante) detectarán colisiones
con los Hurtboxes (en el cuerpo del receptor del daño).
8.2. Simulación Física
● Rigidbodies: Los objetos que necesiten ser movidos por el motor de físicas (ej.
rocas que caen, objetos de puzles) tendrán un componente Rigidbody. El personaje
del jugador NO usará un Rigidbody para su movimiento principal, sino un Character
Controller para un control más preciso y evitar comportamientos físicos no
deseados.
● Raycasting: Se utilizará extensivamente para:
○ Detectar el suelo bajo los pies del jugador.
○ Comprobar la línea de visión de la IA.
○ Detectar objetos interactuables frente al jugador.
8.3. Sistema de Interacción
Se implementará un sistema flexible basado en interfaces de C#.
1. Se definirá una interfaz IInteractable.
2. public interface IInteractable
3. {
4. void Interact();
5. string GetInteractionPrompt();
6. }
7. Cualquier objeto en el juego que pueda ser utilizado (NPCs, cofres, palancas)
implementará esta interfaz.
8. El PlayerController lanzará un Raycast. Si el objeto detectado tiene un componente
que implementa IInteractable, mostrará un aviso en la UI (ej. "Hablar") y permitirá al
jugador activar el método Interact() al presionar un botón.
9. Lógica de Juego e Inteligencia Artificial
9.1. Game Manager y Lógica de Juego
Se utilizará un objeto singleton llamado GameManager para gestionar el estado global del
juego (ej. Playing, Paused, InMenu). Este gestor será responsable de coordinar entre los
diferentes sistemas y manejar la lógica de guardado y carga de partidas a través del
SaveLoadManager.
9.2. Inteligencia Artificial (IA) de Enemigos
La IA se basará en una combinación de Máquinas de Estados Finitas (FSM) y Árboles de
Comportamiento (Behavior Trees).
● Navegación: Se utilizará el sistema NavMesh de Unity para la búsqueda de
caminos (pathfinding) en los terrenos. Todos los entornos se "bakearán" para
generar un NavMesh que los enemigos usarán para moverse.
● FSM: Gestionará los estados básicos del enemigo: Patrolling, Chasing, Attacking,
Fleeing, Stunned.
● Behavior Trees: Para enemigos más complejos (Jefes), se usará un Árbol de
Comportamiento para decidir qué acción tomar. Esto permite una lógica más
modular y compleja que una simple FSM. Ejemplo de un árbol:
○ Raíz
■ Selector: ¿Puedo ver al jugador?
■ Secuencia (Ataque): ¿Estoy en rango de ataque? -> Atacar al
jugador.
■ Secuencia (Persecución): Moverse hacia el jugador.
■ Secuencia (Patrulla): Moverse al siguiente punto de patrulla.
10. Networking
De acuerdo con el GDD, "Guardián del Valle" es una experiencia para un solo jugador. Por
lo tanto, no se implementará una arquitectura de red para el juego multijugador en tiempo
real.
Sin embargo, se considerará la implementación de servicios de backend para:
● Guardado en la Nube: Permitir a los jugadores sincronizar su progreso entre
dispositivos utilizando servicios como iCloud (iOS) o Google Play Games (Android).
● Compras In-App: Conexión segura con las APIs de Apple y Google para gestionar
las transacciones de contenido cosmético.
● Analíticas: Integración de un SDK (como Unity Analytics) para recopilar datos
anónimos sobre el comportamiento del jugador y mejorar el juego.
11. Audio y Efectos Visuales
11.1. Gestión de Audio
Se creará un AudioManager singleton para controlar toda la reproducción de audio.
● Fuentes de Audio: Se usarán pools de AudioSource para reproducir efectos de
sonido de manera eficiente sin tener que instanciar y destruir componentes
constantemente.
● Música: El AudioManager manejará la transición suave entre diferentes pistas
musicales (ej. exploración vs. combate) usando fundidos (crossfades).
● Mezcladores (Audio Mixers): Se utilizarán para agrupar los canales de audio
(Música, SFX, UI) y permitir al jugador ajustar los volúmenes de forma
independiente.
11.2. Efectos Visuales (VFX)
● Shaders Personalizados: Se usará Shader Graph de URP para crear shaders que
logren el estilo visual deseado, como efectos de disolución en enemigos derrotados,
agua estilizada o auras de poder en los artefactos.
● Post-Procesado: Se aplicará una pila de efectos de post-procesado (Bloom, Color
Grading, Vignette) para mejorar la atmósfera y el impacto visual del juego.
12. Plataforma y Requerimientos
12.1. Plataforma de Destino
● Principal: Dispositivos Móviles.
● Sistemas Operativos: iOS y Android.
12.2. Requerimientos de Software y Hardware
● Requerimientos de Software:
○ iOS 14.0 o superior.
○ Android 8.0 (Oreo) o superior, con soporte para Vulkan o OpenGL ES 3.2.
● Requerimientos de Hardware (Mínimos Recomendados):
○ CPU: A12 Bionic (ej. iPhone XR) / Snapdragon 730G o equivalente.
○ RAM: 3 GB.
○ Almacenamiento: 2 GB de espacio libre.
● Dispositivos Objetivo (Para pruebas de rendimiento):
○ Gama Media: iPhone 11, Samsung Galaxy A52.
○ Gama Alta: iPhone 14, Samsung Galaxy S22.
