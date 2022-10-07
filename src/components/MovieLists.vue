<template>
	<div class="flex flex-wrap flex-col sm:flex-row my-0 w-full sm:align-center sm:justify-center">
		<div class="movie py-4 px-2 mt-4 md:w-80" :key="movie.imdbID" v-for="movie in movies">
			<router-link :to="'/movie/' + movie.imdbID" class="movie-link flex flex-col">
				<div class="relative block">
					<img :src="movie.Poster" alt="Movie Poster" class="w-full block object-fit-cover h-72">
					<div class="movie-type absolute px-4 py-2 text-white uppercase bottom-4 left-0 backdrop-opacity-5">{{movie.Type}}</div>
				</div>
				<div class="detail pt-4 px-2 rounded-lg">
					<p class="year text-white">{{movie.Year}}</p>
					<h3 class="text-white">{{movie.Title}}</h3>
				</div>
			</router-link>
			<button @click="delMovie(movie)" class="p-2 mt-2 font-semibold hover:italic text-white rounded-3xl bg-gradient-to-r from-green-400 to-blue-500 hover:from-blue-500 hover:to-green-400">Delete</button>
		</div>
	</div>
</template>

<script>
export default {
	props: ['movies'],
	methods: {
		delMovie(movie) {
			this.$emit('del', movie)
		}
	}
}
</script>

<style>

</style>