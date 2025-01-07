<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulação de Frete</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Simulação de Frete</h1>
        <form id="freteForm">
            <label for="origem">Cidade de Origem:</label>
            <input type="text" id="origem" name="origem" required>

            <label for="destino">Cidade de Destino:</label>
            <input type="text" id="destino" name="destino" required>

            <label for="peso">Peso da Carga (kg):</label>
            <input type="number" id="peso" name="peso" required min="1">

            <button type="submit">Calcular Frete</button>
        </form>

        <div id="resultado">
            <h3>Resultado</h3>
            <p id="distancia">Distância: </p>
            <p id="valorFrete">Valor do Frete: </p>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
