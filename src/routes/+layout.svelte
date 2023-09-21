<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar, LightSwitch, initializeStores, Drawer } from '@skeletonlabs/skeleton';
	import {get} from 'svelte/store';
	import {players} from './store'
	// array mit spielern
	var playerArray: string[] = $players
	// methode zum erstellen löschen
	var name = '';
	function addPlayer(): any {
		if (name != '') {
			playerArray.push(name);
			players.set(playerArray);
			playerArray = playerArray;
			name = '';
		}
	}
	function removeItem(index:number) {
		playerArray.splice(index, 1);
		playerArray = playerArray;
		players.set(playerArray)
	}

	initializeStores();
</script>

<Drawer>
	<div>
		<ul class="list">
			{#each playerArray as player, i}
				<li>
					<span class="flex-auto">{player}</span>
					<button type="button" class="btn btn-s variant-filled" on:click={() => removeItem(i)}>X</button>
				</li>
				<hr />
			{/each}
		</ul>
		<div class="flex flex-col justify-center ">
			<label class="label mt-5 mb-2">
				<input class="input" type="text" placeholder="Input Name" bind:value={name} />
			</label>
			<button type="button" class="btn btn-xl variant-filled" on:click={addPlayer}>+</button>
		</div>
	</div>
</Drawer>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar
			clgridColumns="grid-cols-3"
			slotDefault="place-self-center"
			slotTrail="place-content-end"
		>
			<svelte:fragment slot="lead" />

			<a href="/"><strong class="text-xl uppercase">Partygames</strong></a>

			<svelte:fragment slot="trail">
				<a href="https://www.youtube.com/">Game 1 (Youtube)</a>
				<LightSwitch />
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
