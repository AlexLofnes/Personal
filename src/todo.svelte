<script>
	let adding = false;
	let newItem = "";
	let todos = [];
	let notDeltedItems = [];
	const src = "https://findicons.com/files/icons/1681/siena/128/trash.png"

	function addNew () {
		adding = true;
	}

	function handleSubmit () {
		todos.push({name: newItem, completed: false, delted: false});
		notDeltedItems = todos.filter(item => !item.delted);
		newItem = "";
		adding = false;
	}

	function deleteItem (item) {
		todos = todos.filter(i => i !== item);
	}

</script>

{#if adding}
	<form on:submit|preventDefault={handleSubmit}>
		<input placeholder="Add a new task: " bind:value={newItem}>
		<button type="submit">Submit</button>
	</form>

{:else}
<ul>
	{#each todos as item}
		<li class:complete={item.completed} on:click={() => item.completed = !item.completed}>{item.name}</li>
		<img {src} alt="Delte Item" on:click={() => deleteItem(item)}>
	{/each}
</ul>

<button on:click={addNew}>Add New Item</button>
{/if}

<style>
	.complete {
		text-decoration: line-through;
		background: #52D452;
	}

	li {
		background: #ff6961;
        color: whitesmoke;
	}

	li:hover, img:hover {
		cursor: pointer;
	}

	img {
		height: 30px;
		width: 30px;
	}
</style>