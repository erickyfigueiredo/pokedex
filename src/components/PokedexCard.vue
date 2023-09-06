<template>
<v-card @click="show_pokemon(get_id(pokemon))" :flat="flat">
    <v-container>
        <v-row class="mx-0 flex justify-center">
            <img class="row-pointer" v-if="!isImageLoaded" src="https://i.gifer.com/ZKZg.gif" alt="Loading" width="80%" />
            <img class="row-pointer" :src="pokemonImage" :alt="pokemon.name" width="80%" v-else />
            <h2 class="text-center resize-text">{{ get_name(pokemon.name) }}</h2>
        </v-row>
    </v-container>
</v-card>
</template>

<script>
export default {
    name: 'App',

    data() {
        return {
            isImageLoaded: false,
            pokemonImage: '',
        }
    },

    props: {
        pokemon: Object,
        flat: {
            type: Boolean,
            default: false,
        },
    },

    methods: {
        get_id(pokemon) {
            return Number(pokemon.url.split("/")[6]);
        },

        get_name(pokemon) {
            return pokemon.charAt(0).toUpperCase() + pokemon.slice(1);
        },

        show_pokemon(id) {
            this.$emit("clicked", id);
        },
        preloadImage() {
            const image = new Image();
            image.src = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/" + this.get_id(this.pokemon) + ".png";
            image.onload = () => {
                this.pokemonImage = image.src;
                this.isImageLoaded = true;
            };
        },
        onImageLoad() {
            this.isImageLoaded = true;
        },
    },
    watch: {
        pokemon: {
            handler() {
                this.isImageLoaded = false;
                this.pokemonImage = '';
                this.preloadImage();
            },
            deep: true,
        },
    },
    mounted() {
        this.preloadImage();
    },
}
</script>

<style>
.resize-text {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}
</style>
