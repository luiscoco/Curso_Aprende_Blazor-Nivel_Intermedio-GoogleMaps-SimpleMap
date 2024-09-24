# How to integrate in your Blazor Web App a Google Simple Map

https://developers.google.com/maps/documentation/javascript/examples/map-simple

## 1. We create a Blazor Web App with Visual Studio 2022 Community Edition.

## 2. We create the JavaScript function for invoking the GoogleMap API

We create a new JavaScript file inside wwwroot folder

![image](https://github.com/user-attachments/assets/6c22be11-30a0-4104-bb9e-84f3cc31302a)

We type the JavaScript code in the ##googlemaps.js## file 

```JavaScript
let map;

async function initMap() {
    const { Map } = await google.maps.importLibrary("maps");

    map = new Map(document.getElementById("map"), {
        center: { lat: -34.397, lng: 150.644 },
        zoom: 8,
    });
}

initMap();
```

We create the 




## 3. 
