---
date: '2023-02-16'
draft: false
title: Custom-Storage-Adapters-for-Ghost
---

# Custom-Storage-Adapters-for-Ghost

# Custom Storage Adapters for Ghost
Created: April 22, 2020 7:06 AM
URL: https://ghost.org/docs/concepts/storage-adapters/
It's possible to send your publication's images to a 3rd party service, CDN or database using a custom storage module.
## Using a custom storage adapter
By default Ghost stores images on your filesystem.
In order to use a custom storage adapter, your custom configuration file needs to be updated to provide config for your new storage module and set it as active:
```
storage: {
active: 'my-module',
'my-module': {
key: 'abcdef'
}
}
```
The storage block should have 2 items:
- An active key, which contains the name* of your module
- A key which reflects the name* of your module, containing any config your module needs
## Available custom storage adapters
- [local-file-store](https://github.com/TryGhost/Ghost/blob/0304816/core/server/storage/local-file-store.js) (default) saves images to the local filesystem
- [http-store passes](https://gist.github.com/ErisDS/559e11bf3e84b89a9594) image requests through to an HTTP endpoint
- [s3-store](https://github.com/spanishdict/ghost-s3-compat) saves to Amazon S3 and proxies requests to S3
- [s3-store](https://github.com/colinmeinke/ghost-storage-adapter-s3) saves to Amazon S3 and works with 0.10+
- [qn-store](https://github.com/Minwe/qn-store) saves to Qiniu
- [ghost-cloudinary-store](https://github.com/mmornati/ghost-cloudinary-store) saves to Cloudinary
- [ghost-storage-cloudinary](https://github.com/eexit/ghost-storage-cloudinary) saves to Cloudinary with RetinaJS support
- [upyun-ghost-store](https://github.com/sanddudu/upyun-ghost-store) saves to Upyun
- [ghost-upyun-store](https://github.com/pupboss/ghost-upyun-store) saves to Upyun
- [ghost-google-drive](https://github.com/robincsamuel/ghost-google-drive) saves to Google Drive
- [ghost-azure-storage](https://github.com/tparnell8/ghost-azurestorage) saves to Azure Storage
- [ghost-imgur](https://github.com/wrenth04/ghost-imgur) saves to Imgur
- [google-cloud-storage](https://github.com/thombuchi/ghost-google-cloud-storage) saves to Google Cloud Storage
- [ghost-oss-store](https://github.com/MT-Libraries/ghost-oss-store) saves to Aliyun OSS
- [ghost-b2](https://github.com/martiendt/ghost-storage-adapter-b2) saves to Backblaze B2
- [ghost-github](https://github.com/ifvictr/ghost-github) saves to GitHub
- [pages-store](https://github.com/zce/pages-store) saves to GitHub Pages or other pages service, e.g. Coding Pages
- [WebDAV Storage](https://github.com/bartt/ghost-webdav-storage-adapter) saves to a WebDAV server.
- [ghost-qcloud-cos](https://github.com/ZhelinCheng/ghost-qcloud-cos) saves to Tencent Cloud COS.
## Creating a custom storage adapter
In order to replace the storage module, use these requirements.
Inside of `content/adapters/storage` create a file or a folder: `content/adapters/storage/my-module.js` or `content/adapters/storage/my-module` - if using a folder, create a file called `index.js` inside it
### Base adapter class inheritance
A custom storage adapter must inherit from your base storage adapter.
```
'use strict';
var BaseAdapter = require('ghost-storage-base');
class MyCustomAdapter extends BaseAdapter{
constructor() {
super();
}
}
module.exports = MyCustomAdapter;
```
### Required methods
Your custom storage adapter must implement five required functions:
- `save` - The `.save()` method stores the image and returns a promise which resolves the path from which the image should be requested in future.
- `exists` - Used by the base storage adapter to check whether a file exists or not
- `serve` - Ghost calls `.serve()` as part of its middleware stack, and mounts the returned function as the middleware for serving images
- `delete`
- `read`
```
'use strict';
var BaseAdapter = require('ghost-storage-base');
class MyCustomAdapter extends BaseAdapter{
constructor() {
super();
}
exists() {
}
save() {
}
serve() {
return function customServe(req, res, next) {
next();
}
}
delete() {
}
read() {
}
}
module.exports = MyCustomAdapter;
```
## Summary
You have discovered how to use a custom storage module to replace the storage layer which handles images with custom code.
