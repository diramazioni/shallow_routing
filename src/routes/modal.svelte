<script lang="ts">
	import { createBubbler } from 'svelte/legacy';

	const bubble = createBubbler();
	interface Props {
		modal: HTMLDialogElement;
		children?: import('svelte').Snippet;
	}

	let { modal = $bindable(), children }: Props = $props();
</script>

<dialog bind:this={modal} onclose={bubble('close')}>
	{@render children?.()}
</dialog>

<style>
	dialog {
		border: none;
		border-radius: 8px;
	}

	dialog::backdrop {
		background-color: hsl(0 0% 0% / 40%);
	}
</style>
