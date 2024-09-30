# WEARFITS API

![WEARFITS](img/wearfits_logo_sq_bl_sm.png)

**[WEARFITS](https://wearfits.com) is a comprehensive web application designed for virtual try-ons and size fitting. Leveraging modern web technologies like 3D, Augmented Reality (AR), Machine Learning, and Generative AI, WEARFITS provides users with an interactive and seamless experience to visualize garments and accessories in both apparel and footwear contexts.**

## Products

| Category                | Solution                | Description                                                                 | Implementation Requirements                                         |
|------------------------|-----------------------|-----------------------------------------------------------------------------|-----------------------------------------------------|
| Footwear & Bags  | **[AR Try-On](#footwear-and-bags-ar-try-on)**             | Virtual try-on in AR and Digital Mirror for footwear, bags, and backpacks | 3D model of a product (`OBJ`, `GLB`, `FBX`, etc.)            |
| Footwear & Bags                   | **[2D-to-3D Converter](#footwear-and-bags-2d-to-3d-converter)**    | Automatic conversion of 2D images into 3D models, useful for shoes and bags digitization | Studio photographs (>30) of a product (`JPG`, `PNG`)       |
| Footwear  | **[Scan and Fit](#footwear-scan-and-fit)**    | Mobile app for precise foot measurements and accurate size recommendations  | Shoe last measurements (e.g. `CSV`, `XLS` or API integration)       |
| Apparel                 | **[3D Virtual Try-On](#apparel-3d-virtual-try-on-and-size-fitting)**             | Visualization and size fitting of apparel in 3D on mannequin-like avatars of your silhouette size     | Parametric 3D model of a garment (`ZPAC`)           |
| Apparel                 | **[Size Fitting](#apparel-3d-virtual-try-on-and-size-fitting)**          | Fit heatmaps and size recommendations                                       | Sizing tables or garment measurements (e.g. `CSV`, `XLS` or API integration)       |
| Apparel                 | **[Gen-AI Try-On](#apparel-generative-ai-try-on)**             | Visualization of garments on yourself with AI-generated images              | 1 photo of a garment (`JPG`, `PNG`)                   |
| Apparel                 | **[AR Try-On](#apparel-ar-try-on)**             | Visualization of garments in AR on yourself                  | 3D model of a garment (`OBJ`, `GLB`, `FBX`, etc.)              |
| Any object                   | **[3D and AR Viewer](#3d-and-ar-viewer)**        | Instant visualization of 3D models of any objects on the web and in AR     | 3D model of an object (`OBJ`, `GLB`, `FBX`, etc.)              |

*Check also our [examples repository](examples/README.md).*

## Footwear and Bags: AR Try-On

The AR Try-On feature allows users to virtually try on shoes, bags, and backpacks in real-time using their mobile device's camera. It can be accessed via a direct link or by scanning a QR code.

### Demo

Scan the AR code below or click this link on your mobile device: [https://dev.wearfits.com/tryon](https://dev.wearfits.com/tryon)

![WEARFITS](img/wearfits_shoes_ar_qr.png)

### API

#### List of endpoints:

| Endpoint | Description |
|----------|-------------|
| `/tryon` | Provides the footwear AR Try-On experience. May be used as a direct link or via QR code. Currently supports product types such as shoes, bags, and backpacks. Additional parameters are described below. |
| `/tryon/dev` | Currently developed version with new functionalities. Do not use in production environment. |

*💡 Utility tool allowing for changing camera, quality, and mirroring options may be displayed by clicking 4 times in the top right corner of the Try-On Viewer.*

#### List of main query string parameters:

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

#### List of additional query string parameters:

| Parameter        | Type     | Description                                                              | Accepted Values| Default Value|
|------------------|----------|---------------------------------------------------------|-------------------------------|------------------------|
| `quality`        | `string` | Sets the rendering quality                                      | `low`, `medium`, `high`, `auto` | `auto` |
| `ml_model_url`   | `string` | URL to the ML model in JSON format                       | Any valid URL or `small`, `medium`| `null`|
| `tf_backend`     | `string` | Forces the AI backend to use                                     | `webgpu`, `wasm`, or `webgl`| `null` (auto selected)|
| `nocamera` | `number` | Disables camera and uses video as input | `0` or `1` | `0` |
| `debug_video_clip` | `string` | Debug video clip used with nocamera parameter | Valid URL | `null` |
| `native_ml_version` | `string` | Native ML version to use | Valid version string | `null` |
| `object_scale` | `number` | Object scale | Any positive float | `1.0` |
| `nologo` | `number` | Hides logo | `0` or `1` | `0` |
| `object_collection_id` | `string` | Group ID used in demo. Allows user to change shoes within the group by swiping left or right. Group of models is defined by admin   | `null` |
| `object_carousel_interval` | `number` | Used with object_collection_id, automatic shoe rotation time in seconds | Positive integer | `null` |
| `fps` | `number` | FPS limit | Positive integer | `null` |
| `zoom` | `number` | Camera zoom | Positive integer | `100` |
| `show_snapshot_button` | `number` | Shows snapshot button | `0` or `1` | `0` |
| `handbag` | `number` | Enables handbag mode | `0` or `1` | `0` |
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

### Digital Mirror - Communicating with the Viewer via IFRAME

Examples:

- **CodePen:** [https://codepen.io/wearfits/pen/poMjQOz](https://codepen.io/wearfits/pen/poMjQOz)
- **GitHub:** [examples/14-wearfits-digital-mirror-communication.html](examples/14-wearfits-digital-mirror-communication.html)

The communication is done using the postMessage API for sending messages to the IFRAME.

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

**Receiving messages from the IFRAME:**

1. Add an event listener for the 'message' event on the window object.
2. Check if the message source is the IFRAME.
3. Parse the event data (it's a JSON string).
4. Handle the event based on its name.

**Available events from the IFRAME:**

| Event Name                     | Description                                                                                     | Data Type                                                                                     |
|--------------------------------|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| `loadingProgressHandler`          | Triggered during app load                                                                     | Loading progress percentage (`int`)                                                             |
| `loadingFinishedHandler`          | Triggered when the app is loaded                                                                   | null or an error code (`int`)                                                                   |
| `objectLoadingProgressHandler`    | Triggered during object loading                                                                | Object loading progress percentage (`int`)                                                      |
| `objectLoadingFinishedHandler`    | Triggered when the object finishes loading                                                         | An object; error field is missing if the object is loaded successfully `{ id: string, error: int }` |
| `shoesVisibilityChangedHandler`   | Triggered when feet visibility changes                                                     | A `boolean` indicating visibility                                                                |

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

## Apparel: 3D Virtual Try-On and Size Fitting

The 3D Try-On Viewer enables users to virtually try on apparel in 3D on avatars of their size. It supports web-based and AR visualizations, providing a versatile platform for different user experiences. The built-in comfort heatmap allows for accurate size fitting.

### Demo

A demo is available at: [https://dev.wearfits.com/demo-apparel](https://dev.wearfits.com/demo-apparel)

### Digitization

Our platform is compatible with 3D models of garments in the `ZPAC` format.

1. Use CLO3D to put the garment on the WEARFITS avatar and export the `ZPAC` file.
2. Upload the `ZPAC` file to the WEARFITS garment admin and process it on the selected avatar.
3. Set the garment ID and wait for the results.
4. Check the results: `https://dev.wearfits.com/render3/<id>`

*💡 The size fitting solution (heatmaps without garment visualizations) doesn't require 3D models of garments - only product measurements or general sizing tables.*

### JavaScript API

Examples:
- GitHub: [examples/1-wearfits-virtualfitting-room.html](examples/1-wearfits-virtual-fitting-room.html)
- CodePen: [https://codepen.io/wearfits/pen/oNKjVeZ](https://codepen.io/wearfits/pen/oNKjVeZ)

1. Import WEARFITS CSS and JavaScript components:

	```html
	<link rel="stylesheet" href="https://dev.wearfits.com/static/css/virtual-advisor.css">

	<script type="text/javascript" src="https://dev.wearfits.com/static/js/wearfits.fr.bundle.min.js"></script>

	<script type="text/javascript" src="https://dev.wearfits.com/static/js/virtual_advisor.js"></script>
	```

2. Prepare a DIV placeholder:

	```html
	<div id="wearfits_viewer"></div>
	```

	You can customize the style, but don't change the ID (`wearfits_viewer`).

3. Add JavaScript code:

	```html
	<script>
		// Required parameter:
		wearfits.current_garment_name = "<id>";
		
		// Optional parameters:
		wearfits.showRayTracingButton = false;
		wearfits.showARButton = true;
		wearfits.showMaterialPresets = true;
		wearfits.showSizeSelectionUI = true;
		wearfits.showAvatarSelectionUI = true;
		wearfits.showComfortMapButton = true;
		wearfits.controlsType = "MOUSE_POSITION";
		
		// Required action:
		wearfits.loadDefaultOrCreateIt();
	</script>
	```

#### List of JavaScript Parameters

| Parameter | Type | Description | Accepted Values | Default Value |
| --- | --- | --- | --- | --- |
| `current_garment_name` (required) | `string` | The ID of the current garment | ID / name of the garment (without `<` `>`) | `null` |
| `showRayTracingButton` | `boolean` | Show or hide the ray tracing button | `true`, `false` | `false` |
| `showARButton` | `boolean` | Show or hide the AR button | `true`, `false` | `true` |
| `showMaterialPresets` | `boolean` | Show or hide material presets | `true`, `false` | `true` |
| `showSizeSelectionUI` | `boolean` | Show or hide size selection UI | `true`, `false` | `true` |
| `showAvatarSelectionUI` | `boolean` | Show or hide avatar selection UI | `true`, `false` | `true` |
| `showComfortMapButton` | `boolean` | Show or hide comfort map button | `true`, `false` | `true` |
| `controlsType` | `string` | Type of controls to use | `MOUSE_POSITION`, `TOUCH_POSITION` | `MOUSE_POSITION` |

#### Multiple Instances of Viewers

To embed multiple viewers on the same website, load the JS file with the `instancesCount` parameter as shown below:

```html
<script type="text/javascript" src="https://dev.wearfits.com/static/js/wearfits.fr.bundle.min.js?instancesCount=2"></script>
```

For additional viewers, use `wearfits_X` object names (e.g., `wearfits`, `wearfits_1`, `wearfits_2`, etc.).

Examples:

- In `<script>` tag:

	```javascript
	wearfits_1.canvas_container_id = "wearfits_viewer2";
	wearfits_1.loadDefaultOrCreateIt();
	// [...]
	```

- In `<body>` tag:

	```html
	<div id="wearfits_viewer2" style="width:100%; height:100%;"></div>
	```

#### Advanced Implementation

An advanced implementation example with external and customized controls can be found [here](examples/13-wearfits-apparel-and-size-fitting-demo.html). Please check the source code to examine it.

To display two garments on the avatar, use the following function instead of `loadDefaultOrCreateIt()`:

```javascript
wearfits.loadByHashAndId("<avatar_id>", ["<id1>_<size>", "<id2>_<size>"]);
```

Example:

```javascript
wearfits.loadByHashAndId("51a2dc298a9ed146e1d6844b6558468e", ["Burda8_38", "Szorty_38"]);
```

To get the preferred size, use this function:

```javascript
wearfits.getPreferredSize();
```

or:

```javascript
wearfits.fetchGarmentMetadata(user_measurements, garment_name, garment_color);
```

It returns:
```json
{
	"name": "fetchGarmentMetadata",
	"data": {
		"garment_name": "<string>",
		"user_measurements": "<object>",
		"preferred_size": "<string>",
		"sizes": ["<string>", "<string>", "..."]
	}
}
```

To change the style of the fit information text, modify the CSS class `wearfits-fit-info-text`:

```css
.wearfits-fit-info-text {
  font-size: 12px;
}
```

To dynamically update the avatar and/or garment, use the following function:

```javascript
wearfits.updateAvatarAndGarment(user_measurements, garment_name, garment_size, garment_color);
```

It returns:
```json
{
	"name": "updateAvatarAndGarment",
	"data": {
		"garment_name": "<string>",
		"garment_size": "<string>",
		"garment_color": "<string>",
		"user_measurements": "<object>",
		"fit_data": {
			"chest": "<string>",
			"waist": "<string>",
			"buttock": "<string>"
		},
		"garment_measurement_3d": {
			"height": "<int>"
		},
		"preferred_size": "<string>"
	}
}
```

### IFRAME

Use one of the following endpoints in the IFRAME source:

- `/render` - The best style for embedding via IFRAME inside a website

	```html
	<iframe src="https://dev.wearfits.com/render/<id>?lang=en&size=M"></iframe>
	```

- `/render3` - The best style for top layer, new tab/window, or mobile standalone view

	```html
	<iframe src="https://dev.wearfits.com/render3/<id>?lang=en&size=M"></iframe>
	```

#### List of Query String Parameters

| Parameter         | Type     | Description                                                   | Accepted Values                     | Default Value                       |
|-------------------|----------|---------------------------------------------------------------|-------------------------------------|-------------------------------------|
| `id` (required)           | `string` | Specifies the ID of the garment                       | ID / name of the garment (without `<` `>`)  | `null` |
| `size` (recommended)            | `string` | Specifies the size of the garment                            | `S`, `M`, `40`, etc.  (same as set in admin)                | `M`                                 |
| `preset`          | `string` | Specifies the garment color                          | Color preset name (e.g., `variant1`) | `null`                              |
| `lang`            | `string` | Specifies the language for the viewer                       | `en`, `fr`, `es`, etc.              | `en`                                |
| `nocolorlist`     | `number`    | Hides the garment color selection list when set to `1`      | `0` or `1`                          | `0`                                 |
| `noavatarselection`| `number`    | Disables the avatar selection when set to `1`               | `0` or `1`                          | `0`                                 |
| `nocomfortbutton` | `number`    | Hides the comfort (heatmap) button when set to `1`                    | `0` or `1`                          | `0`                                 |
| `norenderbutton`  | `number` | Hides the HQ render button when set to `1`                     | `0` or `1`                          | `0`                                 |
| `controlstype`    | `string` | Specifies the type of controls for the viewer               | `mouse`, `touch`					  | `mouse`                             |
| `background`       | `string` | Sets the background color of the viewer                      | Hex color code (e.g., `ffffff` for white) | `ffffff`                            |
| `nopan`            | `number` | Disables panning (two-finger object move) when set to `1`  | `0` or `1`                          | `0`                                 |
| `nofittext`        | `number` | Disables fit info text when set to `1`                           | `0` or `1`                          | `0`                                 |
| `nozoom`           | `number` | Disables zoom when set to `1`                    | `0` or `1`                          | `0`                                 |
| `nosizeselection` | `number` | Disables size selection when set to `1`                           | `0` or `1`                          | `0`                                 |
| `noar`            | `number` | Hides the AR button when set to `1`                               | `0` or `1`                          | `0`                                 |



Example URL: `https://dev.wearfits.com/render3/Burda3?preset=wariant2&nocolorlist=0&lang=en&size=40`








## Apparel: Generative AI Try-On

Generative AI allows for photo-realistic visualization of garments on users with just one photo of a garment. [Ask us](#contact) for a demo.

## Apparel: AR Try-On

Augmented Reality allows users to visualize garments on themselves in real-time. [Ask us](#contact) for a demo.

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

#### List of Endpoints

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

#### List of Query String Parameters

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

## Contact

**For any questions, inquiries, or to request an account, please email us at [contact@wearfits.com](mailto:contact@wearfits.com) or schedule an online meeting via [Calendly](https://calendly.com/lukasz-rzepecki/30min).**

Our website: [https://wearfits.com](https://wearfits.com)