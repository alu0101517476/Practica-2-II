# Practica-2-II

Autor: Eric Bermúdez Hernández

Email: alu0101517476@ull.edu.es

----

# Índice

- [Ejercicio 1: Script colores](#1-ejercicio-1-script-colores)
- [Ejercicio 2: Magnitud vectores](#2-ejercicio-2-magnitud-vectores)
- [Ejercicio 3: Mostrar en pantalla el vector con la posición de la esfera](#3-ejercicio-3-mostrar-en-pantalla-el-vector-con-la-posición-de-la-esfera)
- [Ejercicio 4: Mostrar la distancia del cubo y el cilindro de la esfera](#4-ejercicio-4-mostrar-la-distancia-del-cubo-y-el-cilindro-de-la-esfera)
- [Ejercicio 5: Vectores numéricos](#5-ejercicio-5-vectores-numéricos)
- [Ejercicio 6: Velocidad al Cubo](#6-ejercicio-6-velocidad-al-cubo)
- [Ejercicio 7: Tecla H con la función de disparo](#7-ejercicio-7-tecla-h-con-la-función-de-disparo)
- [Ejercicio 8: Movimiento del Cubo con Vector de Dirección y Velocidad](#8-ejercicio-8-movimiento-del-cubo-con-vector-de-dirección-y-velocidad)
- [Ejercicio 9: Movimiento cubo y esfera con las teclas](#9-ejercicio-9-movimiento-cubo-y-esfera-con-las-teclas)
- [Ejercicio 10: Adaptación movimiento ejercicio 4](#10-ejercicio-10-adaptación-movimiento-ejercicio-4)
- [Ejercicio 11: Adaptación movimiento ejercicio 5](#11-ejercicio-11-adaptación-movimiento-ejercicio-5)
- [Ejercicio 12: Modificación ejercicio 11](#ejercicio-12-modificación-ejercicio-11)
- [Ejercicio 13: Avanzar hacia adelante mediante el eje Horizontal](#ejercicio-13-avanzar-hacia-adelante-mediante-el-eje-horizontal)

----

Descripción del trabajo realizado

### **1. Ejercicio 1: Script colores**

Para realizar el ejercicio, he hecho el siguiente script y lo he asignado a un cubo.
Código del Script:

```C#
using UnityEngine;

public class ColorChanger : MonoBehaviour
{
    // Frames de espera antes de cambiar el color (configurable desde el inspector)
    public int framesToWait = 120;

    // Vector con 3 posiciones (R, G, B)
    private float[] colorValues = new float[3];

    // Contador de frames
    private int frameCounter = 0;

    private Renderer objectRenderer;

    void Start()
    {
        // Inicializamos el vector con valores aleatorios entre 0 y 1
        for (int i = 0; i < colorValues.Length; i++)
        {
            colorValues[i] = Random.Range(0.0f, 1.0f);
        }

        // Obtenemos el Renderer del objeto para poder cambiarle el color
        objectRenderer = GetComponent<Renderer>();

        // Aplicamos el color inicial
        ApplyColor();
    }

    void Update()
    {
        frameCounter++;

        // Cuando llegue al número de frames, cambiar un valor del vector
        if (frameCounter >= framesToWait)
        {
            // Elegir una posición aleatoria (0=R, 1=G, 2=B)
            int index = Random.Range(0, 3);

            // Asignar un nuevo valor aleatorio entre 0 y 1
            colorValues[index] = Random.Range(0.0f, 1.0f);

            // Aplicar el nuevo color al objeto
            ApplyColor();

            // Reiniciar contador
            frameCounter = 0;
        }
    }

    // Método para convertir el array en un Color y asignarlo al objeto
    private void ApplyColor()
    {
        Color newColor = new Color(colorValues[0], colorValues[1], colorValues[2]);
        objectRenderer.material.color = newColor;
    }
}

```

A continuación se encuentra un vídeo en el que se demuestra el comportamiento del cubo al asignarle el Script:

![Gif cubo](Img/Ejercicio%201.gif)

### **2. Ejercicio 2: Magnitud vectores**

Para desarrollar el ejercicio, se ha creado un objeto 3D Esfera, a la cual se le ha añadido el color rojo para resaltarla. Posteriormente se ha creado el siguiente Script y se le ha asignado a la Esfera. 
El código del Script es el siguiente:
```C#
using UnityEngine;

public class VectorOperations : MonoBehaviour
{
    // Vectores configurables desde el Inspector
    public Vector3 vectorA = new Vector3(1, 2, 0);
    public Vector3 vectorB = new Vector3(3, 0, 4);


    // Variables para mostrar resultados en el inspector
    [Header("Resultados")]
    public float magnitudA;
    public float magnitudB;
    public float angulo;
    public float distancia;
    public string mayorAltura;

    void Start()
    {
        vectorA = new Vector3(1, 2, 0);
        vectorB = new Vector3(3, 0, 4);
        // a) Magnitud de cada vector
        magnitudA = vectorA.magnitude;
        magnitudB = vectorB.magnitude;

        // b) Ángulo entre ambos (Unity lo da en grados)
        angulo = Vector3.Angle(vectorA, vectorB);

        // c) Distancia entre ambos
        distancia = Vector3.Distance(vectorA, vectorB);

        // d) Vector con mayor altura (componente Y)
        if (vectorA.y > vectorB.y)
            mayorAltura = "El Vector A está a mayor altura.";
        else if (vectorB.y > vectorA.y)
            mayorAltura = "El Vector B está a mayor altura.";
        else
            mayorAltura = "Ambos vectores tienen la misma altura.";

        // Mostrar en consola
        Debug.Log("Magnitud A: " + magnitudA);
        Debug.Log("Magnitud B: " + magnitudB);
        Debug.Log("Ángulo entre A y B: " + angulo + " grados");
        Debug.Log("Distancia entre A y B: " + distancia);
        Debug.Log(mayorAltura);
    }
}

```

El resultado de la ejecución del Script al iniciar el juego es el siguiente:
![Ejercicio 2](Img/Ejercicio2.png)

Como se puede apreciar, en la consola aparecen las magnitudes de A y B, el ángulo que forman los dos vectores, la distancia entre ellos y que vector está a más altura, que en este caso es el A. Para que salgan estos valores en la consola, le hemos asignado valores a los vectores al iniciar la ejecución.

### **3. Ejercicio 3: Mostrar en pantalla el vector con la posición de la esfera.**

Para resolver el ejercicio desarrollé un Script, el cual he añadido a la esfera con el siguiente código que lo que hace es mostrar por consola la posición de la esfera:

```C#
using UnityEngine;

public class ShowSpherePosition : MonoBehaviour
{
    void Update()
    {
        // Opción A (más directa)
        Vector3 position = transform.position;

        // Opción B (equivalente, usando GetComponent<Transform>())
        // Vector3 position = GetComponent<Transform>().position;

        Debug.Log("Posición de la esfera: " + position);
    }
}

```
En la siguiente imagen se encuentra la comprobación de que el Script funciona:

![Ejercicio 3](Img/Ejercicio%203.png)

### **4. Ejercicio 4: Mostrar la distancia del cubo y el cilindro de la esfera**

Para completar el siguiente ejercicio, lo que he hecho ha sido crear un Script con el siguiente código y añadirlo a una nueva esfera que he creado. A esta nueva esfera le he dado el color azul para diferenciarla de la otra que es roja y que ya tenía otro Script añadido.
Código del Script:

```C#
using UnityEngine;

public class DistanceToObjects : MonoBehaviour
{
    // Referencias a los otros objetos (se buscarán por Tag)
    private GameObject cube;
    private GameObject cylinder;

    void Start()
    {
        // Buscar los objetos por sus etiquetas
        cube = GameObject.FindWithTag("cube");
        cylinder = GameObject.FindWithTag("cylinder");

        // Verificar que se encontraron
        if (cube == null || cylinder == null)
        {
            Debug.LogError("No se encontraron los objetos con las etiquetas 'cube' o 'cylinder'.");
            return;
        }

        // Calcular distancias
        float distanceToCube = Vector3.Distance(transform.position, cube.transform.position);
        float distanceToCylinder = Vector3.Distance(transform.position, cylinder.transform.position);

        // Mostrar en consola
        Debug.Log("Distancia entre la esfera y el cubo: " + distanceToCube);
        Debug.Log("Distancia entre la esfera y el cilindro: " + distanceToCylinder);
    }
}

```

En la siguiente imagen se puede comprobar que el Script funciona correctamente al mostrar la distancia entre el cubo y el cilindro con la esfera por consola:

![Ejercicio 4](Img/Ejercicio%204.png)

### **5. Ejercicio 5: Vectores numéricos**

Para realizar el ejercicio, lo primero que he hecho ha sido crear 3 objetos 3D básicos, los cuales son una Esfera, un Cubo y un Cilindro en la misma escena. Después cree 2 Scripts, el primero se llama `DesplazamientoObjeto.cs`, el cual fue asignado a cada uno de estos 3 objetos. Para finalizar cree un EmptyObject al cual le asigné un nuevo script el cual llamé `MarcadorColocacion.cs`. Acto seguido en el inspector del EmptyObject, asigné los 3 objetos 3D básicos de la siguiente forma:
- Objeto A: Sphere Green

- Objeto B: Cube Green

- Objeto C: Cylinder Green

Dentro del mismo componente EmptyObject, configuré los offsets del objeto con valores de ejemplo para que cuando saltara con la barra espaciadora los objetos se movieran de su posición original en función del offset. 
Después para que funcionara todo esto a la hora de saltar con la barra espaciadora, hice lo siguiente:
- Edit --> Project Settings --> Input Manager --> Axes
- Busqué `Jump` y cambie el valor de `Positive Button` a `Space`

Después cambié lo siguiente: 
- Edit --> Project Settings --> Player --> Other Settings --> Active Input Handling
- Cambié el valor a `Both`

A continuación mostraré el código de los Scripts mencionados anteriormente:

`DesplazamientoObjeto.cs`:

```C#
using UnityEngine;

public class DesplazamientoObjeto : MonoBehaviour
{
    [Header("Desplazamiento relativo a la posición original")]
    public Vector3 desplazamiento = Vector3.zero;

    [HideInInspector] public Vector3 posicionOriginal;

    void Awake()
    {
        // Guardamos la posición original al iniciar la escena
        posicionOriginal = transform.position;
    }
}

```

`MarcadorColocacion.cs`:

```C#
using UnityEngine;

public class MarcadorColocacion : MonoBehaviour
{
    [Header("Referencia a los 3 objetos a colocar")]
    public DesplazamientoObjeto objetoA;
    public DesplazamientoObjeto objetoB;
    public DesplazamientoObjeto objetoC;

    [Header("Desplazamientos configurados en el MARCADOR (Vector3)")]
    public Vector3 offsetA = new Vector3(0f, 0f, 0f);
    public Vector3 offsetB = new Vector3(0f, 0f, 0f);
    public Vector3 offsetC = new Vector3(0f, 0f, 0f);

    [Header("Entrada")]
    [Tooltip("Nombre del eje definido en el Input Manager (por defecto 'Jump' = barra espaciadora).")]
    public string ejeSalto = "Jump";
    [Tooltip("Umbral para considerar que la barra está pulsada (0..1).")]
    public float umbral = 0.5f;

    // Para detectar flanco de subida y no disparar cada frame
    private bool estabaPulsado = false;

    void Update()
    {
        float valorEje = Input.GetAxis(ejeSalto); // -> usa el Input Manager (antiguo)
        bool pulsadoAhora = valorEje > umbral;

        // Flanco de subida: pasa de no pulsado -> pulsado
        if (pulsadoAhora && !estabaPulsado)
        {
            ColocarObjetos();
        }

        estabaPulsado = pulsadoAhora;
    }

    private void ColocarObjetos()
    {
        if (objetoA != null)
        {
            // Opción A: usar los offsets definidos en el MARCADOR (recomendado por enunciado)
            objetoA.transform.position = objetoA.posicionOriginal + offsetA;

            // (Opcional) Reflejar el offset del marcador en el componente del objeto:
            objetoA.desplazamiento = offsetA;
        }

        if (objetoB != null)
        {
            objetoB.transform.position = objetoB.posicionOriginal + offsetB;
            objetoB.desplazamiento = offsetB;
        }

        if (objetoC != null)
        {
            objetoC.transform.position = objetoC.posicionOriginal + offsetC;
            objetoC.desplazamiento = offsetC;
        }

        Debug.Log("Objetos colocados según los desplazamientos del marcador.");
    }
}

```

Para ilustrar todos estos cambios, adjunto el siguiente gift en el que se aprecia como al saltar los objetos 3D básicos se mueven de su posición original:

![Ejercicio 5](Img/Ejercicio5.gif)

### **6. Ejercicio 6: Velocidad al Cubo**

Para completar el ejercicio, lo que hice fue crear un cubo y adjuntarle un Script con el siguiente código: 

```C#
using UnityEngine;

public class ArrowSpeedReporter : MonoBehaviour
{
    [Header("Configuración")]
    public float velocidad = 5f;
    public string ejeHorizontal = "Horizontal";
    public string ejeVertical = "Vertical";

    void Update()
    {
        // Leemos los valores de los ejes (sin suavizado)
        float h = Input.GetAxisRaw(ejeHorizontal);
        float v = Input.GetAxisRaw(ejeVertical);
        //  FLECHAS HORIZONTALES
        if (Input.GetKeyDown(KeyCode.RightArrow))
            Debug.Log($"→ Flecha derecha pulsada | Resultado: {velocidad * h}");
        
        if (Input.GetKeyDown(KeyCode.LeftArrow))
            Debug.Log($"← Flecha izquierda pulsada | Resultado: {velocidad * h}");
        //  FLECHAS VERTICALES
        if (Input.GetKeyDown(KeyCode.UpArrow))
            Debug.Log($"↑ Flecha arriba pulsada | Resultado: {velocidad * v}");
        
        if (Input.GetKeyDown(KeyCode.DownArrow))
            Debug.Log($"↓ Flecha abajo pulsada | Resultado: {velocidad * v}");
        //  TECLAS A / D
        if (Input.GetKeyDown(KeyCode.D))
            Debug.Log($"Tecla D pulsada | Resultado: {velocidad * h}");
        
        if (Input.GetKeyDown(KeyCode.A))
            Debug.Log($"Tecla A pulsada | Resultado: {velocidad * h}");
        //  TECLAS W / S
        if (Input.GetKeyDown(KeyCode.W))
            Debug.Log($"Tecla W pulsada | Resultado: {velocidad * v}");
        
        if (Input.GetKeyDown(KeyCode.S))
            Debug.Log($"Tecla S pulsada | Resultado: {velocidad * v}");
    }
}

```

De esta manera, cuando se pusen o bien WASD o las flechas el cubo calcula y muestra por consola `velocidad * valorHorizontal` en caso del eje horizontal y `velocidad * valorVertical` en el del ejer vertical.
En el siguiente vídeo se muestra el funcionamiento del script:

![Ejercicio 6](Img/WASD.gif)

### **7. Ejercicio 7: Tecla H con la función de disparo**

Para completar el ejercicio propuesto, en el `Input Manager`, concretamente en: `Edit → Project Settings → Input Manager → Axes`, auménte el `Size` en `Axes` de 30 a 31 y al último elemento lo llamé `Disparo`. Acto seguido, en `Positive Button` escribí `h`, en `Type` seleccioné `Key or Mouse Button`. Después de eso, añadí al EmptyObject que creé en el ejercicio 5, el siguiente Script:

```C#
using UnityEngine;
using UnityEngine.InputSystem;   // <- necesario para Keyboard.current

public class DisparoNuevo : MonoBehaviour
{
    void Update()
    {
        // Detecta si la tecla H fue presionada en este frame
        if (Keyboard.current.hKey.wasPressedThisFrame)
        {
            Debug.Log("¡Disparo activado con la tecla H!");
        }
    }
}

```

Con esto, al abrir la consola, y ejecutar la escena, si pulso `h` se mostrará el mensaje por consola *¡Disparo activado!*
En la siguiente imagen se demuestra el funcionamiento del Script:

![Ejercicio 7](Img/Ejercicio%207.png)

### **8. Ejercicio 8: Movimiento del Cubo con Vector de Dirección y Velocidad**

Para cumplir con lo que dicta el enunciado, he calculado el desplazamiento mediante la función `Translate(x, y, z)`, siendo `(x, y, z)` las componentes de `moveDirection`. La velocidad inicial es mayor que 1 y el cubo parte de una posición `y = 0`. Para ello, he creado un cubo 3D de color naranja esta vez, al cual le he añadido el siguiente Script:

```C#
using UnityEngine;

public class MoveWithDirection : MonoBehaviour
{
    [Header("Parámetros (editar en el Inspector)")]
    public Vector3 moveDirection = new Vector3(1f, 0f, 0f);
    public float speed = 2f;
    [Tooltip("True = mover en ejes locales del cubo. False = en ejes globales.")]
    public bool useLocalSpace = true;

    [Header("Inicialización")]
    [Tooltip("Colocar el cubo a y=0 al empezar la escena.")]
    public bool forceStartYZero = true;

    void Start()
    {
        if (forceStartYZero)
        {
            Vector3 p = transform.position;
            p.y = 0f;
            transform.position = p;
        }
    }

    void Update()
    {
        Space refSpace = useLocalSpace ? Space.Self : Space.World;

        transform.Translate(
            moveDirection.x * speed * Time.deltaTime,
            moveDirection.y * speed * Time.deltaTime,
            moveDirection.z * speed * Time.deltaTime,
            refSpace
        );
    }
}

```

El desplazamiento aplicado en cada frame es proporcional al vector de dirección, a la velocidad y al tiempo transcurrido entre frames:

$\Delta \mathbf{p} = \mathbf{moveDirection} \cdot \text{speed} \cdot \Delta t$


El uso de `Time.deltaTime` garantiza que el movimiento sea independiente de los FPS.  
El parámetro `useLocalSpace` permite conmutar entre movimiento **local** y global.
A continuación comentaremos todas las situaciones indicadas en el enunciado de la práctica:

**a) Duplicar las coordenadas de la dirección del movimiento**

- **Configuración:**  
  `moveDirection = (1, 0, 0)` → `(2, 0, 0)` con la misma `speed`.

- **Resultado:**  
  El cubo se mueve en la misma dirección, pero el desplazamiento por frame se duplica, por lo que duplicar `moveDirection` multiplica por 2 la magnitud del desplazamiento, manteniendo la trayectoria.  

**b) Duplicar la velocidad manteniendo la dirección del movimiento**

- **Configuración:**  
  `moveDirection = (1, 0, 0)`, `speed = 2` → `speed = 4`.

- **Resultado:**  
  La trayectoria es idéntica al caso anterior, pero el cubo se mueve al doble de velocidad. Por lo tanto, duplicar `speed` o `moveDirection` produce el mismo efecto sobre el **módulo del desplazamiento**.  
  Solo cambia cuánto se avanza por unidad de tiempo, no la dirección.

**c) Velocidad menor que 1**

- **Configuración:**  
  `speed = 0.5`, `moveDirection` constante.

- **Resultado:**  
  El cubo se mueve más lentamente; el desplazamiento por segundo se reduce en proporción directa a `speed`.

**d) Posición inicial del cubo con y > 0**

- **Configuración:**  
  Cubo inicial a `y = 3`, `moveDirection = (1, 0, 0)`.

- **Resultado:**  
  El cubo se desplaza de forma paralela al suelo a la altura `y = 3`.  
  Si `moveDirection` tuviera componente Y, por ejemplo `(1, 1, 0)`, se movería en diagonal ascendente a la posición inicial. Por lo tanto, la altura inicial no altera el modelo de movimiento, solo el plano en el que se produce y queda claro que el componente Y del vector determina si el movimiento incluye ascenso o descenso.

**e) Movimiento relativo al sistema local vs mundial**

- **Configuración:**  
  `useLocalSpace = true` (local) y `false` (global), cubo rotado 45° sobre Y, `moveDirection = (1, 0, 0)`.

- **Resultado:**  
  - En **Space.World**, el cubo se mueve en **+X global**, ignorando su rotación.  
  - En **Space.Self**, el cubo se mueve en su **eje local X**, por lo que la trayectoria en el mundo es **diagonal** respecto al plano global. Por tanto, cambiar entre local y global no altera la magnitud del desplazamiento, pero sí su dirección espacial. El movimiento local sigue la orientación del objeto y el global, la del mundo.

### **9. Ejercicio 9: Movimiento cubo y esfera con las teclas**
Para resolver el ejercicio planteado, lo que hice fue añadir al EmptyObject ya existente y mencionado en anteriores ejercicios el siguiente Script:

```C#
 using UnityEngine;
#if ENABLE_INPUT_SYSTEM
using UnityEngine.InputSystem; // Nuevo Input System (Unity 6.x)
#endif

public class MoveCubeAndSphere : MonoBehaviour
{
    [Header("Referencias")]
    public Transform cube;    // arrastra aquí tu Cubo
    public Transform sphere;  // arrastra aquí tu Esfera

    [Header("Velocidades (u/s)")]
    public float cubeSpeed = 5f;    // velocidad del cubo
    public float sphereSpeed = 5f;  // velocidad de la esfera

    [Header("Espacio de traslación")]
    [Tooltip("Si está activo: mueve según ejes locales del objeto. Si no: ejes globales.")]
    public bool useLocalSpace = false;

    private Space SpaceMode => useLocalSpace ? Space.Self : Space.World;

    void Update()
    {
        // --- CUBO: flechas ---
        if (cube != null)
        {
            Vector2 arrow = ReadArrows(); // x: ←/→  |  y: ↑/↓
            Vector3 delta = new Vector3(arrow.x, arrow.y, 0f) * cubeSpeed * Time.deltaTime;
            cube.Translate(delta, SpaceMode);
        }

        // --- ESFERA: WASD ---
        if (sphere != null)
        {
            Vector2 wasd = ReadWASD(); // x: A/D  |  y: W/S
            Vector3 delta = new Vector3(wasd.x, wasd.y, 0f) * sphereSpeed * Time.deltaTime;
            sphere.Translate(delta, SpaceMode);
        }
    }

    // Lee flechas
    private Vector2 ReadArrows()
    {
        float x = 0f, y = 0f;
#if ENABLE_INPUT_SYSTEM
        if (Keyboard.current != null)
        {
            if (Keyboard.current.leftArrowKey.isPressed)  x -= 1f;
            if (Keyboard.current.rightArrowKey.isPressed) x += 1f;
            if (Keyboard.current.upArrowKey.isPressed)    y += 1f;
            if (Keyboard.current.downArrowKey.isPressed)  y -= 1f;
            return new Vector2(x, y);
        }
#endif
        // Respaldo: Input Manager (Old)
        x = (Input.GetKey(KeyCode.LeftArrow)  ? -1f : 0f) + (Input.GetKey(KeyCode.RightArrow) ? 1f : 0f);
        y = (Input.GetKey(KeyCode.UpArrow)    ?  1f : 0f) + (Input.GetKey(KeyCode.DownArrow)  ? -1f : 0f);
        return new Vector2(Mathf.Clamp(x, -1f, 1f), Mathf.Clamp(y, -1f, 1f));
    }

    // Lee WASD
    private Vector2 ReadWASD()
    {
        float x = 0f, y = 0f;
#if ENABLE_INPUT_SYSTEM
        if (Keyboard.current != null)
        {
            if (Keyboard.current.aKey.isPressed) x -= 1f;
            if (Keyboard.current.dKey.isPressed) x += 1f;
            if (Keyboard.current.wKey.isPressed) y += 1f;
            if (Keyboard.current.sKey.isPressed) y -= 1f;
            return new Vector2(x, y);
        }
#endif
        // Respaldo: Input Manager (Old)
        x = (Input.GetKey(KeyCode.A) ? -1f : 0f) + (Input.GetKey(KeyCode.D) ? 1f : 0f);
        y = (Input.GetKey(KeyCode.W) ?  1f : 0f) + (Input.GetKey(KeyCode.S) ? -1f : 0f);
        return new Vector2(Mathf.Clamp(x, -1f, 1f), Mathf.Clamp(y, -1f, 1f));
    }
}

```

De esta manera, el cubo se moverá respondiendo a las flechas y la Esfera con w-a-s-d, comportandose de la manera que indicaba el enunciado del ejercicio actual. A continuación se pueden apreciar dos gifs, el primero corresponde al movimiento del Cubo que en este caso cree para el ejercicio y que tiene el color amarillo. En el segundo gif, se aprecia lo mismo pero para la Esfera.

![Cubo](Img/Cubo%20Amarillo.gif)


![Esfera](Img/Esfera%20amarilla.gif)

### **10. Ejercicio 10: Adaptación movimiento ejercicio 4**
Para desarrollar el siguiente ejercicio se crearon 3 objetos 3D básicos, un cubo, un cilindro y una esfera, en este caso los 3 de color negro para diferenciarlos. Después, se creó un script en C# el cual se asoció a la esfera con el siguiente código:

```C#
using UnityEngine;

public class SphereDistanceAndDeltaMove : MonoBehaviour
{
    [Header("Referencias (asigna o autodetecta por Tag)")]
    public Transform cube;              // arrástralo desde la escena o déjalo vacío y usa tags
    public Transform cylinder;          // arrástralo desde la escena o déjalo vacío y usa tags
    public string cubeTag = "cube";     // Tag del cubo (si quieres autodetectar)
    public string cylinderTag = "cylinder"; // Tag del cilindro (si quieres autodetectar)

    [Header("Movimiento (proporcional al tiempo)")]
    public Vector3 moveDirection = new Vector3(1f, 0f, 0f); // dirección editable en Inspector
    public float speed = 2f;                                 // unidades/segundo (> 0)
    public bool useLocalSpace = false;                       // true = ejes locales, false = ejes globales

    [Header("Consola (distancias)")]
    [Tooltip("Segundos entre impresiones para no saturar la consola.")]
    public float logEverySeconds = 0.5f;

    private float _logTimer = 0f;

    void Start()
    {
        // Autodetección por Tag si faltan referencias
        if (cube == null)
        {
            GameObject go = GameObject.FindWithTag(cubeTag);
            if (go != null) cube = go.transform;
        }
        if (cylinder == null)
        {
            GameObject go = GameObject.FindWithTag(cylinderTag);
            if (go != null) cylinder = go.transform;
        }

        // Avisos útiles si algo falta
        if (cube == null)
            Debug.LogWarning("[SphereDistanceAndDeltaMove] No se encontró el cubo (asigna 'cube' en Inspector o Tag correcto).");
        if (cylinder == null)
            Debug.LogWarning("[SphereDistanceAndDeltaMove] No se encontró el cilindro (asigna 'cylinder' en Inspector o Tag correcto).");
    }

    void Update()
    {
        // 1) Movimiento proporcional al tiempo transcurrido entre frames
        //    Δp = moveDirection * speed * Δt
        Space space = useLocalSpace ? Space.Self : Space.World;
        Vector3 step = moveDirection * (speed * Time.deltaTime);
        transform.Translate(step, space);

        // 2) Distancias a cubo y cilindro (impresión periódica)
        _logTimer += Time.deltaTime;
        if (_logTimer >= logEverySeconds)
        {
            float dCube = cube != null ? Vector3.Distance(transform.position, cube.position) : float.NaN;
            float dCylinder = cylinder != null ? Vector3.Distance(transform.position, cylinder.position) : float.NaN;

            Debug.Log($"[Esfera] Distancia a Cubo: {dCube:F3} | Distancia a Cilindro: {dCylinder:F3} | Pos: {transform.position}");
            _logTimer = 0f;
        }
    }
}

```
Gracias a este Script, la esfera se mueve de forma continua y uniforme gracias a `Time.deltaTime`, además, la consola muestra periódicamente en la consola la distancia actual entre la esfera, el cubo y el cilindro. Finalmente, el movimiento y las distancias se actualizan en tiempo real durante la ejecución del juego.

En el siguiente vídeo se muestra la ejecución y funcionamiento del Script:

![Ejercicio 10](Img/Ejercicio%2010.gif)

### **11. Ejercicio 11: Adaptación movimiento ejercicio 5**

Para este ejercicio, lo que he hecho ha sido crear un Cubo y una Esfera, en este caso de color morado para que se diferencien y añadirle al cubo un Script con el siguiente código: 

```C#
using UnityEngine;

public class CubeChaseSphere : MonoBehaviour
{
    [Header("Referencia del objetivo")]
    public Transform sphere;            // Arrastra aquí la esfera

    [Header("Parámetros de movimiento")]
    [Min(0.01f)] public float speed = 3f;       // Unidades/segundo (constante)
    [Tooltip("Distancia a la que se considera que el cubo 'ha llegado' al objetivo.")]
    public float stoppingDistance = 0.05f;

    void Update()
    {
        if (sphere == null) return;

        // 1) Vector que une cubo -> esfera
        Vector3 toTarget = sphere.position - transform.position;

        // 2) No modificar altura: proyectamos en el plano XZ (anulamos Y)
        toTarget.y = 0f;

        // 3) Si ya estamos muy cerca, no mover (evita vibración)
        if (toTarget.sqrMagnitude <= stoppingDistance * stoppingDistance)
            return;

        // 4) Normalizar para que la magnitud sea 1 → dirección pura (no depende de la distancia)
        Vector3 dir = toTarget.normalized;

        // 5) Avance constante: velocidad * deltaTime (independiente de FPS)
        Vector3 step = dir * speed * Time.deltaTime;

        // 6) Trasladar en ejes del mundo para respetar la dirección calculada
        transform.Translate(step, Space.World);
    }

#if UNITY_EDITOR
    // Dibuja una línea en la escena para visualizar la dirección
    void OnDrawGizmosSelected()
    {
        if (sphere == null) return;
        Vector3 from = transform.position;
        Vector3 to = sphere.position; to.y = from.y; // misma altura (Y constante)
        Gizmos.color = Color.cyan;
        Gizmos.DrawLine(from, to);
        Gizmos.DrawSphere(to, 0.05f);
    }
#endif
}

```

Después de hacer esto, lo que hice fue seleccionar el cubo y en el inspector en el componente `CubeChaseSphere` que es como se llama el Script añadido al cubo, arrastré la esfera al campo Sphere. De esta manera, cuando ejecutamos el cubo se mueve hasta alcanzar a la esfera, parando en ese momento. 
En el siguiente GIF, se puede comprobar el funcionamiento del Script:

![Ejercicio 11](Img/Ejercicio%2011.gif)

### **Ejercicio 12: Modificación ejercicio 11**

Este ejercicio se resuelve de manera muy similar al ejercicio 11, de manera que en este el cubo rota y mira siempre hacia la esfera. Para resolverlo cree un cubo y una esfera de color Cian y adjunte al cubo el siguient Script:

```C#
using UnityEngine;
#if ENABLE_INPUT_SYSTEM
using UnityEngine.InputSystem; // Soporte para el nuevo Input System (Unity 6.x)
#endif

public class CubeLookAndChase : MonoBehaviour
{
    [Header("Referencias")]
    [Tooltip("Arrastra aquí la esfera que el cubo debe perseguir.")]
    public Transform sphere;

    [Header("Movimiento del CUBO (mirando a la esfera)")]
    [Min(0.01f)] public float cubeSpeed = 3f;          // unidades/segundo (constante)
    [Tooltip("Distancia para considerar que 'llegó' y evitar vibraciones.")]
    public float stoppingDistance = 0.05f;
    [Tooltip("Mantener la altura del cubo (Y) fija durante el movimiento.")]
    public bool keepCubeYLevel = true;

    [Header("Pruebas: movimiento de la ESFERA con WASD")]
    public bool enableSphereWASD = true;
    public float sphereSpeed = 4f;                     // unidades/segundo
    [Tooltip("Movimiento de la esfera en plano XZ (Y fija).")]
    public bool sphereMoveOnXZ = true;

    void Update()
    {
        if (sphere == null) return;

        // ==========================
        // 1) MOVER ESFERA (pruebas)
        // ==========================
        if (enableSphereWASD)
        {
            Vector2 input = ReadWASD(); // x: A/D, y: W/S
            Vector3 deltaSphere;

            if (sphereMoveOnXZ)
            {
                // Plano XZ: W/S = Z, A/D = X  (Y constante)
                deltaSphere = new Vector3(input.x, 0f, input.y) * sphereSpeed * Time.deltaTime;
            }
            else
            {
                // Plano XY: W/S = Y, A/D = X  (Z constante)
                deltaSphere = new Vector3(input.x, input.y, 0f) * sphereSpeed * Time.deltaTime;
            }

            sphere.Translate(deltaSphere, Space.World);
        }

        // ==========================================
        // 2) ORIENTAR CUBO: eje Z+ apunta a la esfera
        // ==========================================
        Vector3 lookTarget = sphere.position;

        if (keepCubeYLevel)
        {
            // Mantener la altura del cubo: igualamos Y del objetivo a la Y del cubo
            lookTarget.y = transform.position.y;
        }

        // LookAt rota el cubo para que su forward (Z+) apunte al objetivo
        transform.LookAt(lookTarget, Vector3.up);

        // ==========================================
        // 3) AVANZAR HACIA LA ESFERA A VELOCIDAD CONSTANTE
        //    - No depende de la distancia (dirección normalizada implícita al usar forward)
        //    - Independiente de FPS (Time.deltaTime)
        //    - Movimiento en espacio LOCAL para usar su Z+ tras el LookAt
        // ==========================================
        // Comprobación de llegada (distancia horizontal si mantuvimos Y)
        Vector3 toTarget = lookTarget - transform.position;
        if (toTarget.sqrMagnitude > (stoppingDistance * stoppingDistance))
        {
            Vector3 stepLocalForward = Vector3.forward * (cubeSpeed * Time.deltaTime);
            transform.Translate(stepLocalForward, Space.Self); // avanzar en Z+ local
        }
    }

    // Lee WASD (nuevo Input System si está disponible; si no, usa Input clásico)
    private Vector2 ReadWASD()
    {
        float x = 0f, y = 0f;
#if ENABLE_INPUT_SYSTEM
        if (Keyboard.current != null)
        {
            if (Keyboard.current.aKey.isPressed) x -= 1f;
            if (Keyboard.current.dKey.isPressed) x += 1f;
            if (Keyboard.current.wKey.isPressed) y += 1f;
            if (Keyboard.current.sKey.isPressed) y -= 1f;
            // Normaliza a -1..1 sin diagonales más rápidas
            Vector2 v = new Vector2(x, y);
            return v.sqrMagnitude > 1f ? v.normalized : v;
        }
#endif
        // Respaldo: Input Manager (Old)
        x = (Input.GetKey(KeyCode.A) ? -1f : 0f) + (Input.GetKey(KeyCode.D) ? 1f : 0f);
        y = (Input.GetKey(KeyCode.W) ?  1f : 0f) + (Input.GetKey(KeyCode.S) ? -1f : 0f);
        Vector2 vv = new Vector2(x, y);
        return vv.sqrMagnitude > 1f ? vv.normalized : vv;
    }

#if UNITY_EDITOR
    // Gizmos para depurar: ver la línea objetivo en la escena
    void OnDrawGizmosSelected()
    {
        if (sphere == null) return;
        Gizmos.color = Color.cyan;
        Vector3 from = transform.position;
        Vector3 to = sphere.position;
        if (keepCubeYLevel) to.y = from.y;
        Gizmos.DrawLine(from, to);
        Gizmos.DrawSphere(to, 0.06f);
    }
#endif
}

```

Después de añadir este Script al cubo, en el inspector del cubo añadí la esfera. En el siguiente GIF se puede apreciar el funcionamiento del Script al ejecutar:

![Ejercicio 12](Img/Ejercicio%2012.gif)

### **Ejercicio 13: Avanzar hacia adelante mediante el eje Horizontal**

Para compltar el ejercicio, cree un cubo 3D de color verde azulado y le añadí el siguiente Script:

```C#
using UnityEngine;

public class RotateAndAdvance : MonoBehaviour
{
    [Header("Entrada")]
    [Tooltip("Eje del Input Manager (Old). Por defecto: Horizontal")]
    public string horizontalAxis = "Horizontal";

    [Header("Movimiento")]
    [Min(0.01f)] public float moveSpeed = 5f;        // unidades/segundo
    [Min(0.01f)] public float rotationSpeed = 120f;  // grados/segundo

    [Header("Opciones")]
    [Tooltip("Bloquear la altura (Y) mientras avanza.")]
    public bool lockY = false;
    public float fixedY = 0f;

    [Tooltip("Dibuja un rayo para ver la dirección forward (Z+).")]
    public bool debugRay = true;
    public float rayLength = 1.5f;

    void Start()
    {
        if (lockY)
        {
            var p = transform.position;
            p.y = fixedY;
            transform.position = p;
        }
    }

    void Update()
    {
        // 1) Leer el eje Horizontal (-1..1) para girar en Y (yaw)
        float h = Input.GetAxis(horizontalAxis); // Left/Right o A/D, según Input Manager
        float yaw = h * rotationSpeed * Time.deltaTime;
        transform.Rotate(0f, yaw, 0f, Space.Self);

        // 2) Avanzar SIEMPRE hacia adelante (Z+) del objeto
        //    OJO: transform.forward es la dirección Z+ del objeto en espacio de mundo.
        Vector3 step = transform.forward * (moveSpeed * Time.deltaTime);
        transform.position += step; // equivalente a Translate(step, Space.World)

        // 3) (Opcional) Mantener Y fija
        if (lockY)
        {
            var p = transform.position;
            p.y = fixedY;
            transform.position = p;
        }

        // 4) Depuración visual
        if (debugRay)
        {
            Debug.DrawRay(transform.position, transform.forward * rayLength, Color.cyan);
        }
    }
}

```

De esta manera, el cubo cuando le das a ad, rota de dirección y avanza hacia esa dirección. En el siguiente vídeo se puede apreciar este comportamiento:

![Ejercicio 13](Img/Ejercicio%2013.gif)