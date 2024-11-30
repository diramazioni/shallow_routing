<script lang="ts">
	interface Props {
		modal: HTMLDialogElement;
		children?: import('svelte').Snippet;
		onclose: (e: any) => void;
	}
	
	let { 
		modal = $bindable(), 
		children,
		onclose = () => {},
	}: Props = $props();
</script>

<dialog bind:this={modal} onclose={onclose}>
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
