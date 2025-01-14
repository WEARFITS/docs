*Go back to the [main README](README.md).*

## Footwear and Bags: AR Try-On

The AR Try-On feature allows users to virtually try on shoes, bags, and backpacks in real-time using their mobile device's camera. It can be accessed via a direct link or by scanning a QR code.

<img src="img/wearfits_shoes_ar.webp">

### Demo

Scan the AR code below or click this link on your mobile device: [https://dev.wearfits.com/tryon](https://dev.wearfits.com/tryon)

![WEARFITS](img/wearfits_shoes_ar_qr.png)

### API

#### Implementing our AR shoe & bags try-on is as easy as:
- Drag and drop your 3D shoe model (or use our automatic photo to 3D converter).
- Copy the created link or QR code and share the try-on experience anywhere you like.
- Fully automate the process via API for large volumes.

*💡 The process of model positioning and occluder creation is automated!*

#### Endpoints:

| Endpoint | Description |
|----------|-------------|
| `/tryon` | Provides the footwear AR Try-On experience. May be used as a direct link or via QR code. Currently supports product types such as shoes, bags, and backpacks. Additional parameters are described below. |
| `/tryon/dev` | Currently developed version with new functionalities. Do not use in production environment. |

*💡 Utility tool allowing for changing camera, quality, and mirroring options may be displayed by clicking 4 times in the top right corner of the Try-On Viewer.*

#### Main query string parameters:

| Parameter        | Type     | Description                                                              | Accepted Values| Default Value|
|------------------|----------|---------------------------------------------------------|-------------------------------|------------------------|
| `object` (required) | `string` | Specifies the object ID or URL to the 3D model (`.glb`)                                | Any valid URL or object ID | `null`|
| `color`         | `string` | Colorset ID of the object | Any valid color name | `null` |
| `pose`          | `number` | Required for try-on of bags, backpacks, and garments   | `0` or `1` | `0`|
| `mm`            | `number` | Enables the Mirror Mode with chosen quality  | `1` (lowest), `2` (use pose model), or `3` (use pose and mask) | `0` (not Mirror Mode) |
| `res`           | `string` | Specifies the resolution of the camera input. Can be one of: `vga`, `hd`, `fhd`, `qhd`, `uhd`, `4k`, or a custom resolution like `1920x1200` | Any valid resolution string | `fhd`|
| `camera_id`     | `string` | Specifies the camera device ID | `"string"` | `null`|
| `flip_x`        | `number` | Specifies if the camera input on the `x` axis should be flipped | `0` or `1` | `0`|
| `flip_y`        | `number` | Specifies if the camera input on the `y` axis should be flipped | `0` or `1` | `0`|
| `rotated`       | `number` | Specifies if the camera input should be rotated | `0` or `1` | `0`|

#### Additional query string parameters:

| Parameter        | Type     | Description                                                              | Accepted Values| Default Value|
|------------------|----------|---------------------------------------------------------|-------------------------------|------------------------|
| `quality`        | `string` | Sets the rendering quality                                      | `low`, `medium`, `high`, `auto` | `auto` |
| `ml_model_url`   | `string` | URL to the ML model in JSON format                       | Any valid URL or `small`, `medium`| `null`|
| `tf_backend`     | `string` | Forces the AI backend to use                                     | `webgpu`*, `wasm`, or `webgl`| `null` (auto selected)|
| `nocamera` | `number` | Disables camera and uses video as input | `0` or `1` | `0` |
| `debug_video_clip` | `string` | Debug video clip used with nocamera parameter | Valid URL | `null` |
| `native_ml_version` | `string` | Native ML version to use | Valid version string | `null` |
| `object_scale` | `number` | Object scale | Any positive float | `1.0` |
| `object_collection_id` | `string` | Group ID used in demo. Allows user to change shoes within the group by swiping left or right. Group of models is defined by admin   | `null` |
| `object_carousel_interval` | `number` | Used with object_collection_id, automatic shoe rotation time in seconds | Positive integer | `null` |
| `fps` | `number` | FPS limit | Positive integer | `null` |
| `zoom` | `number` | Camera zoom | Positive integer | `100` |
| `show_snapshot_button` | `number` | Shows snapshot button | `0` or `1` | `0` |
| `show_back_button` | `number` | Shows back button | `0` or `1` | `0` |
| `banner_text` | `string` | Banner text | Any string | `null` |
| `banner_url` | `string` | Banner URL | Valid URL | `null` |
| `banner_icon` | `number` | Banner icon | `0` or `1` | `null` |
| `set_crop_region_from_pose` | `number` | Sets crop region from pose | `0` or `1` | `1` |
| `display_objects_after` | `number` | Delay for displaying objects after foot detection | Non-negative integer | `0` |
| `hide_one` | `number` | Hides shoes if only one foot is detected | `0` or `1` | `0` |
| `loop` | `number` | Loops animation | `0` or `1` | `0` |
| `noloader` | `number` | Hides loader | `0` or `1` | `0` |
| `sound` | `string` | URL of sound to play | Valid URL | `null` |
| `colorlist` | `number` | Shows color list | `0` or `1` | `0` |
| `compose_method` | `string` | Composition method; changing may increase performance | `"canvas"`, `"scene"`, or `"shader"` | `"canvas"` (auto selected) |
| `calibration_data` | `string` | Calibration data (base64 encoded) | Valid base64 string | `null` |

*💡 `webgpu` mode offers the best performance but is not supported on all devices yet (iOS requires enabling WebGPU manually in Safari settings).*



#### Additional query string parameters for bags and backpacks try-on:

| Parameter        | Type     | Description                                                              | Accepted Values| Default Value|
|------------------|----------|---------------------------------------------------------|-------------------------------|------------------------|
| `handbag` | `number` | Enables handbag mode | `0` or `1` | `0` |
| `user_height` | `number` | User height for accurate bag/backpack size calibration | e.g. `165` | `null` |



### Digital Mirror - Communicating with the Viewer via IFRAME

Examples:

- **CodePen:** [https://codepen.io/wearfits/pen/poMjQOz](https://codepen.io/wearfits/pen/poMjQOz)
- **GitHub:** [examples/14-wearfits-digital-mirror-communication.html](examples/14-wearfits-digital-mirror-communication.html)

#### Additional query string parameters:

All parameters from the API section above may be used, but there are also additional parameters available for digital mirror mode:

| Parameter        | Type     | Description                                                              | Accepted Values| Default Value|
|------------------|----------|---------------------------------------------------------|-------------------------------|------------------------|
| `settings`        | `number` | Allows for displaying mirror mode settings by 4-click in top-right corner  | `0` or `1` | `1` |
| `calibration`        | `number` | Displaying simplified settings for mirror calibration only | `0` or `1` | `0` |

Communication between the web app and the digital mirror in an IFRAME is done using the `postMessage` API for sending messages to the IFRAME and receiving events.

**Sending messages to the IFRAME:**

1. Get a reference to the IFRAME's content window:

    ```javascript
    const tryon_iframe_element = document.getElementById('tryon_iframe').contentWindow;
    ```

2. Use `postMessage` to send a message:

   ```javascript
   tryon_iframe_element.postMessage(JSON.stringify(message), "*")
   ```

   where `message` is an object with `name` and `data` properties (examples below).

**Available commands:**

1. Load an object (e.g., a shoe) model: 

    ```json
    { 
        "name": "load_object", 
        "data": "<id>"
    }
    ```

2. Enable/disable camera (can be `0` or `1`):  

    ```json
    {
        "name": "enable_camera",
        "data": 0
    }
    ```

2. Set tryon config:  

    ```json
    {
        "name": "set_option",
        "key": "<config_key>",
        "value": "<config_value>",
    }
    ```

**Receiving messages from the IFRAME:**

1. Add an event listener for the 'message' event on the window object.
2. Check if the message source is the IFRAME.
3. Parse the event data (it's a JSON string).
4. Handle the event based on its name.

**Available events from the IFRAME:**

| Event Name                     | Description                                                                                     | Data Type  |
|--------------------------------|-------------------------------------------------------------------------------------------------|------------------|
| `loadingProgressHandler`          | Triggered during app load                                                                     | Loading progress percentage (`int`)  |
| `loadingFinishedHandler`          | Triggered when the app is loaded                                                                   | null or an error code (`int`)  |
| `objectLoadingProgressHandler`    | Triggered during object loading                                                                | Object loading progress percentage (`int`) |
| `objectLoadingFinishedHandler`    | Triggered when the object finishes loading                                                         | An object; error field is missing if the object is loaded successfully `{ id: string, error: int }` |
| `shoesVisibilityChangedHandler`   | Triggered when feet visibility changes                                                     | A `boolean` indicating visibility   |
| `detectorStateChanged` | Triggered when left or right hand enters or leaves the detection area | `data: { index: <0 - left detector, 1 right detector>, value: <true or false> }` |
| `calibrationParameter` | Triggered when `Save` button, after bag size calibration, is pushed | `{ name: "calibrationParameter", data: "&calibration_data=<...>" }` |

**Hand detection area configuration:**

```javascript
const message = {
    name: "set_option",
    key: "detector_positions",
    value: [
        {
            left: "1vw",
            top: "49vh",
            width: "7vh",
            height: "7vh",
        },
        {
            right: "2.5vw",
            top: "49vh",
            width: "7vh",
            height: "7vh",
        },
    ],
}

tryon_iframe_element.postMessage(JSON.stringify(message), "*")
```

#### Error codes:

| Error Code | Error Message                                              | Error Description |
|------------|---------------------------------------------------------------|-------------|
| `1`          | Unknown error                                             | Any other errors not listed below                          |
| `10`         | Camera error                                       | Camera undefined error                                     |
| `11`         | Camera not found                                   | Camera not found                                          |
| `12`         | Camera disabled in browser                         | navigator.mediaDevices.getUserMedia is undefined         |
| `13`         | Camera permission denied                           | Camera permission denied                                   |
| `14`         | Camera error                                       | Camera device not readable                                 |
| `15`         | Camera disabled in browser                         | WKWebView without allowsInlineMediaPlayback               |
| `20`         | Device not supported                                | Failed to load ML model, unknown error                   |
| `21`         | Device not supported                                | Failed to compile fragment shader                          |
| `30`         | Load error                                         | 3D model load unknown error                               |
| `31`         | Load error                                         | 3D model not found                                        |
| `32`         | Connection error                                   | 3D model download error                                   |
| `33`         | Unauthorized model URL                             | Unauthorized URL origin                                   |
| `34`         | Aborted loading                                   | Connection aborted when trying to load a new object         |

### SDK for iOS and Android

The preferred method is simple and quick browser-based integration, but we may also provide an SDK for native integration of the Footwear AR Try-On into iOS and Android apps. [Ask us](#contact) for more details.




## Footwear: Scan and Fit

Our mobile app for iOS and Android allows users to scan their feet using just a smartphone camera. It provides precise foot measurements and personalized shoe size recommendations.

[Contact us](#contact) for integration details.

## Footwear and Bags: 2D-to-3D Converter

- Our web tool allows for the automatic conversion of 2D images to 3D models.
- The converter is available at: [https://dev.wearfits.com/upload](https://dev.wearfits.com/upload)
- Anonymous service is limited and may be disabled at times. Files are deleted periodically.
- [Contact us](#contact) for more details.




## 3D and AR Viewer

This feature allows users to visualize any 3D objects (including shoes, bags, furniture, etc.) on the website in 3D and in an augmented reality environment. This is achieved by embedding the Viewer via the JavaScript API or by using an `iframe`. The AR visualization is available on mobile devices through a direct URL or by scanning a QR code.

### Demo

A demo is available at: [https://dev.wearfits.com/demo-footwear](https://dev.wearfits.com/demo-footwear)

### Admin Tool

- The web editor allows for uploading and saving objects in multiple 3D formats.
- The editor is available at: [https://dev.wearfits.com/editor](https://dev.wearfits.com/editor)
- After saving the object, you will get the object `id` with corresponding preview links for 3D, AR, and QR code.
- Each object gets a unique URL allowing for editing and sharing: `https://dev.wearfits.com/object/<id>`
- In our web editor, you can change textures, PBR parameters, lighting, scale, position, rotation, etc. One object may have multiple texture/color presets.
- Objects representing **shoes** may be instantly enabled for AR Try-On.
- [Login](https://dev.wearfits.com/account/login) to keep your models private. Anonymous uploads are public and are periodically deleted.
- [Contact us](#contact) for an account and API integration.

#### Endpoints

| Endpoint | Description |
|----------|-------------|
| `/editor` | Allows for uploading new objects and editing (e.g., textures, size, etc.). Login to keep your models private. |
| `/object` | Allows for managing and sharing the file (convert to try-on, edit, export to GLTF, delete), provides preview links (3D, AR, QR code). |
| `/viewer` | 3D viewer which can be embedded into a website or used as a direct link to an object's 3D viewer. Additional parameters are described below. |
| `/viewar` | AR viewer with automatic detection of client device (iOS/Android), utilizes native system AR functionality. |
| `/tryon` | AR Try-On viewer used as a direct link or via QR code - currently supported types: shoes, bags, backpacks. Additional parameters are described below. |

### JavaScript API

1. Import the WEARFITS JavaScript library:

    ```html
    <script type="text/javascript" src="https://dev.wearfits.com/static/js/wearfits.bundle.min.js?"></script>
    ```

2. Create a DIV layer for the 3D visualization:

    ```html
    <div id="wearfits_viewer" style="width:100%; height:100%"></div>
    ```

    You can customize the style but don't change the ID (`wearfits_viewer`).

3. Add JavaScript code:

    ```html
    <script>
        // Required parameters:
        wearfits.showRayTracingButton = false;
        wearfits.showARButton = true;
        
        // Optional parameters:
        wearfits.showMaterialPresets = true;
        wearfits.controlsType = "MOUSE_POSITION";
        
        // Required action:
        wearfits.load("<id>");
    </script>
    ```

    `<id>` is the object name set in the WEARFITS admin.

4. Multiple objects:

    To load and visualize more objects in a 3D viewer, you can use the additional `index` parameter:

    ```html
    wearfits.load("<id>", {index:1});
    ```

    The index number is the number of the object - default (first) is `0`, and `1` is the second one, etc.

### IFRAME

Use the `/viewer` endpoint in the IFRAME source:

```html
<iframe style="width:100%;height:100%" src="https://dev.wearfits.com/viewer?object=<id>&<other_parameters>"></iframe>
```

#### Query String Parameters

| Parameter         | Type     | Description                                                   | Accepted Values                     | Default Value                       |
|-------------------|----------|---------------------------------------------------------------|-------------------------------------|-------------------------------------|
| `object` (required)          | `string` | Specifies the ID of the object to load                       | ID of the object (without `<` `>`)  | `null` |
| `preset`          | `string` | Specifies the object color variant name                            | Any valid color variant name        | `null`                              |
| `nocolorlist`     | `number` | Hides the color list if set to `1`                             | `0` or `1`                          | `0`                                 |
| `norenderbutton`  | `number` | Hides the HQ render button when set to `1`                     | `0` or `1`                          | `0`                                 |
| `noarbutton`      | `number` | Hides the AR button when set to `1`                           | `0` or `1`                          | `0`                                 |
| `nofullscreen`    | `number` | Disables the fullscreen mode when set to `1`                  | `0` or `1`                          | `0`                                 |
| `autorotate`      | `number` | Enables automatic rotation when set to `1`                    | `0` or `1`                          | `0`                                 |
| `hidesettings`    | `number` | Hides the settings panel when set to `1`                      | `0` or `1`                          | `0`                                 |
| `arscale`         | `number` | Sets the initial scale of the object in AR mode               | Any positive number                 | `1`                                 |

Example URL: `https://dev.wearfits.com/viewer?object=backpack&preset=red&nocolorlist=1&autorotate=1`

*Go back to the [main README](README.md).*

## Contact

**For any questions, inquiries, or to request an account, please email us at [contact@wearfits.com](mailto:contact@wearfits.com) or schedule an online meeting via [Calendly](https://calendly.com/lukasz-rzepecki/30min).**

© 2024 [WEARFITS](https://wearfits.com). All rights reserved.
