### División de carpetas Proyecto
Aquí tienes una explicación detallada de cada archivo de tu proyecto, qué contiene, qué función cumple y por qué esta estructura es una buena práctica recomendada para el futuro.

---

### 📁 1. Estructura y Rol de Cada Archivo

```mermaid
graph TD
    A["Código.js (Punto de entrada Web App)"] -->|Evalúa plantilla| B["Mascotas.html (Estructura visual)"]
    B -->|incluir('Estilos')| C["Estilos.html (CSS / Diseño)"]
    B -->|incluir('MascotasJS')| D["MascotasJS.html (JavaScript Cliente)"]
    D -->|google.script.run| E["MascotasScript.js (Backend / Google Sheets)"]
    E -->|Lectura / Escritura| F[("Google Sheets (Base de Datos)")]
```

---

### 📄 2. Explicación Archivo por Archivo

#### 1. [Código.js](file:///c:/Users/usuario/AppScript_renzo/C%C3%B3digo.js) (Punto de entrada / Servidor)
* **¿Qué hace?**: Es el archivo principal que Google Apps Script ejecuta cuando alguien entra a la URL de tu aplicación web.
* **Contenido principal**:
  * `doGet(e)`: Carga y evalúa la plantilla `Mascotas.html`, configurando el título y la vista móvil (`viewport`).
  * `incluir(nombreArchivo)`: Función auxiliar imprescindible que permite insertar fragmentos de otros archivos HTML (`Estilos` y `MascotasJS`) dentro de la vista principal.

---

#### 2. [Mascotas.html](file:///c:/Users/usuario/AppScript_renzo/Mascotas.html) (Estructura y Maquetación)
* **¿Qué hace?**: Define el esqueleto y la interfaz visual limpia (sin mezclar código JS complejo ni bloques gigantes de CSS).
* **Contenido principal**:
  * `<?!= incluir("Estilos"); ?>`: En la cabecera `<head>`, inyecta los estilos visuales.
  * **Sección 1 (Formulario de Propietario)**: Inputs con validaciones HTML5 nativas (`maxlength="8"`, `pattern="[0-9]{8}"`, campos `required`) para DNI, nombre, fecha, teléfono, dirección y correo.
  * **Sección 2 (Formulario de Mascota)**: Oculta por defecto. Incluye el selector visual (Perro/Gato), nombre, raza, edad, alergias y el contenedor dinámico para las vacunas.
  * `<?!= incluir("MascotasJS"); ?>`: Al final del `<body>`, inyecta la interactividad JavaScript.

---

#### 3. [MascotasJS.html](file:///c:/Users/usuario/AppScript_renzo/MascotasJS.html) (Lógica del Cliente / Navegador)
* **¿Qué hace?**: Controla todo lo que ocurre en el navegador del usuario en tiempo real antes de enviar datos al servidor.
* **Contenido principal**:
  * **Objeto `Validadores`**: Verifica al instante que el DNI tenga 8 dígitos, el teléfono 9 dígitos y el email tenga formato correcto (ahorrando llamadas innecesarias a Google Sheets).
  * **Manejadores de eventos (`submit`, `change`)**:
    * Al enviar el propietario: bloquea el botón con `"Guardando..."`, llama a `google.script.run.registrarPropietario(datos)` y, al tener éxito, desbloquea la sección de mascota con los datos del dueño vinculado.
    * Al cambiar el tipo de mascota: genera dinámicamente las casillas de vacunas según sea canino o felino.
    * Al enviar la mascota: registra en Google Sheets y permite agregar otra mascota al mismo dueño o reiniciar con *"Cambiar / Nuevo Propietario"*.
  * **Helpers de UI**: `mostrarMensaje()`, `setEstadoBoton()`, `escapar()`.

---

#### 4. [MascotasScript.js](file:///c:/Users/usuario/AppScript_renzo/MascotasScript.js) (Lógica del Servidor / Base de Datos)
* **¿Qué hace?**: Es el backend seguro que interactúa directamente con tu Google Sheets (`SpreadsheetApp`).
* **Contenido principal**:
  * **Capa de acceso a datos**: `obtenerHoja()`, `obtenerFilasDatos()`, `insertarFila()` y `buscarFilaPorValor()`.
  * **Capa de validaciones del servidor**:
    * Comprueba que los datos no vengan vacíos ni manipulados.
    * **Validación de unicidad**: Busca si el DNI ya existe en la hoja *Propietarios*. Si ya existe, detiene la operación y lanza un error descriptivo para no generar duplicados.
  * **Capa de servicios**: `registrarPropietario()` y `registrarMascota()`.

---

#### 5. [Estilos.html](file:///c:/Users/usuario/AppScript_renzo/Estilos.html) (Diseño y CSS)
* **¿Qué hace?**: Contiene todas las reglas de diseño, colores, fuentes, tarjetas y adaptación a móviles (`@media`).
* **Contenido principal**:
  * Variables CSS (`--principal`, `--secundario`, `--error`, `--exito`).
  * Estilos para tarjetas, inputs, botones, mensajes de alerta y el panel de propietario vinculado (`.resumen-seleccion`).

---

### 💡 3. ¿Por qué esta separación es una buena práctica a futuro?

1. **Principio de Responsabilidad Única (Separation of Concerns)**:
   Si necesitas cambiar el color de un botón, solo abres [Estilos.html](file:///c:/Users/usuario/AppScript_renzo/Estilos.html). Si necesitas cambiar una regla de validación de Google Sheets, vas directo a [MascotasScript.js](file:///c:/Users/usuario/AppScript_renzo/MascotasScript.js). No tienes que navegar por un archivo monolítico de más de 1000 líneas.

2. **Reutilización para Nuevos Módulos**:
   Si mañana creas una nueva vista (por ejemplo, `Citas.html` o `HistorialMedico.html`), podrás:
   - Reutilizar [Estilos.html](file:///c:/Users/usuario/AppScript_renzo/Estilos.html) para que toda tu app tenga el mismo diseño profesional sin repetir código CSS.
   - Reutilizar las funciones de búsqueda de datos de [MascotasScript.js](file:///c:/Users/usuario/AppScript_renzo/MascotasScript.js) (como `buscarFilaPorValor`).

3. **Flujo de Trabajo Profesional con `clasp`**:
   `clasp` maneja perfectamente archivos modulares locales. Cuando ejecutas:
   ```bash
   clasp push
   ```
   Clasp sube cada archivo ordenado a Google Apps Script, permitiéndote versionar tu código con Git y trabajar como en cualquier proyecto moderno de desarrollo de software.