# 3D Storytelling

[3D Storytelling video](https://storage.googleapis.com/3d-solutions-assets/storytelling-1080p-overview.gif)

![](readme-images/storytelling-4k.gif)
## Overview

Explore the [hosted app](https://js-3d-storytelling-admin-t6a6o7lkja-uc.a.run.app/).

Create a fork and start building your own 3D Storytelling solution.

This repository consists of two parts. The Storytelling app and an Admin app which adds a control panel to create new stories.

You build a story configuration using the Admin UI and then you can download the config.
The demo app uses this config which is loaded from locally to load the story.

## Installation

### Prerequisits

The solution leverages Google maps Platform Photorealistic 3D tiles with Cesium.js as the renderer. Enable all the following APIs:

- [Map Tiles API](https://console.cloud.google.com/marketplace/product/google/tile.googleapis.com?utm_source=3d_solutions_storytelling)
- [Maps JavaScript API](https://console.cloud.google.com/marketplace/product/google/maps-backend.googleapis.com?utm_source=3d_solutions_storytelling)
- [Places API](https://console.cloud.google.com/marketplace/product/google/places-backend.googleapis.com?utm_source=3d_solutions_storytelling)

You need to create a [Google API Key](https://console.cloud.google.com/apis/credentials) and restrict it to at least these APIs.

Also, it is always a good idea to add restrictions for specific websites (i.e. `localhost:5500` for local development).

### Storytelling Solution

There are no external dependencies to view and work with the Storytelling Solution and Demo.

If you want to try with the app without any [local installation](#local-development), try our [hosted demo version](https://goo.gle/3d-storytelling-admin).

### Quickstart - Static webserver

1. [Download](https://github.com/googlemaps-samples/js-3d-area-explorer/archive/refs/heads/main.zip) or `git clone` this repository
2. Extract the contents of the `src` folder
3. Adjust the `config.json` to your needs - see [Configuration](#Configuration)
4. Add your Google Maps Platform API key to [env.exmaple.js](src/env.exmaple.js) and rename the file to `env.js`
5. Serve the files with a static webserver

### Quickstart: Start Admin App using build in bash script

1. Clone this repo to your local machine: `git clone ...`
2. Run the admin setup script: `cd js-3d-area-explorer && chmod +x build_admin.sh`
3. Start the server: `./build_admin.sh <YOUR_GMP_API_KEY>`
    * Note: The script can pick up the API_KEY from envrionment variable `API_KEY` as well.


## Build using Node.js

### Demo app

You can  use your own local webserver to show the 3D Area Explorer app like this:

* From the root directory: `npx http-server -p 5500 ./src`
For the local development you still need the API key for 3D Map Tiles and Google Places/Maps requests.

## Build using Docker

### Build the Demo App with Docker

You need to have docker installed to best work with the **demo-app** locally. 

1. Clone the repository
2. `docker-compose build demo`
3. `docker-compose up demo`

### Build the Admin App with Docker

There is a second docker compose service `docker-compose up app` which only serves the admin app. For this you may need to update the `config.json` file to include you data.

### Manually build the Admin app
Note: You should follow these instructions if you want to create your own admin app in a 
different language other than bash.

To start the local server as **admin app** do the following:

1. Copy the files in demo/src to demo/
     * Bash command from `/demo` directory: `cp -r ../demo/src ./demo`
2. In index.html, at the end of the file, it has reference to main.js. Change it to demo/sidebar.js.
    * Bash command from `/src` directory: `sed -i'.bak' "s/main.js/demo\/sidebar.js/g" index.html`
3. Start the node app by running npx
    * Bash commpand from `src` directory: `http-server -p 5500 ./src`


## Configuration

You can edit the `config.json` file in the `src` directory to change settings. It is also possible to implement your own `loadConfig` function to get configuration from a different file on a different server or to request an API which dynamically returns configuration.


### Story configuration

The `properties` object in the `config.json` is responsible for the overall story settings. Here you can set the hero image, title, date, description and inital camera position of the story as a whole.

### Chapter

The `chapters` property of the config object holds an array of all the story chapters. For each chapter there are different options to set. For example the cahpter title image/video url geo-coordinates and other content. Additionaly you can adjust the camera position and heading (`cameraOptions`), and how to focus the chapter location on the globe (`focusOptions`).

### Camera

The camera object in the story and chapter properties. The location, where the camera is positioned in the 3D space is configured in the `position` object. The orientation, what the camera is looking at, is set via `heading`, `pitch` and `roll`.

### Cesium / Globe

Most of the cesium setting are located and documented in `/src/utils/cesium.js`.

Here are some highlights:

**RADIUS**: The radius from the target point to position the camera.
**BASE_PITCH_RADIANS**: The base pitch of the camera. Defaults to -30 degrees in radians.
**BASE_HEADING_RADIANS**: The base heading of the camera. Defaults to 180 degrees in radians.
**DEFAULT_HIGHLIGHT_RADIUS**: The default radius size of the highlighted area.

## Local Development

For the local development you still need the API key for 3D Map Tiles and Google Places/Maps requests.


## Deployment

To deploy the 3D Story telling app you need to upload everything in the `src` folder to a static web server or some other hosting service. A static web server is enough. You need a domain for you webspace, though. Since the Google Maps API key is only restricted on a domain you would risk misuse of the key.

Included in the repository is a `Dockerfile` which can be used to build a docker image. This can be used to deploy with Google Cloud Run or other container cloud services.

## Repository structure

The repositiory is structured to have separate folder for the actual app (`/src`) and the demo/configuration-ui (`/demo/src`). This is due to fact that we need to deploy different versions.

The app part of the repository is self contained and can be used as is (after updating the configuration). This will show the globe with 3D tiles. Centered on the `location` setting in `config.json`. It will be filled with places from the Google Places API (configured in `config.json`).

The demo folder contains additional code to render a configuration UI to play with the settings in the `config.json`. The code is added to the deployment by running the `/demo/Dockerfile`.


## Terms of Service

This library uses Google Maps Platform services, and any use of Google Maps Platform is subject to the Terms of Service.

For clarity, this library, and each underlying component, is not a Google Maps Platform Core Service.

## Support

This library is offered via an open source license. It is not governed by the Google Maps Platform Support Technical Support Services Guidelines, the SLA, or the Deprecation Policy (however, any Google Maps Platform services used by the library remain subject to the Google Maps Platform Terms of Service).

This library adheres to semantic versioning to indicate when backwards-incompatible changes are introduced. Accordingly, while the library is in version 0.x, backwards-incompatible changes may be introduced at any time.

If you find a bug, or have a feature request, please file an issue on GitHub. If you would like to get answers to technical questions from other Google Maps Platform developers, ask through one of our developer community channels. If you'd like to contribute, please check the Contributing guide.

You can also discuss this library on our Discord server.