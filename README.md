# How to integrate in your Blazor Web App (.NET 9) a Google Simple Map

In this sample we are going to create a Blazor Web Application with Visual Studio 2022 and .NET 9. We will create a Razor component to invoke the GoogleMap API to show a simple map

**Note**: for getting more information about GoogleMaps API in JavaScript visit this example in the URL

https://developers.google.com/maps/documentation/javascript/examples/map-simple

## 1. We create a Blazor Web App with Visual Studio 2022 Community Edition

Install Visual Studio 2022 Versión 17.12.0 Preview 2.0 Community Edition

Run Visual Studio and create a new project:

![image](https://github.com/user-attachments/assets/55158bf9-11cf-4e69-9e12-f6911cbae56b)

We select **Blazor Web App** project template: 

![image](https://github.com/user-attachments/assets/7c69aa07-a889-47a7-b97f-9dbec38e4a0a)

We set the project name and location in the hard disk:

![image](https://github.com/user-attachments/assets/ada3147b-5541-4b8c-9445-76b2654e733c)

We leave all the default values for the following options and press the Create button

![image](https://github.com/user-attachments/assets/84045a59-6a94-4de8-a85b-4da48cc5c4a6)

See the project folders and files structure

![image](https://github.com/user-attachments/assets/b5c3838a-1278-4765-8207-2bb4b9662239)

## 2. We create a GoogleMap API Key in the Google Cloud Console

We navigate to the Google Cloud Console and we login

https://cloud.google.com/cloud-console

We press in the Console button to login 

![image](https://github.com/user-attachments/assets/ee22472f-4a50-4f10-af8a-cabc4dbf55e9)

We expand the menu and we select **APIs and Services** menu option

![image](https://github.com/user-attachments/assets/a0c99814-4474-45e3-9893-5209007c63b5)

We create a new API Key

![image](https://github.com/user-attachments/assets/e0b9741a-676b-4b89-acf0-a4797b90b3a3)

We copy the API Key code from the GoogleCloud console

![image](https://github.com/user-attachments/assets/ccb46f74-2957-47b6-84bc-6ba495ba8d86)

And we paste this code in the **App.razor** component

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

# 5. Create a new Razor Component to show the Google Map

We right click on the Pages folder and create a new component **GoogleMaps.razor**

![image](https://github.com/user-attachments/assets/575edcd7-3aa6-40bf-933f-f7a314577e9d)

This is the new component source code:

**GoogleMaps.razor**

```razor
@page "/googleMaps"

@inject IJSRuntime JSRuntime

<h3>Google Maps with Geolocation</h3>

<!-- Map container -->
<div id="map-container">
    <div id="map" style="height: 400px; width: 100%;"></div>
</div>

<!-- Button to trigger geolocation and center the map -->
<button class="btn btn-primary" @onclick="PanToCurrentLocation">Pan to Current Location</button>

@code {
    private async Task PanToCurrentLocation()
    {
        await JSRuntime.InvokeVoidAsync("initMap");
    }
}
```

## 6. Create a new menu item in the NavMenu.razor component

We open the NavMenu.razor component and we create a new NavLink item for navigating to the new component

```razor
<div class="nav-item px-3">
     <NavLink class="nav-link" href="googleMaps">
          <span class="bi bi-list-nested-nav-menu" aria-hidden="true"></span> GoogleMaps
     </NavLink>
</div>
```

# 7. We run the application a see the result

We select the menu option **GoogleMaps** and then press the **Pan to Current Location** button

![image](https://github.com/user-attachments/assets/f46885ac-ecb2-4a10-af64-67f96084aad6)


