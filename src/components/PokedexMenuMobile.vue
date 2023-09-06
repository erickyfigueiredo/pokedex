<template>
<div>
    <v-app-bar app class="white">
        <v-app-bar-nav-icon @click="toggleMenu"></v-app-bar-nav-icon>
    </v-app-bar>

    <div class="menu-container" :class="{ 'menu-open': isMenuOpen }">
        <v-list v-if="isMenuOpen" class="menu-list">
            <v-list-item v-for="selectGeneration in generation" :key="selectGeneration.id" @click="get_all(selectGeneration)" :flat="flat">
                <v-list-item-action>
                    <v-icon color="white">mdi-pokeball</v-icon>
                </v-list-item-action>
                <v-list-item-content>
                    <v-list-item-title class="white--text">{{ selectGeneration.name }}</v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-list>
    </div>
</div>
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

    },

}
</script>

<style scoped>
.menu-container {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 1;
}

.v-app-bar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
}

.menu-open {
    display: block;
}

.menu-list {
    position: absolute;
    top: 60px;
    left: 0;
    width: 100%;
    background: linear-gradient(to bottom right,
            rgba(10, 10, 10, 1),
            rgba(12, 39, 63, 1)) no-repeat center center fixed !important;
    z-index: 999;
}
</style>
