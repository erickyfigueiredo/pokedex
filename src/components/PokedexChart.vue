<template>
<div>
    <canvas ref="barChart" :width="mobileClass" height="200"></canvas>
</div>
</template>

<script>
import {
    Chart
} from 'chart.js/auto';

export default {
    data() {
        return {
            chartWidth: 550,
            pokemon: {
                name: '',
                stats: {
                    hp: 0,
                    attack: 0,
                    defense: 0,
                    specialAttack: 0,
                    specialDefense: 0,
                    speed: 0,
                },
            },
        };
    },
    props: {
        pokemonId: Number,
        pokemonData: Object,
    },

    methods: {
        fetchPokemonData() {
            const {
                name,
                stats
            } = this.pokemonData;
            this.pokemon.name = name; // Update pokemon name
            this.pokemon.stats = { // Update all stats
                hp: stats[0].base_stat,
                attack: stats[1].base_stat,
                defense: stats[2].base_stat,
                specialAttack: stats[3].base_stat,
                specialDefense: stats[4].base_stat,
                speed: stats[5].base_stat,
            };

            this.createChart(); // Call chart after load data
        },

        createChart() {
            const ctx = this.$refs.barChart.getContext('2d');
            if (this.chart) {
                this.chart.destroy();
            }
            this.chart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['HP', 'Attack', 'Defense', 'Sp. Atk', 'Sp. Def', 'Speed'],
                    datasets: [{
                        label: 'Base Stats',
                        backgroundColor: [
                            'rgba(255, 0, 0, 0.6)', // HP
                            'rgba(255, 165, 0, 0.6)', // Attack
                            'rgba(0, 128, 255, 0.6)', // Defense
                            'rgba(255, 255, 0, 0.6)', // Sp. Atk
                            'rgba(173, 216, 230, 0.6)', // Sp. Def
                            'rgba(0, 255, 0, 0.6)', // Speed
                        ],
                        borderColor: [
                            'rgba(0, 0, 0, 1)',
                        ],
                        borderWidth: 2,
                        borderRadius:4,
                        data: Object.values(this.pokemon.stats),
                    }, ],
                },
                options: {
                    indexAxis: 'y',
                    scales: {
                        x: {
                            grid: {
                                display: false,
                            },
                        },
                        y: {
                            grid: {
                                display: false,
                            },
                            beginAtZero: true,
                            max: 100,
                        },
                    },
                    responsive: false,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false,
                        },
                        title: {
                            display: true,
                            text: 'Base Stats',
                            font: {
                                size: 16,
                            },
                        },
                    },
                },
            });
        },
    },

    watch: {
        pokemonData(newVal) {
            if (newVal) {
                this.fetchPokemonData();
            }
        },
    },

    mounted() {
        // Inicialize o gráfico quando o componente for montado
        this.fetchPokemonData();
    },

    computed: {
        mobileClass() {
            // Verifique se a largura da janela é menor que 600 pixels (ou seu limite desejado para dispositivos móveis)
            const isMobile = window.innerWidth < 600; // Ajuste o limite conforme necessário
            return isMobile ? '300' : '550'; // Adicione 'ml-2' apenas em dispositivos móveis
        },
    },
};
</script>
