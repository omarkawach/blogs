<html>
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="initial-scale=1, maximum-scale=1, user-scalable=no"
    />
    <title>Calcite and map components (imperative)</title>
    <script
      src="https://js.arcgis.com/calcite-components/1.9.2/calcite.esm.js"
      type="module"
    ></script>
    <link
      rel="stylesheet"
      href="https://js.arcgis.com/calcite-components/1.9.2/calcite.css"
    />
    <script src="https://js.arcgis.com/4.28/"></script>
    <link
      rel="stylesheet"
      href="https://js.arcgis.com/4.28/esri/themes/light/main.css"
    />
  </head>

  <style>
    html,
    body,
    #viewDiv {
      height: 100%;
      width: 100%;
      padding: 0;
      margin: 0;
    }
  </style>

  <body>
    <calcite-shell>
      <calcite-navigation slot="header">
        <calcite-navigation-logo slot="logo" />
      </calcite-navigation>
      <div id="viewDiv"></div>
    </calcite-shell>
    <script>
      require(["esri/WebMap", "esri/widgets/LayerList", "esri/views/MapView"], (
        WebMap,
        LayerList,
        MapView
      ) => {
        const webMap = new WebMap({
          portalItem: {
            id: "e691172598f04ea8881cd2a4adaa45ba",
          },
        });
        const view = new MapView({
          container: "viewDiv",
          map: webMap,
          zoom: 4,
        });
        view.when(() => {
          const portalItem = view.map.portalItem;
          const navigationLogo = document.querySelector(
            "calcite-navigation-logo"
          );
          navigationLogo.heading = portalItem.title;
          navigationLogo.description = portalItem.snippet;
          navigationLogo.thumbnail = portalItem.thumbnailUrl;
          const layer = view.map.layers.find(
            (layer) => layer.id === "Accidental_Deaths_8938"
          );
          layer.popupTemplate.title = "Accidental Deaths";
          const layerList = new LayerList({
            view,
          });
          view.ui.add(layerList, "top-right");
          layerList.listItemCreatedFunction = (event) => {
            const item = event.item;
            if (item.layer.type !== "group") {
              item.panel = {
                content: "legend",
              };
            }
          };
        });
      });
    </script>
  </body>
</html>
