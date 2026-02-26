<body>
  <div id="viewDiv"></div>
  
  <script type="module">
    const [MapView, Legend, Search, WebMap] = await $arcgis.import([
      "@arcgis/core/views/MapView",
      "@arcgis/core/widgets/Legend",
      "@arcgis/core/widgets/Search",
      "@arcgis/core/WebMap",
    ]);

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
  </script>
</body>