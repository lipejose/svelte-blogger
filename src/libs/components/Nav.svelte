<script lang="ts">
	import Github from '../icons/social/Github.svelte';
	import Linkedin from '../icons/social/Linkedin.svelte';
	import Instagram from '../icons/social/Instagram.svelte';
	import { onMount } from 'svelte';
	import { DARK_THEME, LIGHT_THEME } from '../../config';
	import Links from './Links.svelte';

	type Social = {
		github?: string;
		linkedin?: string;
		instagram?: string;
	};

	export let social: Social;
	export let name: string;

	$: theme = '';

	function handleTheme() {
		theme = localStorage.getItem('theme') === DARK_THEME ? '☀️' : '🌙';
	}

	onMount(() => {
		theme = localStorage.getItem('theme') === LIGHT_THEME ? '☀️' : '🌙';
	});
</script>

<div class="navbar mb-2 shadow-lg bg-neutral text-neutral-content rounded-box mx-8 mt-4">
	<div class="flex-none px-2 mx-2">
		<span class="text-lg font-bold"> {name} </span>
	</div>
	<div class="flex-1 md:px-2 md:mx-2">
		<Links title="Home" to="/" />
		<div class="items-stretch hidden lg:flex">
			<slot />
		</div>
	</div>

	{#if social?.github}
		<div class="flex-none" data-testid="github">
			<a class="btn btn-square btn-ghost" href="https://github.com/{social.github}">
				<Github />
			</a>
		</div>
	{/if}

	{#if social?.linkedin}
		<div class="flex-none" data-testid="linkedin">
			<a class="btn btn-square btn-ghost" href="https://linkedin.com/in/{social.linkedin}">
				<Linkedin />
			</a>
		</div>
	{/if}

	{#if social?.instagram}
		<div class="flex-none" data-testid="instagram">
			<a class="btn btn-square btn-ghost" href="https://instagram.com/{social.instagram}">
				<Instagram />
			</a>
		</div>
	{/if}

	<button
		class="lg:px-8 px-2"
		data-testid="theme"
		data-toggle-theme={`${DARK_THEME},${LIGHT_THEME}`}
		data-act-class="ACTIVECLASS"
		on:click={handleTheme}>{theme}</button
	>
</div>
