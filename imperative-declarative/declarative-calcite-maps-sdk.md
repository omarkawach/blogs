<html lang="en" dir="ltr">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no" />
    <title>Calcite and map components (declarative)</title>
    <script src="https://js.arcgis.com/calcite-components/1.9.2/calcite.esm.js" type="module"></script>
    <link rel="stylesheet" href="https://js.arcgis.com/calcite-components/1.9.2/calcite.css" />
    <link rel="stylesheet" href="https://js.arcgis.com/4.28/esri/themes/light/main.css" />
    <script src="https://js.arcgis.com/4.28/"></script>
    <script type="module" src="https://js.arcgis.com/map-components/4.28/arcgis-map-components.esm.js"></script>
</head>

<style>
    html,
    body,
    #viewDiv {
        padding: 0;
        margin: 0;
        height: 100%;
        width: 100%;
    }

    body {
        display: flex;
    }

    calcite-loader {
        align-self: center;
        justify-self: center;
    }

    #header-title {
        margin-left: 1rem;
        margin-right: 1rem;
    }
</style>

<body>
    <calcite-loader></calcite-loader>
    <calcite-shell content-behind>
        <h2 id="header-title" slot="header">
            Predominant Educational Attainment
        </h2>
        <calcite-shell-panel slot="panel-start" display-mode="float">
            <calcite-action-bar slot="action-bar">
                <calcite-action data-action-id="layers" icon="layers" text="Layers"></calcite-action>
                <calcite-action data-action-id="basemaps" icon="basemap" text="Basemaps"></calcite-action>
                <calcite-action data-action-id="legend" icon="legend" text="Legend"></calcite-action>
                <calcite-action data-action-id="bookmarks" icon="bookmark" text="Bookmarks"></calcite-action>
                <calcite-action data-action-id="print" icon="print" text="Print"></calcite-action>
            </calcite-action-bar>
            <calcite-panel heading="Layers" height-scale="l" data-panel-id="layers" hidden>
                <arcgis-layer-list id="layers-container" reference-element="#viewDiv"></arcgis-layer-list>
            </calcite-panel>
            <calcite-panel heading="Basemaps" height-scale="l" data-panel-id="basemaps" hidden>
                <arcgis-basemap-gallery id="basemaps-container" reference-element="#viewDiv"></arcgis-basemap-gallery>
            </calcite-panel>
            <calcite-panel heading="Legend" height-scale="l" data-panel-id="legend" hidden>
                <arcgis-legend id="legend-container" reference-element="#viewDiv"></arcgis-legend>
            </calcite-panel>
            <calcite-panel heading="Bookmarks" height-scale="l" data-panel-id="bookmarks" hidden>
                <arcgis-bookmarks id="bookmarks-container" reference-element="#viewDiv"></arcgis-bookmarks>
            </calcite-panel>
            <calcite-panel heading="Print" height-scale="l" data-panel-id="print" hidden>
                <arcgis-print id="print-container" reference-element="#viewDiv"></arcgis-print>
            </calcite-panel>
        </calcite-shell-panel>
        <arcgis-map item-id="05e015c5f0314db9a487a9b46cb37eca" id="viewDiv" />
    </calcite-shell>
</body>
<script type="module">
    // Reference the map component
    const mapElem = document.querySelector("arcgis-map");
    mapElem.addEventListener("viewReady", ({ detail: { view } }) => {
        view.ui.move("zoom", "top-right");
        view.padding = { left: 49 };
        let activeWidget;
        const handleActionBarClick = ({ target }) => {
            if (target.tagName !== "CALCITE-ACTION") {
                return;
            }
            const nextWidget = target.dataset.actionId;
            if (nextWidget === activeWidget) {
                target.active = false;
                document.querySelector(`[data-panel-id=${nextWidget}]`).hidden = true;
                activeWidget = null;
            } else {
                if (activeWidget) {
                    document.querySelector(`[data-action-id=${activeWidget}]`).active = false;
                    document.querySelector(`[data-panel-id=${activeWidget}]`).hidden = true;
                }
                target.active = true;
                document.querySelector(`[data-panel-id=${nextWidget}]`).hidden = false;
                activeWidget = nextWidget;
            }
        };
        let actionBarExpanded = false;
        document.addEventListener("calciteActionBarToggle", event => {
            actionBarExpanded = !actionBarExpanded;
            view.padding = {
                left: actionBarExpanded ? 150 : 49
            };
        });
        document.querySelector("calcite-action-bar").addEventListener("click", handleActionBarClick);
        document.querySelector("calcite-shell").hidden = false;
        document.querySelector("calcite-loader").hidden = true;
    });
</script>
</html>