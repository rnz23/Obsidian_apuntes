"Index.html"
```
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3 en Raya - JS puro</title>

    <style>
        body { 
            font-family: sans-serif; 
            text-align: center; 
            background-color: #f0f8ff; 
        }

        #tablero { 
            display: grid; 
            grid-template-columns: repeat(3, 100px); 
            gap: 10px; 
            justify-content: center; 
            margin: 20px auto; 
        }

        .celda { 
            width: 100px; 
            height: 100px; 
            background-color: white; 
            border: 2px solid #333; 
            display: flex; 
            align-items: center; 
            justify-content: center; 
            font-size: 2.5rem; 
            font-weight: bold; 
            cursor: pointer;
            transition: background 0.3s;
        }

        .celda:hover { 
            background-color: #e0e0e0; 
        }

        button { 
            padding: 10px 20px; 
            font-size: 1rem; 
            cursor: pointer; 
        }
    </style>
</head>

<body>

    <h1>Juego: 3 en Raya</h1>
    <h2 id="estado">Turno de: X</h2>

    <div id="tablero">
        <div class="celda" data-idx="0"></div>
        <div class="celda" data-idx="1"></div>
        <div class="celda" data-idx="2"></div>
        <div class="celda" data-idx="3"></div>
        <div class="celda" data-idx="4"></div>
        <div class="celda" data-idx="5"></div>
        <div class="celda" data-idx="6"></div>
        <div class="celda" data-idx="7"></div>
        <div class="celda" data-idx="8"></div>
    </div>

    <button id="reiniciar">Reiniciar Juego</button>


    <script src="app_ofuscada.js"></script>

</body>
</html>
```
 

app.js
```
document.addEventListener("DOMContentLoaded", () => {
    let turno = "X";
    let juegoActivo = true;
    let estadoTablero = ["", "", "", "", "", "", "", "", ""];

    const celdas = document.querySelectorAll(".celda");
    const estado = document.getElementById("estado");
    const botonReiniciar = document.getElementById("reiniciar");


    // Evento click en cada celda
    celdas.forEach(celda => {
        celda.addEventListener("click", () => {
            const indice = celda.getAttribute("data-idx");
            if (estadoTablero[indice] === "" && juegoActivo) {
                estadoTablero[indice] = turno;
                // Actualizar UI
                celda.textContent = turno;
                celda.style.color = (turno === "X") ? "#2196F3" : "#F44336";
                if (verificarGanador()) {
                    estado.textContent = "¡El ganador es " + turno + "!";
                    juegoActivo = false;
                }
                else if (!estadoTablero.includes("")) {
                    estado.textContent = "¡Es un empate!";
                    juegoActivo = false;
                }
                else {
                    turno = (turno === "X") ? "O" : "X";
                    estado.textContent = "Turno de: " + turno;
                }
            }
        });
    });

    function verificarGanador() {
        const combinaciones = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],
            [0, 3, 6], [1, 4, 7], [2, 5, 8],
            [0, 4, 8], [2, 4, 6]
        ];

        return combinaciones.some(combinacion => {
            return combinacion.every(index => {
                return estadoTablero[index] === turno;
            });
        });
    }
    // Reiniciar juego

    botonReiniciar.addEventListener("click", () => {
        estadoTablero = ["", "", "", "", "", "", "", "", ""];
        turno = "X";
        juegoActivo = true;

        estado.textContent = "Turno de: X";

        celdas.forEach(celda => {
            celda.textContent = "";
            celda.style.backgroundColor = "white";
        });

    });

});
```
