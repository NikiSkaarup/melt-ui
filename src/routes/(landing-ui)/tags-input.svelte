<script lang="ts">
	import { cn } from '$docs/utils';
	import { createTagsInput, melt } from '$lib/index.js';
	import { X } from 'lucide-svelte';

	const {
		elements: { root, input, tag, deleteTrigger, edit },
		states: { tags },
	} = createTagsInput({
		defaultTags: ['Svelte', 'Typescript'],
		unique: true,
	});

	let className = '';
	export { className as class };
</script>

<div class={cn('flex flex-col items-start justify-center gap-2', className)}>
	<div
		use:melt={$root}
		class="flex min-w-[240px] flex-row flex-wrap gap-2.5 rounded-xl bg-white px-3 py-2 text-magnum-700
		focus-within:ring focus-within:ring-magnum-400"
	>
		{#each $tags as t}
			<div
				use:melt={$tag(t)}
				class="flex items-center overflow-hidden rounded-lg bg-magnum-200 text-magnum-900 [word-break:break-word]
			data-[disabled]:bg-magnum-300 data-[selected]:bg-magnum-300 data-[disabled]:hover:cursor-default
				data-[disabled]:focus:!outline-none data-[disabled]:focus:!ring-0"
			>
				<span class="flex items-center border-r border-white/10 px-1.5">{t.value}</span>
				<button
					use:melt={$deleteTrigger(t)}
					class="flex h-full items-center px-1 enabled:hover:bg-magnum-300"
				>
					<X class="square-3" />
				</button>
			</div>
			<div
				use:melt={$edit(t)}
				class="flex items-center overflow-hidden rounded-md px-1.5 [word-break:break-word] data-[invalid-edit]:focus:!ring-red-500"
			/>
		{/each}

		<input
			use:melt={$input}
			type="text"
			placeholder="Enter tags..."
			class="min-w-[4rem] shrink grow basis-0 border-0 text-black outline-none focus:!ring-0
      data-[invalid]:text-red-500"
		/>
	</div>
</div>
