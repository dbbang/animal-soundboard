<script lang="ts">
	export let text: string = '';
	export let color: string = 'bg-orange-50';
	export let disabled: boolean = false;
	export let onClick: (() => void) | undefined = undefined;

	const handleClick = () => {
		onClick?.();
	};
</script>

<button class={`border border-black p-2 text-black ${color}`} {disabled} on:click={handleClick}>
	{text}
</button>





