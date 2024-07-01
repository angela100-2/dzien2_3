<template>
    <div>
        <h2 class="text-blue-600">Wpisy na bloga:</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="bg-blue-600 rounded text-white p-4">Odśwież</button>
        </div>
        <div class="grid mx-6 gap-4 my-4">
            <div v-for="(wpis, index) in wpisy" class="drop-shadow-xl bg-stone-300 p-4">
                <p>id: {{ index }}</p>
                <p>{{ wpis }}</p>
                <button @click="deleteWpis(index)" class="bg-blue-600 rounded text-white p-4">Usuń wpis</button>
                <button @click="editWpis(index)" class="bg-blue-600 rounded text-white p-4 m-2">Edytuj wpis</button>
                <input v-model="nowyBlog" type="text" class="border-2 border-blue-600 p-4">
            </div>
        </div>
        <div class="flex justify-center flex-col">
            <input v-model="nowyBlog" type="text" class="border-2 border-blue-600 p-4">
            <button @click="dodajWpis" class="bg-blue-600 rounded text-white p-4">Dodaj wpis</button>
        </div>
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
                await this.pobierzWpisy();
            },
            async deleteWpis(index) {
                await dzien2_3_backend.usun_wpis(index);
                await this.pobierzWpisy();
            },
            async editWpis(index) {
                await dzien2_3_backend.edytuj_wpis(index, this.nowyBlog);
                await this.pobierzWpisy();
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