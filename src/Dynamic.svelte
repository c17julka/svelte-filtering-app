<script>
	// Variables
	export let items
	$: searchTerm = ""
	let tag = "all"
	let currentTag = "all"
	let currentRepo = "bulma"
	
	// Filtering items on update
	$: filteredItems = items.filter(item => item.title.includes(searchTerm)).filter(item => tag === "all" ? true : item.tags.includes(tag))
	
	// Remove all currently applied filters
	function removeFilters() {
		searchTerm = ""
		tag = "all"
		currentTag = "all"
		currentRepo = "bulma"
	}
</script>

<nav class="panel">
	
  <p class="panel-heading">
    Repositories
  </p>
	
	<!-- Search function -->
  <div class="panel-block">
    <p class="control has-icons-left">
      <input bind:value={searchTerm} class="input" type="text" placeholder="Search">
			
      <span class="icon is-left">
        <i class="fas fa-search" aria-hidden="true"></i>
      </span>
    </p>
  </div>
	
	<!-- Filter tabs -->
  <p class="panel-tabs">
		<!-- svelte-ignore a11y-missing-attribute -->
    <a on:click="{() => tag = 'all'}" class:is-active="{currentTag === 'all'}" on:click="{() => currentTag = 'all'}">All</a>
		<!-- svelte-ignore a11y-missing-attribute -->
    <a on:click="{() => tag = 'public'}" class:is-active="{currentTag === 'public'}" on:click="{() => currentTag = 'public'}">Public</a>
		<!-- svelte-ignore a11y-missing-attribute -->
    <a on:click="{() => tag = 'private'}" class:is-active="{currentTag === 'private'}" on:click="{() => currentTag = 'private'}">Private</a>
		<!-- svelte-ignore a11y-missing-attribute -->
    <a on:click="{() => tag = 'sources'}" class:is-active="{currentTag === 'sources'}" on:click="{() => currentTag = 'sources'}">Sources</a>
		<!-- svelte-ignore a11y-missing-attribute -->
    <a on:click="{() => tag = 'forks'}" class:is-active="{currentTag === 'forks'}" on:click="{() => currentTag = 'forks'}">Forks</a>
  </p>
	
	<!-- Repositories list -->
	{#each filteredItems as item}
		
		<!-- svelte-ignore a11y-missing-attribute -->
		<a class="panel-block" class:is-active="{currentRepo === item.title}" on:click="{() => currentRepo = item.title}">
			<span class="panel-icon">
				<i class="fas fa-book" aria-hidden="true"></i>
			</span>
			{item.title}
		</a>
			
		
	{/each}
	
	<!-- Reset filters function -->
  <div class="panel-block">
    <button on:click={removeFilters} class="button is-link is-outlined is-fullwidth">
      Reset all filters
    </button>
  </div>
</nav>