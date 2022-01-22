<script>
	import { onMount } from "svelte";
    
	let movies = [];
	let pagination = null;
  
	const getMovies = async () => {
	  await fetch(`http://localhost:3000/movies`)
		.then((res) => res.json())
		.then((data) => {
		  movies = data.data;
		  pagination = data.pagination;
		})
		.catch((err) => console.log(err));
	};
	onMount(async () => getMovies());
	
  </script>


  <main class="text-center">
	<div class="container">
		<h1>List of movies</h1>
		<ul class="list-group">
			{#each movies as movie}
			<li href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center">
			  <div >
				<b>Title :</b>{movie.title}
				<p>
				
			<b>Genre :</b>
					{#each movie.genres as genre}
					  <span>{genre}</span>,
					{/each}
					<br />
				<b>Year: </b><span>{movie.year}</span>
				</p>
			  </div>
			  <div class="image-parent">
				<img src={movie.poster} class="card-img-top" alt={movie.title}  style="max-width: 50px; max-height:50px;"/>
			  </div>
			</li>
			{/each}
		  </ul>
	</div>



  </main>
  
  <style>
	main {
	  text-align: center;
	  padding: 1em;
	  max-width: 240px;
	  margin: 0 auto;
	}
  
	h1 {
	  color: #ff3e00;
	  text-transform: uppercase;
	  font-size: 4em;
	  font-weight: 100;
	}
  
	@media (min-width: 640px) {
	  main {
		max-width: none;
	  }
	}
  </style>



