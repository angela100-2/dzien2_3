<template>
    <div>
        <button @click="pobierzWpisy">Pobierz wpisy</button>
        siema blog
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
        }
    }
</script>