google.script.run   ->  Para una llamada asíncrona


### División de Código en App Script

├── Config.gs        // Variables globales, IDs de tablas, constantes
├── Models.gs        // Clases e interfaces de datos (POO)
├── Controller.gs    // Funciones backend llamadas desde el HTML (google.script.run)
├── Page.gs          // Funciones para servir el HTML (doGet)
├── Index.html       // Estructura principal del HTML
├── Styles.html      // Hojas de estilo CSS
└── Scripts.html     // JavaScript del lado del cliente



# Actividad 2
La división en tres archivos (`Mascotas.html`, `MascotasJS.html` y `MascotasScript.js`) responde al estándar recomendado para desarrollar aplicaciones web con **Google Apps Script** (HTML Service), aplicando el principio de **separación de responsabilidades** (Separation of Concerns).

A continuación te explico qué contiene cada archivo y por qué se estructuran de esa manera:

---

### 1. `Mascotas.html` (La Estructura y Vista - HTML/Tailwind)

- **¿Qué contiene?**  
    Contiene únicamente el marcado HTML de la interfaz de usuario: la barra superior (navbar), las tarjetas del formulario (sección de Propietario y sección de Mascota), los campos de texto (`input`), botones y los contenedores de los mensajes de alerta.
- **Función:**  
    Es la plantilla principal que Google Apps Script carga cuando entras a la aplicación mediante `doGet()`. Define **cómo se ve** visualmente la página.

---

### 2. `MascotasJS.html` (El Comportamiento del Cliente - Frontend JavaScript)

- **¿Qué contiene?**  
    Es un archivo con etiquetas `<script>` que contiene el código JavaScript que se ejecuta **en el navegador del usuario**.
- **Función:**
    - **Manejo de UI e Interacción:** Escucha cuando el usuario presiona botones, valida que los datos ingresados tengan el formato correcto (DNI de 8 dígitos, teléfono de 9 dígitos, etc.) antes de enviarlos.
    - **Comunicación asíncrona:** Usa `google.script.run` para enviarle los datos al servidor sin recargar la página.
    - **Dinámica visual:** Muestra las alertas de éxito/error, habilita o deshabilita inputs y muestra la lista de vacunas según si seleccionas "Perro" o "Gato".

---

### 3. `MascotasScript.js` (La Lógica del Servidor - Backend Apps Script)

- **¿Qué contiene?**  
    Es un archivo de código Apps Script (`.gs` en el entorno de Google) que corre **en los servidores de Google**.
- **Función:**
    - **Persistencia de Datos:** Conecta la aplicación web con la base de datos en Google Sheets (`SpreadsheetApp.openById`).
    - **Reglas de Negocio Backend:** Comprueba que un DNI no esté duplicado en la hoja de _Propietarios_, o valida que un cliente exista antes de registrarle una mascota.
    - **Seguridad e Integridad:** Guarda la fecha de registro y asigna IDs automáticos a las mascotas (`MAS-xxxx`).

---

### ¿Por qué se dividen de esta forma?

1. **Requisito de Google Apps Script:**  
    Google Apps Script no admite subir archivos `.js` de frontend directamente para incluirlos en el navegador. Por ello, los archivos de JavaScript del cliente se guardan dentro de archivos tipo HTML (como `MascotasJS.html`) y se inyectan en la página principal con la función `<?!= incluir("MascotasJS"); ?>`.
    
2. **Seguridad:**  
    Separar el código del cliente (`MascotasJS.html`) del código del servidor (`MascotasScript.js`) garantiza que las credenciales (como la ID de tu hoja de cálculo) y la lógica de acceso a la base de datos se mantengan ocultas en el servidor y el usuario no pueda modificarlas desde el navegador.
    
3. **Mantenibilidad y Limpieza:**  
    Permite trabajar de forma ordenada: si necesitas cambiar un color o mover un botón modificas `Mascotas.html`, si quieres cambiar las validaciones en pantalla vas a `MascotasJS.html`, y si necesitas modificar las pestañas o columnas de tu hoja de Google Sheets editas `MascotasScript.js`.
	 