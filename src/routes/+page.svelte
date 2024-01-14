<script>
	import './styles.css';

	import Mode from './Mode.svelte';
  	import Status from './Status.svelte';
  	import Battery from './Battery.svelte';
  	import Map from './Map.svelte';
  	import Nav from './Nav.svelte';
  	import Speed from './Speed.svelte';
	import { fade, slide } from 'svelte/transition';
  	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	export const speed = writable(0);

	let currentSpeed = 2;
  	let mode = 'ECO';
  	let isConnected = false; // Example static value, implement actual Bluetooth logic
  	let batteryLevel = 100; // Example static value, implement actual battery level logic

  // Geolocation options
	const options = {
		enableHighAccuracy: true,
		maximumAge: 0
	};

	// This function will be called whenever the device's position updates
	function handlePosition(position) {
		// Calculate speed, note that speed from geolocation is in meters per second
		//currentSpeed = (position.coords.speed * 3.6).toFixed(2); // Convert m/s to km/h and fix to 2 decimal places
	}

	// Error handling for geolocation
	function handleError(error) {
		console.log('Geolocation error:', error);
	}

	// Watch for position changes
	onMount(() => {
		navigator.geolocation.watchPosition(handlePosition, handleError, options);
	});
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>


	{#if currentSpeed <= 0}
		<div class="stationery-layout h-screen flex flex-col space-y-1 p-1" transition:slide>
			<div class="flex justify-between">
				<Mode extraClass="" {mode} />
				<Status extraClass="" {isConnected} />
			</div>
			<Battery extraClass="" {batteryLevel} />
			<Speed extraClass="" {currentSpeed} />
			<Map extraClass="flex-grow" />
			<Nav  />
		</div>
	{:else if currentSpeed > 0 && currentSpeed < 30}
		<div class="slow-layout h-screen flex flex-col max space-y-1 p-1" transition:fade>

			<Battery extraClass="flex-grow max-h-[15%]" {batteryLevel} />
			<Speed extraClass="flex-grow" {currentSpeed} />
			<Map extraClass="flex-grow" />
		</div>
	{:else}
		<div class="fast-layout h-screen flex flex-col max space-y-1 p-1" transition:fade>
			<Battery extraClass="flex-grow max-h-[15%]" {batteryLevel} />
			<Speed extraClass="flex-grow" {currentSpeed} />
			<Map extraClass="min-h-32" />
	</div>
	{/if}	


<style>
	
</style>
