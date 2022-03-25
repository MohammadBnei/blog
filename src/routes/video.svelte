<script lang="ts">
  import { onMount } from 'svelte'

  let videos = []
  let selected = null

  onMount(async () => {
    const res = await fetch('http://localhost:3001/videos')
    if (res.ok) {
      videos = (await res.json()).videos
      if (videos.length > 0) {
        selected = videos[0]
      }
    }
  })
</script>

{#each videos as v}
  <button
    on:click={() => {
      selected = v
    }}
  >
    {v}
  </button>
{/each}
{#if selected}
  <video src={'http://localhost:3001/stream/' + selected} controls />
{/if}
