<template>
	<div class="home">
		<div class="relative">
			<router-link to="/movie/tt0348150tt0988824">
				<img src="https://wallpapercave.com/wp/wp9478214.jpg" alt="Superman Poster" class="block w-full h-72 object-cover md:object-fill relative z-0">
				<div class="details absolute inset-x-0 bottom-0 p-1 z-10">
					<h3 class="mb-4 text-white text-center">Superman</h3>
					<p class="text-white text-center">nfghgj jfkvntku jdknfdkun noiiront undfvioui oifnuuf io judfui iuiruu diuduufoifi jifui 
						hfujgug hghgh.
					</p>
				</div>
			</router-link>
		</div>

		<form @submit.prevent="handleSearch()" class="flex flex-col md:flex-row justify-center align-center p-4">
			<input class="block border-0 outline-0 w-full text-black text-xs py-2 px-4 rounded-lg md:pl-2 md:mr-2 duration-300" type="text" placeholder="search here..." v-model="search">
			<input type="submit" value="Search" class="block border-0 outline-0 w-full p-2 mt-2 md:mt-0 rounded-lg text-lg duration-300 uppercase cursor-pointer bg-lime-600">
		</form>

		<div class="flex flex-wrap flex-col sm:flex-row my-0 w-full sm:align-center sm:justify-center">
			<div class="movie py-4 px-2" :key="movie.imdbID" v-for="movie in movies">
				<router-link :to="'/movie/' + movie.imdbID" class="movie-link flex flex-col h-full">
					<div class="relative block">
						<img :src="movie.Poster" alt="Movie Poster" class="w-full block object-fit-cover h-72">
						<div class="movie-type absolute px-4 py-2 text-white uppercase bottom-4 left-0 backdrop-opacity-5">{{movie.Type}}</div>
					</div>
					<div class="detail py-4 px-2 rounded-lg">
						<p class="year text-white">{{movie.Year}}</p>
						<h3 class="text-white">{{movie.Title}}</h3>
					</div>
				</router-link>
			</div>
		</div>
	</div>
</template>

<script>
import { ref } from 'vue'
import env from '@/env';

export default {
	setup() {
		const term = 'superman';
		const movies = ref([]);

		const load = () => {
			fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${term}&type=movie`)
			.then(resp => resp.json())
			.then(data => {
				movies.value = data.Search.sort((a, b) => b.Year - a.Year);
				console.log(data);
			});
		}

		load();

		return {
			search,
			movies,
			handleSearch,
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
