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
      const mapElement = document.querySelector("arcgis-map");
      const layerListElement = document.querySelector("arcgis-layer-list");

      layerListElement.addEventListener("arcgisReady", (event) => {
          const layerList = event.target;
          layerList.listItemCreatedFunction = (event) => {
              const item = event.item;
              if (item.layer.type !== "group") {
                  item.panel = {
                      content: "legend",
                  };
              }
          };
      });

      mapElement.addEventListener("arcgisViewReadyChange", (event) => {
          const { map } = event.target;
          const { portalItem } = map;
          const navigationLogo = document.querySelector("calcite-navigation-logo");
          navigationLogo.heading = portalItem.title;
          navigationLogo.description = portalItem.snippet;
          navigationLogo.thumbnail = portalItem.thumbnailUrl;
          const layer = map.layers.find(
              (layer) => layer.id === "Accidental_Deaths_8938"
          );
          layer.popupTemplate.title = "Accidental Deaths";
      });
  </script>
</body>