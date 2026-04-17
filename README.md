# JS_Tarea2_Intervals

## Autora
Hailie Mountain

## Enunciados

Ejercicio 1: Reloj en tiempo real

Un párrafo con id "reloj" que muestre la hora actual y se actualice automáticamente cada segundo, sin necesidad de pulsar ningún botón. El reloj arranca solo al cargar la página.

setInterval(función, milisegundos)
— ejecuta la función repetidamente cada N ms
— 1000 ms = 1 segundo
— no necesita un botón: se llama directamente
const reloj = document.getElementById("reloj")

function actualizarHora() {
  const ahora = new Date()
  reloj.innerHTML = ahora.toLocaleTimeString()
}

actualizarHora() → llamada inicial (evita el retraso de 1s)
setInterval(actualizarHora, 1000) 

Ejercicio 2: Cuenta atrás con parada

Un párrafo que muestre una cuenta atrás desde 10 hasta 0. Cuando llegue a 0, mostrar "¡Tiempo!" y detener el intervalo. Usar dos botones: "Iniciar" y "Parar".
const intervalo = setInterval(fn, 1000)
clearInterval(intervalo) → lo detiene
— hay que guardar el retorno de setInterval en una variable
— si se llama setInterval varias veces sin limpiar, se acumulan
let cuenta = 10
let intervalo = null

function iniciar() {
  intervalo = setInterval(function() {
    cuenta = cuenta - 1
    resultado.innerHTML = cuenta
    if (cuenta === 0) {
      clearInterval(intervalo)
      resultado.innerHTML = "¡Tiempo!"
    }
  }, 1000)
}
 
 
Ejercicio 3: Texto parpadeante

Un párrafo que alterne entre ser visible e invisible cada 500 ms, creando un efecto de parpadeo. Un botón "Iniciar" y otro "Detener". Usar una variable booleana let visible = true para alternar el estado.
— setInterval puede ejecutarse más rápido que 1 segundo
— 500 ms = medio segundo
— alternar un booleano: visible = !visible
let visible = true
let intervalo = null

intervalo = setInterval(function() {
  visible = !visible
  if (visible) {
    parrafo.style.visibility = "visible"
  } else {
    parrafo.style.visibility = "hidden"
  }
}, 500) 

Ejercicio 4: Barra de progreso animada

Un <div> que actúa como barra de progreso: empieza en 0% de ancho y llega al 100% en 10 segundos. Al llegar al 100%, mostrar "¡Completado!" y detener. Un botón "Iniciar" que también reinicia la barra si ya había llegado al final.
— la barra exterior tiene: width: 300px; border: 1px solid
— la barra interior empieza con: width: 0%; height: 20px; background: green
— cada 100 ms se suma 1% → 100 pasos × 100ms = 10s
— element.style.width = progreso + "%"
let progreso = 0
let intervalo = null
const barra = document.getElementById("barra")

function iniciar() {
  progreso = 0
  clearInterval(intervalo)
  intervalo = setInterval(function() {
    progreso = progreso + 1
    barra.style.width = progreso + "%"
    if (progreso >= 100) {
      clearInterval(intervalo)
      resultado.innerHTML = "¡Completado!"
    }
  }, 100)
}
 
Ejercicio 5: Parar el número
Un número aleatorio entre 1 y 10 cambia cada 200 ms en pantalla. El jugador pulsa "¡Para!" e intenta detenerlo exactamente en el número 7. Si acierta: "¡Ganaste!", si no: "Era el [N], inténtalo de nuevo." Un botón "Jugar de nuevo" reinicia.
— Math.floor(Math.random() * 10) + 1 → número entre 1 y 10
— hay que guardar en una variable el número que se está mostrando
— al pulsar "Para": clearInterval y comprobar si es 7
— este juego combina todo lo aprendido en las tareas anteriores
let numeroActual = 1
let intervalo = null

function jugar() {
  intervalo = setInterval(function() {
    numeroActual = Math.floor(Math.random() * 10) + 1
    display.innerHTML = numeroActual
  }, 200)
}

function parar() {
  clearInterval(intervalo)
  if (numeroActual === 7) {
    resultado.innerHTML = "¡Ganaste!"
  } else {
    resultado.innerHTML = "Era el " + numeroActual + ", inténtalo de nuevo."
  }
}

