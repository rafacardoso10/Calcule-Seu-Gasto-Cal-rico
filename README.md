# Calcule-Seu-Gasto-Cal-rico
Carol Lisita
<label for="idade">Idade:</label>
        <input type="number" id="idade" required>

        <label for="sexo">Sexo:</label>
        <select id="sexo" required>
            <option value="masculino">Masculino</option>
            <option value="feminino">Feminino</option>
        </select>

        <label for="altura">Altura (cm):</label>
        <input type="number" id="altura" required>

        <label for="peso">Peso (kg):</label>
        <input type="number" id="peso" required>

        <label for="nivelAtividade">Nível de Atividade:</label>
        <select id="nivelAtividade" required>
            <option value="sedentario">Sedentário</option>
            <option value="leve">Leve</option>
            <option value="moderado">Moderado</option>
            <option value="ativo">Ativo</option>
            <option value="muito ativo">Muito Ativo</option>
        </select>

        <label for="email">E-mail:</label>
        <input type="email" id="email" required>

        <button type="submit">Calcular</button>
    </form>

    <div class="result" id="resultado"></div>
</div>

<script>
    document.getElementById('caloriasForm').addEventListener('submit', function (event) {
        event.preventDefault();

        const nome = document.getElementById('nome').value;
        const idade = parseInt(document.getElementById('idade').value);
        const sexo = document.getElementById('sexo').value;
        const altura = parseFloat(document.getElementById('altura').value);
        const peso = parseFloat(document.getElementById('peso').value);
        const nivelAtividade = document.getElementById('nivelAtividade').value;
        const email = document.getElementById('email').value;

        function calcularTMB(sexo, peso, altura, idade) {
            if (sexo === 'masculino') {
                return 88.362 + (13.397 * peso) + (4.799 * altura) - (5.677 * idade);
            } else if (sexo === 'feminino') {
                return 447.593 + (9.247 * peso) + (3.098 * altura) - (4.330 * idade);
            }
            return null;
        }

        function calcularGastoCalorico(TMB, nivelAtividade) {
            const fatores = {
                'sedentario': 1.2,
                'leve': 1.375,
                'moderado': 1.55,
                'ativo': 1.725,
                'muito ativo': 1.9
            };
            return TMB * (fatores[nivelAtividade] || 1.2);
        }

        const TMB = calcularTMB(sexo, peso, altura, idade);
        if (TMB !== null) {
            const gastoCalorico = calcularGastoCalorico(TMB, nivelAtividade);
            document.getElementById('resultado').innerHTML = `
                <p>Olá, ${nome}!</p>
                <p>Sua Taxa Metabólica Basal (TMB) é: <strong>${TMB.toFixed(2)} kcal</strong></p>
                <p>Seu gasto total de calorias é: <strong>${gastoCalorico.toFixed(2)} kcal</strong></p>
            `;
        } else {
            document.getElementById('resultado').innerHTML = "<p>Sexo inválido. Por favor, insira 'masculino' ou 'feminino'.</p>";
        }
    });
</script>
