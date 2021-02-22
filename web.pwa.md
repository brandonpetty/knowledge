# Convert Web App Into Installable Progressive Web App (PWA)

[dev.to](https://dev.to/zippytyro/how-to-convert-any-website-webpage-into-an-installable-progressive-web-app-pwa-59ai
)

A progressive web app (PWA) is the set of mobile web application development techniques that entails building apps that feel and look like native ones. Using a web stack (JS, HTML, and CSS), progressive web apps combine rich functionality and a smooth user experience associated with native apps. Simply put, PWA is the web app with the native-app flavor: After the installation, a user clicks on its icon on a device's home screen and gets straight to the website.

## Create A Service Worker File

Create a `service-worker.js` file in the root directory of the project so that static content can be stored in cache storage.

```javascript
// install service worker
const CACHE_NAME  = 'APPLICATION_NAME';

// add relative url to static content for offline cache storage
let resourcesToCache = [
  "./",
  "./img/logo.png",
  "./app.js",
  "./styles.css"
];

self.addEventListener("install", e=>{
  e.waitUntil(
    caches.open(CACHE_NAME).then(cache =>{
      return cache.addAll(resourcesToCache);
    })
  );
});

```

Then add two event listeners:

```javascript
// cache and return requests
self.addEventListener("fetch", e=>{
  e.respondWith(
    caches.match(e.request).then(response=>{
      return response || fetch(e.request);
    })
  );
});

// update the service worker
const cacheWhitelist = ['APPLICATION_NAME'];
self.addEventListener('activate', event => {
  event.waitUntil(
    caches.keys().then(cacheNames => {
      return Promise.all(
        cacheNames.map(cacheName => {
          if (cacheWhitelist.indexOf(cacheName) === -1) {
            return caches.delete(cacheName);
          }
        })
      );
    })
  );
});

```

## Check If Functionality Is Supported

For static websites, update the main HTML document to check for the availability of service workers and then register the application using the `service-worker.js` file from the previous step.

```html
<script>
  if('serviceWorker' in navigator){
    navigator.serviceWorker.register('/service-worker.js');
  } 
  else {
    console.log("service worker not supported");
  }
</script>
```

### Setup Application Metadata

Create a `manifest.json` file that is linked to in the main HTML document.

```html
<link rel="manifest" href="./manifest.json">
```

This file contains important metadata about the applcation such as app name, icons, start url, etc. Here you can specify a single icon OR multiple icons for use with different screen sizes.

```yaml
{
  "name": "APPLICATION NAME",
  "short_name": "SHORT APPLICATION NAME",
  "start_url": "/",
  "background_color": "#ffffff",
  "theme_color": "#000000",
  "icons": [
    {
      "src": "img/192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "maskable any"
    },
    {
      "src": "img/512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "maskable any"
    }
  ],
  "display": "standalone",
  "orientation":"portrait"
}
```

## Dev Tools Debugging

Inside of Chrome Dev Tools click on the application tab and check if the service worker and manifest files are detected by the browser.

You can also verify that your application meets the standard for PWA inside of the lighthouse tab.

Application options should now be visible when visiting the application (based upon the browser or device).
