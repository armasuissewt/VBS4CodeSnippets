## swisstopo 2D Map

Here is how you can integrate the swisstopo 2D map into VBS4 by using the WMTS service. 

- Install the VBS4 version 24.2.3.24 or newer.
- In the VBS4 editor, go to View -> Map Settings -> Layers
- Press Add Layer button and enter the WMTS service
<p><img alt="smoothing" src="https://github.com/armasuissewt/VBS4CodeSnippets/blob/main/rsc/wmts_settings.png" width="70%"></p>

By modifying the URL, you can alter the actual map. Just adapt the layer names by your need. Some examples

<p>URL: <b>https://wmts.geo.admin.ch/EPSG/4326/1.0.0/WMTSCapabilities.xml?SERVICE=WMTS&REQUEST=GetCapabilities&VERSION=1.0.0&LAYER=ch.swisstopo.pixelkarte-farbe</b><img alt="smoothing" src="https://github.com/armasuissewt/VBS4CodeSnippets/blob/main/rsc/pixelkarte-farbe.png" width="70%"></p>

<p>URL: <b>https://wmts.geo.admin.ch/EPSG/4326/1.0.0/WMTSCapabilities.xml?SERVICE=WMTS&REQUEST=GetCapabilities&VERSION=1.0.0&LAYER=ch.swisstopo.pixelkarte-grau</b><img alt="smoothing" src="https://github.com/armasuissewt/VBS4CodeSnippets/blob/main/rsc/pixelkarte-grau.png" width="70%"></p>

You can find out specific layer names when going to https://map.geo.admin.ch/ and setup the map for your needs. Then you can lookup the layer names in the URL.
