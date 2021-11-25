<script>
   import { fade, fly } from 'svelte/transition';
   import { Navbar } from './components';
   import { onMount } from 'svelte';

   let data = [];

   async function fetchData() {
      await fetch(`https://api.github.com/users/sveltejs/repos`)
         .then(async res => {
            data = await res.json();
            console.log('Attempted Data:', data);
         });
   }

   onMount(() => {
      fetchData();
   });
</script>

<Navbar />
<main class='content'>
   <h1 class='data-title'>Svelte JS Github Repos</h1>
   {#await data}
      <p class='data-loading'>loading...</p>
   {:then repos}
      {#if repos.length > -1 }
         <ul class='repos' in:fly='{{ y: 200, duration: 600 }}' out:fade>
            {#each repos as repo}
               <li>
                  <div class='repo__title'>
                     <a href={repo.html_url} target='_blank' rel='noopener noreffer'>
                        {repo.full_name}
                     </a>
                     {#if repo.archived} <span class='repo-archived'>Archived</span> {/if}
                  </div>
                  <p class='repo__description'>
                     {repo.description ?? 'No description provided'}
                  </p>
               </li>
            {/each}
         </ul>
      {:else if repos.message }
         <p class='data-error'>{repos.message}</p>
      {:else}
         <p class='repos-not-found'>No repos found</p>
      {/if}
   {:catch error}
      <p class='data-error'>{error}</p>
   {/await}
</main>

<style>
    .data-loading {
        color: #fff;
        font-weight: bold;
        font-size: 1.1rem;
    }

    .data-title {
        color: #fff;
    }

    .data-error {
        background-color: #ff4c4c;
        color: #fff;
        padding: 10px;
        font-size: 1.05rem;
        border-radius: 5px;
        cursor: default;
    }

    .content {
        margin: 0 20px;
    }

    .repos {
        list-style: none;
        padding: 0;
    }

    .repos-not-found {
        color: #fff;
        font-weight: bold;
        font-size: 1.1rem;
    }

    .repo__title a {
        color: #ddd;
        font-weight: bold;
        font-size: 1.1rem;
    }

    .repo__title a:hover {
        color: #fff;
    }

    .repo__description {
        color: #999999;
        font-size: 0.9rem;
    }

    .repo-archived {
        color: #ff4c4c;
        border-radius: 15px;
        background-color: #666666;
        padding: 2px 7px;
        text-transform: uppercase;
    }
</style>