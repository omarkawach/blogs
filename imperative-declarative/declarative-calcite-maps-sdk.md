<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="initial-scale=1, maximum-scale=1, user-scalable=no"
    />
    <title>Calcite and map components (declarative)</title>
    <script
      src="https://js.arcgis.com/calcite-components/1.9.2/calcite.esm.js"
      type="module"
    ></script>
    <link
      rel="stylesheet"
      href="https://js.arcgis.com/calcite-components/1.9.2/calcite.css"
    />
    <link
      rel="stylesheet"
      href="https://js.arcgis.com/4.28/esri/themes/light/main.css"
    />
    <script src="https://js.arcgis.com/4.28/"></script>
    <script
      type="module"
      src="https://js.arcgis.com/map-components/4.28/arcgis-map-components.esm.js"
    ></script>
  </head>

  <style>
    html,
    body,
    arcgis-map {
      padding: 0;
      margin: 0;
      height: 100%;
      width: 100%;
    }
  </style>

  <body>
    <calcite-shell>
      <calcite-navigation slot="header">
        <calcite-navigation-logo slot="logo" />
      </calcite-navigation>
      <arcgis-map item-id="e691172598f04ea8881cd2a4adaa45ba" zoom="4">
        <arcgis-layer-list position="top-right" />
      </arcgis-map>
    </calcite-shell>
    <script type="module">
      const mapElm = document.querySelector("arcgis-map");
      const layerListElm = document.querySelector("arcgis-layer-list");
      layerListElm.addEventListener("widgetReady", (event) => {
        const layerList = event.detail.widget;
        layerList.listItemCreatedFunction = (event) => {
          const item = event.item;
          if (item.layer.type !== "group") {
            item.panel = {
              content: "legend",
            };
          }
        };
      });
      mapElm.addEventListener("viewReady", async (event) => {
        const view = event.detail.view;
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
      });
    </script>
  </body>
</html>
