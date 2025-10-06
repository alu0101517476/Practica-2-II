# Practica-2-II

Autor: Eric Bermúdez Hernández

Email: alu0101517476@ull.edu.es

----

# Índice


----

Descripción del trabajo realizado

1. Ejercicio 1: Script colores

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

2. Ejercicio 2: Magnitud vectores

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

3. Ejercicio 3: Mostrar en pantalla el vector con la posición de la esfera.
