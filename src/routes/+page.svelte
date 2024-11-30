<script lang="ts">
	import { preventDefault } from 'svelte/legacy';

	import { goto, preloadData, pushState } from '$app/navigation'
	import { page } from '$app/stores'
	import Modal from './modal.svelte'
	import Image from './photos/[id]/+page.svelte'

	let { data } = $props();

	let modal: HTMLDialogElement = $state()

	async function showModal(e: MouseEvent) {
		// get URL
		const { href } = e.currentTarget as HTMLAnchorElement

		// get result of `load` function
		const result = await preloadData(href)
		console.log(result)

		// create new history entry
		if (result.type === 'loaded' && result.status === 200) {
			pushState(href, { selected: result.data })
			modal.showModal()
		} else {
			goto(href)
		}
	}

	function closeModal() {
		history.back()
	}
</script>

<Modal bind:modal on:close={closeModal}>
	{#if $page.state.selected}
		<Image data={$page.state.selected} />
	{/if}
</Modal>

<div class="feed">
	{#each data.thumbnails as thumbnail}
		<a onclick={preventDefault(showModal)} href="/photos/{thumbnail.id}">
			<img alt={thumbnail.alt} src={thumbnail.src} />
		</a>
	{/each}
</div>

<style>
	.feed {
		max-inline-size: 600px;
		display: grid;
		gap: 2rem;
		margin-inline: auto;
		padding-block: 2rem;
	}
</style>
