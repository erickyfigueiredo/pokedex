<template>
<v-container>
    <v-chip label :class="filterType(types.type.name)" v-for="types in this.pokemonType.types" :key="types.slot"><strong>{{ get_name(types.type.name) }}</strong></v-chip>
</v-container>
</template>

<script>
export default {
    name: 'App',

    data() {
        return {}
    },
    props: {
        pokemonType: Object,
    },

    mounted() {
        (this.pokemonType);
    },

    methods: {
        filterType(type) {
            switch (type) {
                case 'water':
                    return "mr-2 blue white--text";
                case 'fire':
                    return "mr-2 red white--text";
                case 'grass':
                    return "mr-2 green white--text";
                case 'electric':
                    return "mr-2 yellow";
                case 'flying':
                    return "mr-2 pink white--text";
                case 'poison':
                    return "mr-2 purple white--text";
                case 'bug':
                    return "mr-2 green white--text";
                case 'normal':
                    return "mr-2";
                case 'fighting':
                    return "mr-2 brown white--text";
                case 'ghost':
                    return "mr-2 grey white--text";
                case 'rock':
                    return "mr-2 grey white--text";
                case 'ground':
                    return "mr-2 deep-orange white--text";
                case 'ice':
                    return "mr-2 light-blue white--text";
                case 'psychic':
                    return "mr-2 blue-grey white--text";
                case 'fairy':
                    return "mr-2 teal white--text";
                case 'dragon':
                    return "mr-2 indigo white--text";
                default:
                    return "";
            }
        },
        get_name(name) {
            return name.charAt(0).toUpperCase() + name.slice(1);
        },

    }
}
</script>
