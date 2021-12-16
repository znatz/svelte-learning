<script>
	import FancyDiv from './components/FancyDiv.svelte';

	let name = "";

	let firstName = "";
	let lastName = "";

	// reactive value for first name and last name
	$: fullName = `${firstName} ${lastName}`;
	let movies = [
		{"Id":"1","Title":"The Shawshank Redemption","Year":"1994","Rated":"R","Released":"14 Oct 1994","Runtime":"2 h 22 min","Genre":"Crime, Drama","Director":"Frank Darabont","Writer":"Stephen King, Frank Darabont","Actors":"Tim Robbins, Morgan Freeman, Bob Gunton, William Sadler","Plot":"Two imprisoned men bond over a number of years, finding solace and eventual redemption through acts of common decency.","Poster":"https://m.media-amazon.com/images/M/MV5BMDFkYTc0MGEtZmNhMC00ZDIzLWFmNTEtODM1ZmRlYWMwMWFmXkEyXkFqcGdeQXVyMTMxODk2OTU@._V1_QL75_UX190_CR0,0,190,281_.jpg","imdbRating":"9.3","imdbVotes":"1,078,045","imdbID":"tt0111161","Type":"movie","Response":"True","0":{"trailer":"https:\/\/www.youtube.com\/v\/6hB3S9bIaco?version=3&amp;f=videos&amp;app=youtube_gdata"}},
		{"Id":"2","Title":"The Godfather","Year":"1972","Rated":"R","Released":"24 Mar 1972","Runtime":"2 h 55 min","Genre":"Crime, Drama","Director":"Francis Ford Coppola","Writer":"Mario Puzo, Francis Ford Coppola","Actors":"Marlon Brando, Al Pacino, James Caan, Diane Keaton","Plot":"The aging patriarch of an organized crime dynasty transfers control of his clandestine empire to his reluctant son.","Poster":"https://m.media-amazon.com/images/M/MV5BM2MyNjYxNmUtYTAwNi00MTYxLWJmNWYtYzZlODY3ZTk3OTFlXkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_QL75_UY281_CR4,0,190,281_.jpg","imdbRating":"9.2","imdbVotes":"762,332","imdbID":"tt0068646","Type":"movie","Response":"True","0":{"trailer":"https:\/\/www.youtube.com\/v\/sY1S34973zA?version=3&amp;f=videos&amp;app=youtube_gdata"}},
		{"Id":"3","Title":"The Godfather: Part II","Year":"1974","Rated":"R","Released":"20 Dec 1974","Runtime":"3 h 20 min","Genre":"Crime, Drama","Director":"Francis Ford Coppola","Writer":"Francis Ford Coppola, Mario Puzo","Actors":"Al Pacino, Robert De Niro, Robert Duvall, Diane Keaton","Plot":"The early life and career of Vito Corleone in 1920s New York is portrayed while his son, Michael, expands and tightens his grip on his crime syndicate stretching from Lake Tahoe, Nevada to pre-revolution 1958 Cuba.","Poster":"https://m.media-amazon.com/images/M/MV5BMWMwMGQzZTItY2JlNC00OWZiLWIyMDctNDk2ZDQ2YjRjMWQ0XkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_QL75_UY281_CR4,0,190,281_.jpg","imdbRating":"9.0","imdbVotes":"496,772","imdbID":"tt0071562","Type":"movie","Response":"True","0":{"trailer":"https:\/\/www.youtube.com\/v\/qJr92K_hKl0?version=3&amp;f=videos&amp;app=youtube_gdata"}},
	];

	const deleteFrom = (id) => {
		movies = movies.filter(movie => movie.Id !== id);
	};
</script>
<main class="container bg-dark">
	<FancyDiv />
	<h1>Hello {name}!</h1>
	<input bind:value={name} />
	
	<h1>Hello {fullName}!</h1>
	<label for="firstName"></label>
	<input bind:value={firstName} />
	<label for="lastName"></label>
	<input bind:value={lastName} />
	<div class="row mt-3">
		{#each movies as movie (movie.Id)}
			<div class="col-4">
				<div class="card text-dark bg-light mb-3">
					<img src={movie.Poster} class="card-img-top" alt={movie.Title}>
					<div class="card-body">
						<h5 class="card-title">{movie.Title}</h5>
						<p class="card-text">{movie.Plot}</p>
						<button class="btn btn-primary" on:click={()=>deleteFrom(movie.Id)}>Remove</button>
					</div>
				</div>
			</div>
		{:else}
			<div class="col-12">
				<div class="alert alert-info">
					No movies to show.
				</div>
				</div>
		{/each}
	</div>
</main>

<style>
	:global(body) {
		--bs-body-bg: #131212;
	}
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
</style>