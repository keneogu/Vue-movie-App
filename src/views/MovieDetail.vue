<template>
	<div class="movie-detail p-4">
		<h2 class="text-white bottom-4 text-3xl font-semibold">{{movie.title}}</h2>
		<p class="text-white text-sm">{{movie.Year}}</p>
		<img :src="movie.Poster" alt="Movie Poster" class="block max-w-xs">
		<p class="text-white text-sm">{{movie.Plot}}</p>
	</div>
</template>

<script>
	import { ref, onBeforeMount } from "vue";
	import { useRoute } from 'vue-router';
	import env from '@/env.js';

export default {
	setup() {
		const movie = ref({});
		const route = useRoute();

		onBeforeMount(() => {
			fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
			.then(resp => resp.json())
			.then(data => {
				movie.value = data;
			});
		});
		return {
			movie
		}
	}
}
</script>

<style>

</style>
