<template>
<v-dialog v-if="pokemonData" v-model="show_dialog" width="100%" max-width="600">
    <v-card>
        <v-card-title class="text-h5 blue-grey darken-4 white--text">
            Information
        </v-card-title>
        <v-container>
            <v-row class="d-flex align-center">
                <v-col cols="4" md="4" lg="4">
                    <img class="row-pointer" @click="flip_pokemon()" :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${turn_pokemon}/${pokemonData.id}.png`" :alt="pokemonData.name" width="100%">
                </v-col>
                <v-col cols="8" md="8" lg="8">
                    <h1 class="ml-2">{{ get_name(pokemonData.name) }}</h1>
                    <v-container>
                        <v-chip label class="blue-grey darken-3 white--text"><strong>Height: </strong> {{ pokemonData.height}} ft</v-chip>
                        <v-chip label :class="[mobileClass, 'blue-grey darken-3', 'white--text']"><strong>Weight: </strong> {{ pokemonData.weight }} lb</v-chip>
                    </v-container>
                    <TypeColor :pokemonType="pokemonData"></TypeColor>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12">
                    <v-divider class="my-2"></v-divider>
                    <v-container class="mr-2">
                        <h3 class="mb-1">Abilities</h3>
                        <v-chip label class="mr-2 blue-grey white--text" v-for="skill in pokemonData.abilities" :key="skill.ability.name"> {{ get_name(skill.ability.name) }}</v-chip>
                    </v-container>
                    
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12">
                    <v-divider class="my-2"></v-divider>
                    <div class="text-center d-flex justify-center">
                        <PokedexChart :pokemonData="pokemonData" :pokemonId="pokemonData.id"></PokedexChart>
                    </div>
                </v-col>
            </v-row>
        </v-container>
    </v-card>
</v-dialog>
</template>

<script>
import PokedexChart from './PokedexChart.vue';
import TypeColor from './TypeColor.vue';

export default {
    name: 'App',

    data() {
        return {
            turn_pokemon: "",
            show_dialog: Boolean,
        }
    },

    components: {
        PokedexChart,
        TypeColor
    },

    props: {
        pokemonData: Object,
        show: Boolean,
    },

    mounted() {},

    watch: {
        show() {
            this.show_dialog = true;

        },
    },

    methods: {
        flip_pokemon() {
            if (this.turn_pokemon == "") {
                this.turn_pokemon = "back";
            } else {
                this.turn_pokemon = "";
            }
        },

        get_name(name) {
            return name.charAt(0).toUpperCase() + name.slice(1);
        },
        

    },
    computed: {
        mobileClass() {
            const isMobile = window.innerWidth < 600;
            return isMobile ? 'mt-1' : 'ml-2';
        },
    },
}
</script>
