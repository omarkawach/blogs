<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=5.0"
    />
    <title>Map components</title>
    <style>
      html,
      body {
        padding: 0;
        margin: 0;
        width: 100vw;
        height: 100vh;
      }
    </style>
    <!-- Load the ArcGIS Maps SDK for JavaScript -->
    <link
      rel="stylesheet"
      href="https://js.arcgis.com/4.28/esri/themes/light/main.css"
    />
    <script src="https://js.arcgis.com/4.28/"></script>
    <!-- Load the Map Components -->
    <script
      type="module"
      src="https://js.arcgis.com/map-components/4.28/arcgis-map-components.esm.js"
    ></script>
  </head>

  <body>
    <arcgis-map item-id="05e015c5f0314db9a487a9b46cb37eca">
      <arcgis-search position="top-right" />
      <arcgis-legend position="bottom-left" />
    </arcgis-map>
  </body>
</html>
