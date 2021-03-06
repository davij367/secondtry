<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Style circles with a data-driven property</title>
<meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no">
<link href="https://api.mapbox.com/mapbox-gl-js/v2.8.2/mapbox-gl.css" rel="stylesheet">
<script src="https://api.mapbox.com/mapbox-gl-js/v2.8.2/mapbox-gl.js"></script>
<style>
body { margin: 0; padding: 0; }
#map { position: absolute; top: 0; bottom: 0; width: 100%; }
</style>
</head>
<body>
<div id="map"></div>
<script>
	mapboxgl.accessToken = 'pk.eyJ1IjoiZGF2aWozNjciLCJhIjoiY2wyaWF6b3QwMDEwYTNrbnRjYjVoNHc5cCJ9.h81pQSdkmiKjPrPWFTZPYQ';
    const map = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/dark-v10',
        zoom: 12,
        center: [-122.4473, 37.7535]
    });

    map.on('load', () => {
        // Add the vector tileset as a source.
        map.addSource('ethnicity', {
            type: 'vector',
            url: 'mapbox://examples.8fgz4egr'
        });
        map.addLayer({
            'id': 'population',
            'type': 'circle',
            'source': 'ethnicity',
            'source-layer': 'sf2010',
            'paint': {
                // Make circles larger as the user zooms from z12 to z22.
                'circle-radius': {
                    'base': 2.95,
                    'stops': [
                        [12, 2],
                        [22, 180]
                    ]
                },
                // Color circles by ethnicity, using a `match` expression.
                'circle-color': [
                    'match',
                    ['get', 'ethnicity'],
                    'White',
                    '#fbb03b',
                    'Black',
                    '#223b53',
                    'Hispanic',
                    '#e55e5e',
                    'Asian',
                    '#3bb2d0',
                    /* other */ '#ccc'
                ]
            }
        });
    });
</script>


</body>
</html>
