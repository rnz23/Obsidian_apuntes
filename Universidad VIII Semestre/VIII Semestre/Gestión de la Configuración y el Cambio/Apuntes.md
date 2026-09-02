google.script.run   ->  Para una llamada asíncrona


### División de Código en App Script

├── Config.gs        // Variables globales, IDs de tablas, constantes
├── Models.gs        // Clases e interfaces de datos (POO)
├── Controller.gs    // Funciones backend llamadas desde el HTML (google.script.run)
├── Page.gs          // Funciones para servir el HTML (doGet)
├── Index.html       // Estructura principal del HTML
├── Styles.html      // Hojas de estilo CSS
└── Scripts.html     // JavaScript del lado del cliente
