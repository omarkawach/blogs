<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="initial-scale=1, maximum-scale=1,user-scalable=no"
    />
    <title>ArcGIS Maps SDK for JavaScript 4.28</title>
    <style>
      html,
      body,
      #viewDiv {
        padding: 0;
        margin: 0;
        height: 100%;
        width: 100%;
        overflow: hidden;
      }
    </style>
    <link
      rel="stylesheet"
      href="https://js.arcgis.com/4.28/esri/themes/light/main.css"
    />
    <script src="https://js.arcgis.com/4.28/"></script>
    <script>
      require([
        "esri/views/MapView",
        "esri/widgets/Legend",
        "esri/widgets/Search",
        "esri/WebMap",
      ], (MapView, Legend, Search, WebMap) => {
        const webmap = new WebMap({
          portalItem: {
            id: "05e015c5f0314db9a487a9b46cb37eca",
          },
        });
        const view = new MapView({
          container: "viewDiv",
          map: webmap,
        });
        const search = new Search({
          view,
        });
        const legend = new Legend({
          view,
        });
        view.ui.add(search, "top-right");
        view.ui.add(legend, "bottom-left");
      });
    </script>
  </head>

  <body>
    <div id="viewDiv"></div>
  </body>
</html>
