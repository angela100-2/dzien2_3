<template>
    <div>
        <h2 class="text-blue-600">Wpisy na bloga:</h2>
        <button @click="pobierzWpisy">Odśwież</button>
        {{ wpisy }}
        <input v-model="nowyBlog" type="text">
        <button @click="dodajWpis">Dodaj wpis</button>
    </div>
</template>

<script>
import { dzien2_3_backend } from 'declarations/dzien2_3-backend/index';
    export default {
        data() {
            return {
                wpisy: [],
                nowyBlog: ''
            }
        },
        methods: {
            async dodajWpis() {
                await dzien2_3_backend.dodaj_wpis(this.nowyBlog);
            },
            async pobierzWpisy() {
                this.wpisy = await dzien2_3_backend.odczytaj_wpisy();
            }
        },
        async mounted() {
            this.pobierzWpisy();
        }
    }
</script>