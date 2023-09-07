<template>
<v-container fluid>
    <v-row>
        <v-col cols="12" class="d-flex align-center">
            <img src="@/assets/pokedex.png" alt="Pokedex" class="pokedex-image">
            <label class="white--text text-center">SIMPLIFIED POKEDEX</label>
        </v-col>
        <v-col cols="12">
            <v-list class="background-poke">
                <v-list-item class="ml-7" v-for="selectGeneration in generation" :key="selectGeneration.id" @click="get_all(selectGeneration)" :flat="flat">
                    <v-list-item-action>
                        <v-icon :color="selectGeneration.isActive ? 'yellow' : 'white'">mdi-pokeball</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title :class="{ 'yellow--text': selectGeneration.isActive, 'white--text' : !selectGeneration.isActive, }" @click="toggleGeneration(selectGeneration)">{{ selectGeneration.name }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-col>
    </v-row>
</v-container>
</template>

<script>
export default {
    name: 'App',

    data() {
        return {
            isMenuOpen: false,
            generation: {
                i: {
                    id: 1,
                    name: "Generation I",
                    limit: 151,
                    offset: 0,
                    isActive: false
                },
                ii: {
                    id: 2,
                    name: "Generation II",
                    limit: 100,
                    offset: 151,
                    isActive: false
                },
                iii: {
                    id: 3,
                    name: "Generation III",
                    limit: 135,
                    offset: 251,
                    isActive: false
                },
                iv: {
                    id: 4,
                    name: "Generation IV",
                    limit: 107,
                    offset: 386,
                    isActive: false
                },
                v: {
                    id: 5,
                    name: "Generation V",
                    limit: 156,
                    offset: 493,
                    isActive: false
                },
                vi: {
                    id: 6,
                    name: "Generation VI",
                    limit: 72,
                    offset: 649,
                    isActive: false
                },
                vii: {
                    id: 7,
                    name: "Generation VII",
                    limit: 85,
                    offset: 721,
                    isActive: false
                },
                viii: {
                    id: 8,
                    name: "Generation VIII",
                    limit: 99,
                    offset: 806,
                    isActive: false
                },
                ix: {
                    id: 9,
                    name: "Generation IX",
                    limit: 115,
                    offset: 905,
                    isActive: false
                }
            }
        }
    },

    props: {
        flat: {
            type: Boolean,
            default: false,
        },
    },

    methods: {
        get_all(generation) {
            this.$emit("clicked", generation);
            this.isMenuOpen = false;
        },
        toggleMenu() {
            this.isMenuOpen = !this.isMenuOpen;
        },
        toggleGeneration(selectedGeneration) {
            for (const generationKey in this.generation) {
                if (Object.prototype.hasOwnProperty.call(this.generation, generationKey)) {
                    this.generation[generationKey].isActive = false;
                }
            }
            selectedGeneration.isActive = true;
        },

    },
}
</script>

<style>
.background-poke {
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

.pokedex-image {
    max-width: 40%;
    margin-left: 20%;
    display: block;
}
</style>
