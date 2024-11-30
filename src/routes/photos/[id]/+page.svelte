<script lang="ts">
	let { data } = $props();
</script>

<div class="center">
	<img alt={data.image.alt} src={data.image.src} />
</div>
