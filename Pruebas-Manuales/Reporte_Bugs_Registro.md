# 🐛 Registro Técnico de Defectos (Bug Reports)

En este documento se detallan los fallos de software identificados, clasificados y documentados durante los ciclos de ejecución de pruebas en el portal de registro.

---

## 🐜 BUG-001: Error de Concurrencia en Redirección de Registro

* **Título del Defecto:** Error de concurrencia (Race Condition) al realizar clics consecutivos en el botón "Registrate".
* **Severidad:** Alta 🔴 | **Prioridad:** Alta ⚡
* **Componente:** Módulo de Autenticación / Registro de Usuarios.
* **Entorno:** Windows 10/11 | Navegadores: Google Chrome, Mozilla Firefox, Safari.
* **URL:** `https://talentolab-test.netlify.app/`

### 📋 Pasos para Reproducir
1. Navegar al portal principal de la aplicación.
2. Hacer clic de manera consecutiva y rápida (múltiples clics) en el botón **"Registrate"**.
3. Observar el comportamiento de la interfaz durante la transición de pantallas.

### 📊 Resultados de la Prueba
* **Resultado Esperado:** El sistema debe mitigar el doble clic (deshabilitando temporalmente el botón tras la primera interacción) y redireccionar limpiamente a la sección de entrada de datos del nuevo usuario.
* **Resultado Obtenido:** El sistema no bloquea las peticiones concurrentes, interrumpe el flujo y despliega un modal genérico de error en pantalla al momento de procesar la redirección.

---

## 🐜 BUG-002: Ausencia de Control de Excepciones de Red (Modo Offline)

* **Título del Defecto:** Falta de manejo de errores y alertas visuales al intentar acceder al flujo de registro sin conexión a internet.
* **Severidad:** Media 🟡 | **Prioridad:** Alta ⚡
* **Componente:** Capa de Red / Interfaz de Usuario (UI).
* **Entorno:** Windows 10/11 | Navegadores: Google Chrome, Mozilla Firefox, Safari.
* **Precondición:** El dispositivo de pruebas debe encontrarse sin acceso a internet (Modo Avión / Red Desconectada).

### 📋 Pasos para Reproducir
1. Abrir el portal principal de la aplicación estando en línea.
2. Interrumpir o desactivar por completo la conexión a internet del dispositivo.
3. Hacer clic en el botón **"Registrate"**.
4. Desplazarse de manera vertical por la Home Page del sitio.

### 📊 Resultados de la Prueba
* **Resultado Esperado:** El sistema debe detectar el estado offline de la sesión, mitigar la acción y desplegar un modal o banner de alerta con el mensaje descriptivo: *"Sin conexión a internet. Verifique su red"*.
* **Resultado Obtenido:** El sistema no maneja la excepción de red; no se muestra ningún síntoma o alerta visual de desconexión, permitiendo la navegación libre por el Home sin advertir al usuario.

---

## 🐜 BUG-003: Latencia Excesiva en la Respuesta del Servidor

* **Título del Defecto:** Degradación de performance y tiempos de respuesta superiores a los 10 segundos en la redirección del flujo de registro.
* **Severidad:** Media 🟡 | **Prioridad:** Media 🟢
* **Componente:** Rendimiento de API / Redirección de Enrutador.
* **Entorno:** Windows 10/11 | Navegadores: Google Chrome, Mozilla Firefox, Safari.

### 📋 Pasos para Reproducir
1. Ingresar al portal web externo.
2. Hacer clic en el botón **"Registrate"**.
3. Cronometrar el tiempo exacto transcurrido desde el evento del clic hasta la carga completa de la pantalla de destino.

### 📊 Resultados de la Prueba
* **Resultado Esperado:** De acuerdo con las heurísticas de usabilidad y performance, el sistema de enrutamiento y respuesta del servidor debe procesar y redireccionar en un umbral óptimo menor a 1.5 segundos.
* **Resultado Obtenido:** El hilo de ejecución se bloquea experimentando una latencia severa, logrando concretar la redirección recién pasados los 10 segundos.
