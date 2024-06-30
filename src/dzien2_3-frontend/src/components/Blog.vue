<template>
    <div>
        <button @click="pobierzWpisy">Pobierz wpisy</button>
        siema blog
        {{ wpisy }}
    </div>
</template>

<script>
import { dzien2_3_backend } from 'declarations/dzien2_3-backend/index';
    export default {
        data() {
            return {
                wpisy: []
            }
        },
        methods: {
            async pobierzWpisy() {
                this.wpisy = await dzien2_3_backend.odczytaj_wpisy();
            }
        }
    }
</script>