<template>
<v-app>
    <v-main>
        <v-row :class="{ 'mx-0 flex justify-center': isMobile }">
            <PokedexMenuMobile v-if="isMobile" @clicked="get_all"></PokedexMenuMobile>
            <v-col cols="2" v-if="!isMobile">
                <!-- Menu -->
                <PokedexMenu @clicked="get_all"></PokedexMenu>
            </v-col>
            <v-col cols="10">
                <v-container class="ml-1">
                    <v-container fluid>
                        <v-row>
                            <v-col cols="12">
                                <!-- Search Bar -->
                                <v-text-field v-model="search" label="Search Tool" placeholder="Pokemon name" solo></v-text-field>
                            </v-col>
                        </v-row>
                        <!-- Pokemon List -->
                        <v-row>
                            <v-col cols="6" md="2" v-for="pokemon in filtered_pokemons" :key="pokemon.name">
                                <PokedexCard :pokemon="pokemon" @clicked="show_pokemon" />
                            </v-col>
                        </v-row>
                    </v-container>
                </v-container>
            </v-col>
        </v-row>
        <PokedexDialog v-if="selected_pokemon" :pokemonData="selected_pokemon" :show.sync="show_dialog"></PokedexDialog>
        <button @click="scrollToTop" class="scroll-to-top-button">
            <span class="mdi mdi-arrow-up"></span>
        </button>
    </v-main>
</v-app>
</template>

<script>
import axios from "axios";
import PokedexDialog from "./components/PokedexDialog.vue";
import PokedexCard from "./components/PokedexCard.vue";
import PokedexMenu from "./components/PokedexMenu.vue";
import PokedexMenuMobile from "./components/PokedexMenuMobile.vue";

export default {
    name: 'App',

    data() {
        return {
            pokemons: [],
            search: "",
            selected_pokemon: null,
            show_dialog: false,
        }
    },

    components: {
        PokedexDialog,
        PokedexCard,
        PokedexMenu,
        PokedexMenuMobile
    },

    mounted() {
        this.get_all();
    },

    methods: {
        scrollToTop() {
            window.scrollTo({
                top: 0,
                behavior: 'smooth'
            });
        },
        get_all(generation) {
            if (!generation) {
                generation = {
                    limit: 151,
                    offset: 0
                }
            }
            axios.get(`https://pokeapi.co/api/v2/pokemon/?limit=${generation.limit}&offset=${generation.offset}`).then(response => {
                this.pokemons = response.data.results;
            })
        },

        get_id(pokemon) {
            return Number(pokemon.split("/")[6]);
        },

        show_pokemon(id) {
            axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`).then((response) => {
                this.selected_pokemon = response.data;
                this.show_dialog = !this.show_dialog;
            });
        },

    },

    computed: {
        filtered_pokemons() {
            return this.pokemons.filter((item) => {
                return item.name.includes(this.search);
            })
        },
        isMobile() {
            return window.innerWidth < 1100;
        },
    }

};
</script>

<style>
#app {
    background: linear-gradient(to bottom right,
            rgba(10, 10, 10, 1),
            rgba(12, 39, 63, 1)) no-repeat center center fixed !important;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover !important;
    background-position: center;
    min-height: 100vh;
}

.row-pointer {
    cursor: pointer;
}

.scroll-to-top-button {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    font-size: 24px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background-color 0.3s, transform 0.3s;
}

.scroll-to-top-button:hover {
    background-color: #0056b3;
    transform: scale(1.1);
}
</style>
