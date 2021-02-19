<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.1/css/bulma.min.css">
</svelte:head>
<script>
	
	let list = [];
	let listElementPro;

	const createNewListElement = (ownArray, element)=>{
		if(list.length === 0){
			list = [{name: element, id: ownArray.length}];
		}else{
			list = [...ownArray, {name: element, id: ownArray.length}]
		}
	}

	const deleteListElement = (id) =>{
		if(list.length === 1){
			list = []
		}else{
			console.log(list)
			list = [...list.slice(0, id), ...list.slice(id +1)]
			console.log(list)
		}
	}

	const removeElement = (el) => {
		const id = el.path[0].href.split('#')[1];
		parseInt(id)
		deleteListElement(id)
	}

	const addElement = () => {
		createNewListElement(list, listElementPro)
		listElementPro = '';
	}

</script>

<main>
	<div class="columns">
		<div class="column">
			<div class="hero is-link is-medium">
				<div class="hero-body column is-8 is-offset-2">
					<h1 class="title has-text-centered is-size-1">Svelte TodoList</h1>
					<form on:submit|preventDefault={addElement} class="field has-addons">
						<div class="control is-expanded">
							<input class="input is-focused" type="text" placeholder="Do my homework..." bind:value={listElementPro}/>
						</div>
						<div class="control">
							<input class="button is-danger" type="submit" value="Add"  />
						</div>
					</form>
				</div>
			</div>
			<div class="columns">
				<div class="column is-6 is-offset-3 card">
					<ul>
						{#if list.length >= 1}
							{#each list as el, i}
								<li class="level">
									<span class="level-left">{el.name}</span>
									<a href=#{el.id} on:click={removeElement} class="level-right has-text-danger">DELETE</a>
								</li>
							{/each}
						{/if}
					</ul>
				</div>
			</div>
		</div>
	</div>
</main>

<style>

</style>
