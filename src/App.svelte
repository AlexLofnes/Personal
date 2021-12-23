<script>
    import Todo from './todo.svelte'
    import Sort from './sortchoice.svelte'
	import { fade, slide, scale } from 'svelte/transition'
</script>

<div class="container">
	<section out:fade class="one">
		<Sort />
	</section>
	<section out:fade class="two">
		<Todo />
	</section>
</div>

<style>
	:global(body) {
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