<script>
	import Geohash from 'latlon-geohash'
	import { onMount } from 'svelte'

	onMount(() => {
		const L = window.L
		const map = L.map('map').setView([14.575311217792175, 121.03494345767221], 50)
		const marker = L.marker([14.575311217792175, 121.03494345767221]).addTo(map)
		const geohash = Geohash.encode(14.575311217792175, 121.03494345767221, 6)

		marker.bindPopup('<b>GEOHASH: sdasd</b><br>I am a popup.').openPopup()

		L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
			maxZoom: 19,
			attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
		}).addTo(map)

		console.log(geohash)
	})

	function hasStringParam() {
		var url = new URL(window.location.href)
		return url.searchParams.has('string')
	}
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css"
	/>
	<script
		async
		src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet-src.min.js"
	></script>
</svelte:head>

<div id="map"></div>

<style>
	#map {
		height: 98vh;
	}
</style>
