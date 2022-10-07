<template>
	<div class="home">
		<div class="relative">
				<img src="https://wallpapercave.com/wp/wp9478214.jpg" alt="Superman Poster" class="block w-full h-72 object-cover md:object-fill relative z-0">
				<div class="details absolute inset-x-0 bottom-0 p-1 z-10">
					<h3 class="mb-4 text-white text-center">Superman</h3>
					<p class="text-white text-center">nfghgj jfkvntku jdknfdkun noiiront undfvioui oifnuuf io judfui iuiruu diuduufoifi jifui 
						hfujgug hghgh.
					</p>
				</div>
		</div>

		<form @submit.prevent="handleSearch()" class="flex flex-col md:flex-row justify-center align-center p-4">
			<input class="block border-0 outline-0 w-full text-black text-xs py-2 px-4 rounded-lg md:pl-2 md:mr-2 duration-300" type="text" placeholder="search here..." v-model="search">
			<input type="submit" value="Search" class="block border-0 outline-0 w-full p-2 mt-2 md:mt-0 rounded-lg text-lg duration-300 uppercase cursor-pointer bg-lime-600">
		</form>
		<MovieLists :movies="movies" @del="deleteMovie"/>
	</div>
</template>

<script>
import MovieLists from '../components/MovieLists.vue'
import { ref } from 'vue'
import env from '@/env';

export default {
	name: 'Home',
	components: { MovieLists },
	setup() {
		const search = ref("");
		const term = 'superman';
		const movies = ref([]);

		const handleSearch = () => {
			if(search.value != "") {
				fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
				.then(resp => resp.json())
				.then(data => {
					movies.value = data.Search.sort((a, b) => b.Year - a.Year);
					console.log(data);
					search.value = "";
				})
			}
		}

		const load = () => {
			fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${term}&type=movie`)
			.then(resp => resp.json())
			.then(data => {
				movies.value = data.Search.sort((a, b) => b.Year - a.Year);
				console.log(data);
			});
		}

		load();

		const deleteMovie = (movie) => {
			movies.value = movies.value.filter((item) => {
				return movie !== item
			})
		}

		return {
			search,
			movies,
			handleSearch,
			deleteMovie,
		}
	}
}

</script>

<style lang="scss">
	.details {
		background-color: rgba(0,0,0,0.6);
	}
	.movie-type {
		background-color: rgba(56,189,248,0.6);
	}
</style>
