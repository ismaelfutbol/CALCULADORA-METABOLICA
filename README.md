<!DOCTYPE html>
<html lang="es_mx">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calculadora Metabólica</title>
  <style>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB" crossorigin="anonymous">
    body {
      font-family: Arial, sans-serif;
      background-color #f2f2f2
      padding 20px;
      text-align: center;
    }

    .pantalla {
      display: none;
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      max-width: 400px;
      margin: 0 auto;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    button {
      padding: 10px 20px;
      margin-top: 10px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #0056b3;
    }

    .visible {
      display: block;
    }
  </style>
</head>
<body>
  <!-- 🧾 Pantalla Base -->
  <div id="pantallaBase" class="pantalla visible">
    <h1>Calculadora Metabólica</h1>
    <p>Descubre tu metabolismo basal y necesidades energéticas.</p>
    <button onclick="mostrarPantalla('pantallaFormulario')">Comenzar</button>
  </div>

  <!-- 🧍‍♂️ Pantalla Formulario -->
  <div id="pantallaFormulario" class="pantalla">
    <h2>Ingresa tus datos</h2>
    <form id="formMetabolico">
      <label>Sexo:</label><br>
      <select id="sexo" required>
        <option value="">Selecciona</option>
        <option value="hombre">Hombre</option>
        <option value="mujer">Mujer</option>
      </select><br><br>

      <label>Edad:</label><br>
      <input type="number" id="edad" placeholder="Años" required><br><br>

      <label>Peso (kg):</label><br>
      <input type="number" id="peso" placeholder="Ej. 70" required><br><br>

      <label>Altura (cm):</label><br>
      <input type="number" id="altura" placeholder="Ej. 175" required><br><br>

      <label>¿Haces ejercicio?</label><br>
      <select id="actividad">
        <option value="1.2">Poco o nada</option>
        <option value="1.375">Ligero (1-3 días/semana)</option>
        <option value="1.55">Moderado (3-5 días/semana)</option>
        <option value="1.725">Intenso (6-7 días/semana)</option>
        <option value="1.9">Muy intenso</option>
      </select><br><br>

      <button type="button" onclick="calcular()">Calcular</button>
    </form>
  </div>

  <!-- 📊 Pantalla Resultados -->
  <div id="pantallaResultado" class="pantalla">
    <h2>Resultados</h2>
    <p id="resultadoTexto"></p>
    <button onclick="mostrarMas()">Mostrar más datos</button>
    <div id="masDatos" style="display:none;">
      <h3>Detalles adicionales</h3>
      <p id="detallesTexto"></p>
    </div>
    <button onclick="mostrarPantalla('pantallaFormulario')">Volver</button>
  </div>

  <script>
    function mostrarPantalla(id) {
      document.querySelectorAll('.pantalla').forEach(div => div.classList.remove('visible'));
      document.getElementById(id).classList.add('visible');
    }

    function calcular() {
      const sexo = document.getElementById('sexo').value;
      const edad = parseInt(document.getElementById('edad').value);
      const peso = parseFloat(document.getElementById('peso').value);
      const altura = parseFloat(document.getElementById('altura').value);
      const actividad = parseFloat(document.getElementById('actividad').value);

      if (!sexo || !edad || !peso || !altura) {
        alert('Por favor, completa todos los campos.');
        return;
      }

      // Fórmula Harris-Benedict
      let tmb;
      if (sexo === 'hombre') {
        tmb = 88.36 + (13.4 * peso) + (4.8 * altura) - (5.7 * edad);
      } else {
        tmb = 447.6 + (9.2 * peso) + (3.1 * altura) - (4.3 * edad);
      }

      const calorias = tmb * actividad;

      document.getElementById('resultadoTexto').innerHTML = `
        Tu metabolismo basal (TMB) es de <strong>${tmb.toFixed(2)} kcal/día</strong>.<br>
        Tus necesidades energéticas diarias estimadas son de <strong>${calorias.toFixed(2)} kcal/día</strong>.
      `;

      document.getElementById('detallesTexto').innerHTML = `
        Sexo: ${sexo}<br>
        Edad: ${edad} años<br>
        Peso: ${peso} kg<br>
        Altura: ${altura} cm<br>
        Nivel de actividad: ${actividad}
      `;

      mostrarPantalla('pantallaResultado');
    }

    function mostrarMas() {
      const detalles = document.getElementById('masDatos');
      detalles.style.display = detalles.style.display === 'none' ? 'block' : 'none';
    }
  </script>
</body>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI" crossorigin="anonymous"></script>
</html>
