# Sistema de Economía

# Sistema de Economía

## Índice

1. Introducción
2. Objetivos
3. Funcionalidades
4. Ventajas
5. Requisitos
6. Controlador de Personaje
7. Conclusiones

## 1. Introducción

El sistema de economía es una herramienta que permite llevar un control de los ingresos y gastos de una empresa o persona, de forma organizada y eficiente. Este sistema permite conocer en todo momento el estado financiero y tomar decisiones de manera informada.

## 2. Objetivos

El objetivo principal del sistema de economía es brindar a los usuarios una herramienta que les permita llevar un control de sus ingresos y gastos de manera sencilla y eficiente. Algunos de los objetivos específicos de este sistema son:

- Facilitar el registro de ingresos y gastos.
- Proporcionar información detallada sobre el estado financiero.
- Ayudar en la toma de decisiones de manera informada.

## 3. Funcionalidades

El sistema de economía cuenta con diversas funcionalidades que permiten llevar un control financiero completo. Algunas de las funcionalidades más destacadas son:

- Registro de ingresos y gastos en tiempo real.
- Clasificación de ingresos y gastos por categorías.
- Generación de reportes de ingresos y gastos.
- Establecimiento de metas y presupuestos.
- Monitoreo de la evolución financiera.

## 4. Ventajas

El uso del sistema de economía presenta diversas ventajas para los usuarios. Algunas de las principales ventajas son:

- Ahorro de tiempo en el registro de ingresos y gastos.
- Mayor organización y control financiero.
- Identificación de áreas de oportunidad y mejora.
- Toma de decisiones informadas.
- Mantener un control de los puntos obtenidos por el personaje.

## 5. Requisitos

Para utilizar el sistema de economía se requiere contar con un dispositivo con conexión a internet y un navegador web actualizado. El sistema es compatible con WIndows 10 y 11.

## 6. Controlador de Personaje

```jsx

public class CharacterController : MonoBehaviour
{
    public float speed;
    private Rigidbody2D rigidbody;
    private bool mirandoDerecha = true;
    // Update is called once per frame

    private void Start()
    {
        
        rigidbody = GetComponent<Rigidbody2D>();
    }
    void Update()
    {
        Movimiento();
    }

    void Movimiento()
    {
       float inputMovimientohorizontal = Input.GetAxis("Horizontal");
       

        rigidbody.velocity = new Vector2(inputMovimientohorizontal * speed, rigidbody.velocity.y);

        OrientacionPersonaje(inputMovimientohorizontal);
    }

    void OrientacionPersonaje( float inputMovimientohorizontal)
    {
        if( (mirandoDerecha == true && inputMovimientohorizontal > 0) || (mirandoDerecha == false && inputMovimientohorizontal < 0))
        {
            mirandoDerecha = !mirandoDerecha;
            transform.localScale = new Vector2(-transform.localScale.x, transform.localScale.y);
        }
    }
}
```

Este codigo se encarga de mover al personaje a traves del escenario manipulando su velocidad, interacción con el escenario y orientación al dar la vuelta de izquierda a derecha.

## 7.Coin

```jsx
public class Coin : MonoBehaviour
{
    public int valor = 1;
    public GameManager gameManager;

    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Player"))
        {
            gameManager.SumarPuntos(valor);
            Destroy(this.gameObject);
        }

    }
}
```

Este codigo se encarga de darle valor a las monedas que el jugador puede recolectar en el escenario. Por default el valor es uno, pero desde la interfaz de Unity puede ser editado dandole un valor diferente en caso de ser necesario. Tambien tiene una linea de codigo que compara objetos con la etiqueta player para que estos sean los unicos objetos capaces de recolectar las monedas.

## 8. HUD

```jsx
public class HUD : MonoBehaviour
{
    public GameManager gameManager;
    public TextMeshProUGUI puntos;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        puntos.text = gameManager.PuntosTotales.ToString();
    }
}
```

Este codigo se encarga de tomar los datos proporcionados por el game manager para mostrar los puntos que posee el jugador actualmente.

## 9.GameManager

```jsx
public class GameManager : MonoBehaviour
{
    public int PuntosTotales { get { return puntosTotales; } }
    private int puntosTotales;

    public void SumarPuntos(int puntosASumar)
    {
        puntosTotales += puntosASumar;
        Debug.Log(puntosTotales);
    }
}
```

Este codigo se encarga de recolectar, almacenar y calcular los puntos que el jugador acumule en proporción a cuantas monedas halla recogido.

## 10.Tienda

```jsx
[SerializeField] List<PlantillaInformacionItem> informacionItems;
    [SerializeField] GameObject plantillaObjetoTienda;
    [SerializeField] TextMeshProUGUI textoMonedasTotales;
    // Start is called before the first frame update
    void Start()
    {
        if (PlayerPrefs.HasKey("monedasTotales"))
        {
            PlayerPrefs.SetInt("monedasTotales", 900);
        }
        var plantillaItem = plantillaObjetoTienda.GetComponent<Plantillaitemtienda>();

        foreach (var item in informacionItems)
        {
            plantillaItem.imagen.sprite = item.image;
            plantillaItem.titulo.text = item.titulo;
            plantillaItem.textoPrecio.text = item.precio.ToString();

            Instantiate(plantillaItem, transform);
        }
    }

    // Update is called once per frame
    void Update()
    {
        textoMonedasTotales.text = PlayerPrefs.GetInt("monedasTotales").ToString();
    }
```

Este codigo se encarga de administar la tienda dentro del juego en el que el jugador va a gastar sus monedas a su vez que se las resta de la puntiación total.

## 11.CameraController

```jsx
public float FollowSpeed = 2f;
    public float offset = 1f;
    public Transform target;
    // Update is called once per frame
    void Update()
    {
        Vector3 newPos = new Vector3(target.position.x, target.position.y + offset, -10f);
        transform.position = Vector3.Slerp(transform.position, newPos, FollowSpeed * Time.deltaTime);
    }
```

Este codigo se encraga de que la camara siga al jugador atraves del escenario, tiene configuradas unas variables publicas para que el usuario ajuste la velocidad de seguimiento de la camara.

## 12. Conclusiones

El sistema de economía es una herramienta muy útil para llevar un control financiero eficiente y organizado. Su uso permite conocer en todo momento el estado financiero de una empresa o persona, lo que facilita la toma de decisiones informadas. Además, su facilidad de uso y sus diversas funcionalidades lo convierten en una herramienta indispensable para cualquier persona o empresa que desee llevar un control financiero completo.