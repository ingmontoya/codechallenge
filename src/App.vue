<script setup>
import { ref, computed, onBeforeMount } from 'vue';
import CardData from './components/CardData.vue';

const data = ref([]);
const search = ref('hell');
const API_KEY = ref('pLURtkhVrUXr3KG25Gy5IvzziV5OrZGa');
const URL = ref('http://api.giphy.com/v1/gifs/search');
const defaultResults = ref(9);
const pagination = ref(0);
const totalPages = ref(2);

onBeforeMount(() => {
  fetchData();
});

async function fetchData() {
  const response = await fetch(`${URL.value}?api_key=${API_KEY.value}&q=${search.value}`);
  data.value = await response.json();
  pagination.value = data.value.pagination.count;
  totalPages.value = data.value.pagination.total_count / defaultResults.value;
}

function clearResults() {
  data.value = [];
  search.value = '';
}
function loadMore() {
  defaultResults.value += 10;
}
const results = computed(() => data.value.data?.slice(0, defaultResults.value));

</script>

<template>
  <div>
    <v-container class="bg-surface-variant">
      <div class="d-flex align-center">
        <v-text-field density='compact' width="" hide-details="auto" label="Search" v-model="search"
          @input="fetchData"></v-text-field>
        <v-btn @click="clearResults">
          Clear results
        </v-btn>
      </div>
      <v-row no-gutters>

        <v-col v-for="gif in results" :key="gif.id" cols="12" sm="4">
          <v-sheet class="ma-2 pa-2">
            <v-lazy :min-height="200" :options="{ 'threshold': 0.5 }" transition="fade-transition">
              <CardData :image-src="gif.images.preview_gif.url" :title="gif.title" />
            </v-lazy>
          </v-sheet>
        </v-col>
      </v-row>
      <v-row class="d-flex justify-center">
        <v-col class="d-flex justify-center">
          <v-btn @click="loadMore">
            Load more
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>

</template>
