### Diseño y Nuevos Medios → Clase 08 → 27/04/2021

# HTML5 + CSS3 + otras bibliotecas de JavaScript

### Teoría

Las [bibliotecas de JavaScript](https://en.wikipedia.org/wiki/List_of_JavaScript_libraries) que hemos explorado, son:

- [p5.js](https://p5js.org/es/) - [p5.js](https://p5js.org/es/) - *Una biblioteca de JavaScript para la programación creativa*.

- [Chart.js](https://www.chartjs.org/) – *Simple, clean and engaging HTML5 based JavaScript charts*.

- [jQuery](https://jquery.com/) - *A fast, small, and feature-rich JavaScript library*.

Nos queda por explorar:

- [Papa Parse](https://www.papaparse.com/) - *The powerful, in-browser CSV parser for big boys and girls*

- [Leaflet.js](https://leafletjs.com/) – *The leading open-source JavaScript library for mobile-friendly interactive maps*.

- - - - - - - - 

En la clase de hoy revisaremos las que quedan pendientes.

**[Papa Parse](https://www.papaparse.com/) nos permite hacer un análisis sintáctico de una estructura de datos contenidos en un archivo [CSV](https://es.wikipedia.org/wiki/Valores_separados_por_comas) para asignarla a una variable en JavaScript. En inglés, y más breve: CSV parsing.**

Con [Papa Parse](https://www.papaparse.com/) podemos simplificar la instrucción para tal análisis con:

```
Papa.parse("https://raw.githubusercontent.com/profesorfaco/dno037-2022/main/clase-05/indice-uso-cobre.csv", {
download: true,
header: true,
dynamicTyping: true,
complete: function (respuesta) {…}
})
```

Paso a paso, la instrucción es:

1. En este script vamos a usar `Papa.parse()`.
2. Esta biblioteca irá por el CSV en tal dirección `Papa.parse("https://…",{})`.
3. La misma biblioteca se encargará de descargarlo `download: true,` 
4. tomando la primera línea de valores separados por coma como encabezado `header: true,`
5. cuidando el tipo de dato de las líneas siguientes `dynamicTyping: true,` y
6. cuando se complete corresponde abrir una función `complete: function (respuesta) {…}`.
7. La variable `respuesta` será reconocida dentro de tal función, conteniendo el resultado del análisis sintáctido de aquél CSV como un objeto:

```
{
data: [ ... ],    // parsed data
errors: [ ... ],  // errors encountered
meta: {	... }     // extra parse info
}
```

Cada línea de valores separado por coma pasa a ser un elemento en un arreglo al que nos podemos referir con un `respuesta.data`

Esto resulta útil cuando no todos los datos serán encontrados en línea en JSON. Algunos podrían estar en CSV, y para ir por ellos, podemos usar PapaParse. Luego, si contamos con datos con información georeferenciada, podríamos ponerlos en un mapa, por ejemplo:

```
region,lat,lon,boric,kast
"Arica y Parinacota",-18.475,-70.314444,50.58,49.42
"Tarapacá",-20.283333,-69.333333,48.68,51.32
"Antofagasta",-23.644167,-70.410833,59.78,40.22
"Atacama",-27.366667,-70.332222,65.43,34.57
"Coquimbo",-29.907778,-71.254167,63.29,36.71
"Valparaíso",-33.063056,-71.639444,59.30,40.70
"Metropolitana",-33.437778,-70.650278,60.33,39.67
"O'Higgins",-34.371944,-71.124528,57.33,42.67
"Maule",-35.426667,-71.671667,48.96,51.04
"Ñuble",-36.616667,-71.95,41.45,58.55
"Biobío",-36.772778,-73.063056,48.17,51.83
"Araucanía",-38.9,-72.666667,39.86,60.14
"Los Ríos",-39.808333,-73.241667,50.47,49.53
"Los Lagos",-41.471667,-72.936667,50.05,49.95
"Aysén",-45.57,-72.066111,56.26,43.74
"Magallanes",-53.1625,-70.9225,61.29,38.71
```

**Con tales, tomados desde un [CSV en línea](https://raw.githubusercontent.com/profesorfaco/dno037-2022/main/clase-08/segunda-vuelta-presidencial.csv) y ya dentro dentro una variable de JavaScript, datos podemos pasar a [Leaflet.js](https://leafletjs.com/): Una biblioteca de JavasScript que ofrece una alternativa ligera para trabajar con mapas interactivos**. Para usarla necesitamos conocer las coordenadas geográficas de lo que se quiera apuntar para, primero, establecer un centro del mapa y luego hacer las marcas correspondientes. También corresponde decidir por un tipo de mapa a usar: 

- [mapbox/light-v10](https://api.mapbox.com/styles/v1/mapbox/light-v10.html?title=true&access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4M29iazA2Z2gycXA4N2pmbDZmangifQ.-g_vE53SD2WrJ6tFX7QHmA#10/-33.47/-70.64); 
- [mapbox/dark-v10](https://api.mapbox.com/styles/v1/mapbox/dark-v10.html?title=true&access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4M29iazA2Z2gycXA4N2pmbDZmangifQ.-g_vE53SD2WrJ6tFX7QHmA#10/-33.47/-70.64); 
- [mapbox/streets-v11](https://api.mapbox.com/styles/v1/mapbox/streets-v11.html?title=true&access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4M29iazA2Z2gycXA4N2pmbDZmangifQ.-g_vE53SD2WrJ6tFX7QHmA#10/-33.47/-70.64); 
- [mapbox/outdoors-v11](https://api.mapbox.com/styles/v1/mapbox/outdoors-v11.html?title=true&access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4M29iazA2Z2gycXA4N2pmbDZmangifQ.-g_vE53SD2WrJ6tFX7QHmA#10/-33.47/-70.64); o 
- [mapbox/satellite-v9](https://api.mapbox.com/styles/v1/mapbox/satellite-v9.html?title=true&access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4M29iazA2Z2gycXA4N2pmbDZmangifQ.-g_vE53SD2WrJ6tFX7QHmA#10/-33.47/-70.64).

La creación de un mapa con [Leaflet.js](https://leafletjs.com/) puede verse así:

```
var miMapa = L.map('aqui').setView([-33.4189754,-70.6181116], 12);

L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', { 
  maxZoom: 17, 
  id: 'mapbox/light-v10', 
  tileSize: 512, 
  zoomOffset: -1 
}).addTo(miMapa);

L.marker([-33.4189754,-70.6181116]).addTo(miMapa).bindPopup("<strong>Escuela de Diseño</strong><br>Campus Lo Contador");
```

En la instrucción hay tres L de [Leaflet.js](https://leafletjs.com/), las que se usan para:

1. Crear un mapa dentro del elemento con la identidad `aqui`. El mapa debe tener en su centro tal coordenada, con un zoom inicial de 12. Y corresponde referir a lo creado como `miMapa`. 
2. Crear una capa aprovechando un mapa de [Mapbox](https://www.mapbox.com/maps/) al que se le podrá hacer un zoom máximo de 17, y agrega esta capa a `miMapa`.
3. Crear un marcador en tal coordenada y agregarlo a `miMapa`. Tal marcador tiene que desplegar un mensaje.

Dos maneras sencillas para encontrar las coordenadas necesarias: 

- En la dirección de Google Maps, son los dos números que siguen después del arroba en `https://www.google.com/maps/@`

- A la derecha del título principal de cada artículo de Wikipedia, en letra azul y pequeña, habitualmente están las coordenadas con vínculo a GeoHack.

- - - - - - - 

### Práctica

El ejercicio se completa cuando cada estudiante publica, [con GitHub Pages](https://docs.github.com/es/free-pro-team@latest/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site), su versión ajustada del sitio web contenido en [esta carpeta de repositorio](https://profesorfaco.github.io/dno037-2022/clase-08/).

El ejercicio completo puede ser evaluado con:

- **0 punto** → no logrado.

- **1 punto** → logrado.

- **2 puntos** → logrado, con aporte descatado.

El ejercicio incompleto es evaluado con 0 punto.

- - - - - - - 

###### [← CLASE ANTERIOR](https://github.com/profesorfaco/dno037-2022/tree/main/clase-07) — [SIGUIENTE CLASE →](https://github.com/profesorfaco/dno037-2022/tree/main/clase-09)
