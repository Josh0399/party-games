<!-- YOU CAN DELETE EVERYTHING IN THIS PAGE -->
<script lang="ts">
  import { getDrawerStore} from '@skeletonlabs/skeleton';
  import type { DrawerSettings, DrawerStore } from '@skeletonlabs/skeleton';

  const drawerSettings: DrawerSettings = {
	id: 'players',
	// Provide your property overrides:
	bgDrawer: 'bg-primary-900 text-white p-5',
	bgBackdrop: 'bg-gradient-to-tr from-primary-500/50 via-secondary-500/50 to-pink-500/50',
	width: 'w-[280px] md:w-[480px]',
	padding: 'p-4',
	rounded: 'rounded-xl',
};
  const drawerStore = getDrawerStore();

	interface Game {
		name: string;
		image?: string;
		url?: string;
		minPlayers: number;
		maxPlayers?: number;
		drinkingGame: boolean;
	}

	const games: Game[] = [
		{
			name: 'RandomGame',
			image: 'src/public/images/games/skat.jpg',
			url: '/suslord',
			minPlayers: 4,
			maxPlayers: 50,
			drinkingGame: true
		},
		
	];

  function openDrawer() {
    drawerStore.open(drawerSettings);
  }
</script>

<body class="flex items-center h-screen flex-col flex-1">
	<h1 class="h1 mb-5">Mainpage</h1>
  
  <button type="button" class="btn btn-xl variant-filled mb-5" on:click={openDrawer}>Show Players</button>
  
	<div class="grid grid-rows-3 grid-flow-col gap-2">
		{#each games as game}
			<a href={game.url}><div class="card card-hover items-center min-h-full min-w-">
					<header class="card-header">{game.name}</header>
					<section class="p-4"><img src={game.image} alt={game.name} /></section>
					<footer class="card-footer">min: {game.minPlayers} max: {game.maxPlayers}</footer>
				</div>
      </a>
		{/each}
	</div>
</body>
