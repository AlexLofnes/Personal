<script>
    import Todo from './todo.svelte'
    import Sort from './sortchoice.svelte'

    let sort = false;
    let todo = false;
</script>

<div class="container">
	<section>
		<Sort />
	</section>
	<section>
		<Todo />
	</section>
</div>
git 
<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	section {
		height: 100vh;
		scroll-snap-align: start;
	}

	.container {
		scroll-snap-type: y mandatory;
		overflow-y: scroll;
		height: 100vh;
	}
</style>