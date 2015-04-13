#  [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][daviddm-url]][daviddm-image]

> Help you manage manifest when you are developing Chrome Apps and Extensions


## Install

```sh
$ npm install --save chrome-manifest
```


## Usage

### Manifest

```js
var Manifest = require('chrome-manifest');
var manifest = new Manifest('manifest.json');

// exclude value or key what you want
manifest.exclude([
  {
    'content_scripts.[0].matches': [
      "http://*/*"
    ]
  },
  {
    'background.scripts': [
      'scripts/willbe-remove-only-for-debug.js',
      'scripts/user-script.js'
    ]
  },
  'manifest_version',
  'key'
]);

// get/set
manifest.prop('content_scripts.[0].matches').length;
manifest.prop('background.scripts');
manifest.val('content_scripts.[0].matches.[0]');
var bgscript = manifest.manifest.background.scripts[1];
manifest.prop('manifest_version');
manifest.manifest['key'];

// Save manifest with updated content
manifest.save('manifest.copy.json');

// patch version from 0.0.1 to 0.0.2
manifest.patch();

// Get various types
console.log(manifest.toJSON());
console.log(manifest.toBuffer());
console.log(manifest.toString());

// Get value with dot expression and array expression
console.log(manifest.get('background.scripts.[0]'));
```

```sh
$ npm install --global chrome-manifest
$ chrome-manifest --help
```

### Metadata

Generating manifest.json with basic sample configures

```js
var Manifest = require('chrome-manifest');
var metadata = require('chrome-manifest').Metadata;

// Query permissions by stable and platform_app(Chrome Apps)
var permissions = metadata.queryPermissions({
  channel: 'stable',
  extensionTypes: ['platform_app']
});

// Query manifest fields by stable and extension
var fields = metadata.queryManifest({
  channel: 'stable',
  extensionTypes: ['extension']
});

// Get basic template data
var templateData = metadata.getTemplateData();

templateData.backgroundJS = 'background.js',
templateData.icon16 = 'icon/icon-16.png',
templateData.icon48 = 'icon/icon-48.png',
templateData.icon128 = 'icon/icon-128.png'

var manifest = metadata.getManifest({
  fields: Object.keys(fields),
  permissions: Object.keys(permissions),
  templateData: templateData
});
```

## License

MIT ©[Jommy Moon](http://ragingwind.me)


[npm-url]: https://npmjs.org/package/chrome-manifest
[npm-image]: https://badge.fury.io/js/chrome-manifest.svg
[travis-url]: https://travis-ci.org/ragingwind/chrome-manifest
[travis-image]: https://travis-ci.org/ragingwind/chrome-manifest.svg?branch=master
[daviddm-url]: https://david-dm.org/ragingwind/chrome-manifest.svg?theme=shields.io
[daviddm-image]: https://david-dm.org/ragingwind/chrome-manifest
