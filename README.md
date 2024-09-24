# How to integrate in your Blazor Web App a Google Simple Map

https://developers.google.com/maps/documentation/javascript/examples/map-simple

## 1. We create a Blazor Web App with Visual Studio 2022 Community Edition.

## 2. We create a GoogleMap API Key in the Google Cloud Console

We navigate to the Google Cloud Console and we login

https://cloud.google.com/cloud-console

We press in the Console button to login 

![image](https://github.com/user-attachments/assets/ee22472f-4a50-4f10-af8a-cabc4dbf55e9)

We expand the menu and we select **APIs and Services** menu option

![image](https://github.com/user-attachments/assets/a0c99814-4474-45e3-9893-5209007c63b5)

We create a new API Key

![image](https://github.com/user-attachments/assets/e0b9741a-676b-4b89-acf0-a4797b90b3a3)

We copy the API Key code and paste in the **App.razor** component

![image](https://github.com/user-attachments/assets/ccb46f74-2957-47b6-84bc-6ba495ba8d86)

![image](https://github.com/user-attachments/assets/cc8c5373-b1e2-4123-879f-e108a9f36e21)

## 3. We create the JavaScript function for invoking the GoogleMap API

We create a new JavaScript file inside wwwroot folder

![image](https://github.com/user-attachments/assets/6c22be11-30a0-4104-bb9e-84f3cc31302a)

We type the JavaScript code in the **googlemaps.js** file: 

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

## 4. We include the googlemaps.js file reference in the App.razor component

We include this line in the App.razor code for including the googlemaps.js file inthe Blazor Web Application

```
<script src="googlemaps.js"></script>
```

See the whole App.razor source code:

```razor
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <base href="/" />
    <link rel="stylesheet" href="@Assets["bootstrap/bootstrap.min.css"]" />
    <link rel="stylesheet" href="@Assets["app.css"]" />
    <link rel="stylesheet" href="@Assets["GoogleMapsSample1.styles.css"]" />
    <link rel="icon" type="image/png" href="favicon.png" />
    <HeadOutlet @rendermode="InteractiveServer" />
</head>

<body>
    <Routes @rendermode="InteractiveServer" />
    <script src="_framework/blazor.web.js"></script>
    <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDfD9efMapW2jBBO1Tou4fEBwD7WhaxkZo"
            defer></script>
    <script src="googlemaps.js"></script>

</body>

</html>
```

# 5. 


