
<html>

<head>
<script src='https://api.mapbox.com/mapbox-gl-js/v1.12.0/mapbox-gl.js'></script>

<link href='https://api.mapbox.com/mapbox-gl-js/v1.12.0/mapbox-gl.css' rel='stylesheet' />


<style>
body {
  background-color: #fee8c8;
  margin: 0;
  padding: 0;
}
h2,
h3 {
  margin: 10px;
  font-size: 1.2em;
}

h3 {
  font-size: 1em;
}
p {
  font-size: 0.85em;
  margin: 10px;
  text-align: left;
}
.map-overlay {
  position: absolute;
  bottom: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.8);
  font-family: Arial, sans-serif;
  overlay: auto;
  border-radius: 3px;
}
#map {
  position: absolute;
  top: 250px;
  bottom: 0;
  width: 90%;
  margin: 0;
}
#features {
  top: 250px;
  height: 100px;
  margin-top: 0;
  width: 250px;
}
#legend {
  padding: 10px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  line-height: 18px;
  height: 200px;
  margin-bottom: 0;
  margin-right: 0;
  width: 100px;
}
.legend-key {
  display: inline-block;
  border-radius: 20%;
  width: 10px;
  height: 10px;
  margin-right: 5px;
}
ul {
  display: block;
  list-style-type: disc;
  margin-top: 1em;
  margin-bottom: 1 em;
  margin-left: 0;
  margin-right: 0;
  padding-left: 40px;
}
</style>
</head>

<body>
 <h1>Arpan Parashar<br>Studio Lab 3, Interactions with Mapbox GL JS </h1>
  <!-- Add multiple pages to web page-->
  <!-- active class displays the grey box around current page-->
  <ul>
    <a href="index.html" target="_self" style="color: #080200; font-size:20px">&bull; Output 1</a>
    <a class="active" href="mapbox-interaction.html" target="_self" style="color: #080200; font-size:20px">&bull; Output 2</a>
    <a href="mapbox-turfjs.html" target="_self" style="color: #080200; font-size:20px">&bull; Output 3</a>

  </ul>
<div id='map'></div>
<div class='map-overlay' id='features'><h2>US population density</h2><div id='pd'><p>Hover over a state!</p></div></div>
<div class='map-overlay' id='legend'></div>


<script>
mapboxgl.accessToken = 'pk.eyJ1IjoiY2xhcmt1IiwiYSI6ImNrZ2ExNjdjYzAycmwzMW1mMm92Ynl5cDIifQ.0OXA0o-WYeuKNfhhLc45kQ';
var map = new mapboxgl.Map({
  container: 'map', // container id
  style: 'mapbox://styles/clarku/ckgfczge463f01aqg4otowqcw' // replace this with your style URL
});
 map.addControl(new mapboxgl.NavigationControl());

map.on('load', function() {

map.getCanvas().style.cursor = 'default';

map.fitBounds([[-133.2421875, 16.972741], [-47.63671875, 52.696361]]);

var layers = ['0-10', '10-20', '20-50', '50-100', '100-200', '200-500', '500-1000', '1000+'];
var colors = ['#FFEDA0', '#FED976', '#FEB24C', '#FD8D3C', '#FC4E2A', '#E31A1C', '#BD0026', '#800026'];// the rest of the code will go in here


for (i = 0; i < layers.length; i++) {
  var layer = layers[i];
  var color = colors[i];
  var item = document.createElement('div');
  var key = document.createElement('span');
  key.className = 'legend-key';
  key.style.backgroundColor = color;

  var value = document.createElement('span');
  value.innerHTML = layer;
  item.appendChild(key);
  item.appendChild(value);
  legend.appendChild(item);
}

map.on('mousemove', function(e) {
  var states = map.queryRenderedFeatures(e.point, {
    layers: ['statedata']
  });

  if (states.length > 0) {
    document.getElementById('pd').innerHTML = '<h3><strong>' + states[0].properties.name + '</strong></h3><p><strong><em>' + states[0].properties.density + '</strong> people per square mile</em></p>';
  } else {
    document.getElementById('pd').innerHTML = '<p>Hover over a state!</p>';
  }
});
});

</script>
</body>
</html>
