document.getElementById("freteForm").addEventListener("submit", function(event) {
    event.preventDefault();

    // Obtendo os valores dos campos
    const origem = document.getElementById("origem").value;
    const destino = document.getElementById("destino").value;
    const peso = parseFloat(document.getElementById("peso").value);

    // Validação básica
    if (!origem || !destino || !peso || peso <= 0) {
        alert("Por favor, preencha todos os campos corretamente.");
        return;
    }

    // Consultando a distância via Google Maps API
    calcularDistancia(origem, destino, function(distancia) {
        if (distancia) {
            const valorFrete = calcularValorFrete(distancia, peso);

            // Exibindo os resultados
            document.getElementById("distancia").textContent = `Distância: ${distancia} km`;
            document.getElementById("valorFrete").textContent = `Valor do Frete: R$ ${valorFrete.toFixed(2)}`;
        } else {
            alert("Não foi possível calcular a distância.");
        }
    });
});

// Função para calcular a distância utilizando Google Maps API
function calcularDistancia(origem, destino, callback) {
    const key = 'SUA_CHAVE_DE_API';  // Substitua com a sua chave de API do Google Maps
    const service = new google.maps.DistanceMatrixService();

    // Requisição para a API de distâncias
    service.getDistanceMatrix(
        {
            origins: [origem],
            destinations: [destino],
            travelMode: 'DRIVING', // Opção de transporte: carro (por estrada)
        },
        function(response, status) {
            if (status === 'OK') {
                // Pegando a distância da resposta
                const distancia = response.rows[0].elements[0].distance.value / 1000;  // Converter metros para quilômetros
                callback(distancia);
            } else {
                console.error('Erro ao calcular distância:', status);
                callback(null);
            }
        }
    );
}

// Função fictícia para calcular o valor do frete
function calcularValorFrete(distancia, peso) {
    // Definindo uma taxa fixa por quilômetro e por peso
    const taxaPorKm = 0.8; // R$ por km
    const taxaPorKg = 0.1; // R$ por kg

    return (distancia * taxaPorKm) + (peso * taxaPorKg);
}
