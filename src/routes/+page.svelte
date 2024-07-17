<script>
	import Geohash from 'latlon-geohash'
	import { onMount } from 'svelte'

	const defaultLatitude = 14.56349
	const defaultLongitue = 121.03655
	const defaultGeoHashString = 'wdw4f70n'

	onMount(() => {
    const currentURL = window.location.href
    const currentOrigin = window.location.origin
    const extractedString = currentURL.replace(`${currentOrigin}/?string=`, '')

		if (hasStringParam() && extractedString) {
      const { lat, lon } = Geohash.decode(extractedString)
      initializeMap(extractedString, lat, lon)
		} else {
			initializeMap(defaultGeoHashString, defaultLatitude, defaultLongitue)
		}
	})

	function initializeMap(geohash, latitude, longitude) {
		const L = window.L
		const map = L.map('map').setView([latitude, longitude], 50)
		const marker = L.marker([latitude, longitude]).addTo(map)

		marker
			.bindPopup(
				`<b>GEOHASH:</b> ${geohash} <br>
        <b>LATITUDE:</b> ${latitude} <br>
        <b>LONGITUDE:</b> ${longitude} <br>
        `
			)
			.openPopup()

		L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
			maxZoom: 19,
			attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
		}).addTo(map)
	}

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
