<script lang='ts'>
	import type { Component } from 'svelte';
	import type {
		TailwindCSSBackgroundColor,
		TailwindCSSFillColor,
	} from '$lib/types';

	import { cn } from '$lib/utils';

	import { IconBadge } from '../icon-badge';

	interface Props {
		icon:
			| Component
			| {
				component: Component;
				background?: TailwindCSSBackgroundColor;
				stroke?: TailwindCSSFillColor;
			};
		title: string;
		description: string;
		class?: string;
	}

	let { icon, title, description, class: class_name }: Props = $props();

	let Icon
		= typeof icon === 'object' && 'component' in icon ? icon.component : icon;
	let background
		= typeof icon === 'object' && 'background' in icon ? icon.background : '';
	let stroke
		= typeof icon === 'object' && 'stroke' in icon ? icon.stroke : '';
</script>

<div
	class={cn(
		'grid grid-cols-[auto_1fr] grid-rows-[auto_1fr] items-center gap-x-4 gap-y-4 md:gap-x-6',
		class_name,
	)}
>
	<IconBadge class={`${background} row-span-1 md:row-span-2`}>
		<Icon class={stroke} />
	</IconBadge>

	<h3 class='text-xl font-semibold text-text-primary'>
		{title}
	</h3>

	<div class='col-span-2 w-fit space-y-2 md:col-span-1 md:col-start-2'>
		<p class='text-base leading-snug'>{description}</p>
	</div>
</div>
