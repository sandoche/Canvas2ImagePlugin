Canvas2ImagePlugin
============

This plugin allows you to save images from url to the galery.



Installation
------------

### For Cordova 3.0.x:

1. To add this plugin just type: `cordova plugin add https://github.com/sandoche/Canvas2ImagePlugin` or `phonegap local plugin add https://github.com/sandoche/Canvas2ImagePlugin`
2. To remove this plugin type: `cordova plugin remove org.devgeeks.Canvas2ImagePlugin` or `phonegap local plugin remove org.devgeeks.Canvas2ImagePlugin`


Usage:
------

Call the `window.canvas2ImagePlugin.saveImageDataToLibrary()` method using success and error callbacks and the id attribute or the element object of the canvas to save:

### Example

function saveImageToPhone(url, success, error) {
	var canvas, context, imageDataUrl, imageData;
	var img = new Image();
	img.onload = function() {
		canvas = document.createElement('canvas');
		canvas.width = img.width;
		canvas.height = img.height;
		context = canvas.getContext('2d');
		context.drawImage(img, 0, 0);
		try {
			imageDataUrl = canvas.toDataURL('image/jpeg', 1.0);
			imageData = imageDataUrl.replace(/data:image\/jpeg;base64,/, '');
			cordova.exec(
				success,
				error,
				'Canvas2ImagePlugin',
				'saveImageDataToLibrary',
				[imageData]
				);
			}
			catch(e) {
				error(e.message);
			}
		};
		try {
			img.src = url;
		}
		catch(e) {
			error(e.message);
		}
	}



	var success = function(msg){

	};

	var error = function(err){

	};

	saveImageToPhone(URL, success, error);
