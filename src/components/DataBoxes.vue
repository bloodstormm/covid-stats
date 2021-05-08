<template>
    <div class="p-10 sm:p-28 sm:py-10 grid md:grid-cols-2 gap-10">

        <!-- Box 1 -->
        <div class="card">
            <!-- Titulo - Casos -->
            <h3 class="text-3xl font-semibold">Casos</h3>

            <!-- Novos Casos -->
            <div class="text-2xl">
                <span class="text-green-600 font-semibold">Novos casos hoje: </span>
                {{ NumerosComVirgulas(status.NewConfirmed) }}
            </div>

            <!-- Casos Confirmados -->
            <div class="text-2xl">
                <span class="text-green-600 font-semibold">Casos confirmados: </span>
                    {{ NumerosComVirgulas(status.TotalConfirmed) }}
            </div>
        </div>
        
        <!-- Box 2 -->
        <div class="card">
            <!-- Titulo - Mortes -->
            <h3 class="text-3xl font-semibold">Mortes</h3>

            <!-- Novas mortes -->
            <div class="text-2xl">
                <span class="text-green-600 font-semibold">Novas mortes hoje: </span>
                {{ NumerosComVirgulas(status.NewDeaths) }}
            </div>

            <!-- Mortes Confirmadas -->
            <div class="text-2xl">
                <span class="text-green-600 font-semibold">Mortes Confirmadas: </span>
                    {{ NumerosComVirgulas(status.TotalDeaths) }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'DataBoxes',
    props: ['status'],
    methods: {
        // Função para colocar virgula e texto aos números
        NumerosComVirgulas(x) {
            const numeroMil = 1000
            const numeroMi = 999999

            // Formatando texto dos numeros. ex: 2.000 mil ou 2.000.000 mi (MILHOES)
            let texto = x > numeroMil && x < numeroMi ? ' mil' : x > numeroMi ? ' mi' : ''
            
            // Esta linha deixa os números com virgulas
            const numFormatado = x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
            
            return numFormatado + texto;
        }
    }
}
</script>
