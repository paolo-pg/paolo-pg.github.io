## Progressive Web Apps and building your own.
A progressive web app (PWA) is a (mobile) website, acting like a native app. It can be installed on your device and works offline even if you don't have an internet connection. This manual is part of [this](https://github.com/paolo-pg/progressive-web-app-basic) Github project.

#### Pros
- No app store needed, installable by just clicking on add to home screen
- Responsive (desktop, tablet, mobile etc.)
- Feels like an app
- Works offline
- Sharable by just sending the URL
- Fast

#### Cons
- Apple support. PWA don't work as they are intented on iOS (yet)
- Limited to web experience
- Not possible to save data on device

### Requirements
To turn your website into a PWA you need to do the following:
1. Get your work directory ready
2. Add a serviceworker.js
3. Add a web app manifest
4. Force HTTPS
5. Lighthouse

There are several ways to build a working PWA. For example by building a PWA using [React](https://reactjs.org/), [Angular](https://angular.io/) or other framweworks. This manual has been build by using just HTML, CSS and Javascript. This manual will give you a fast start building your own verified PWA.

### Step one: working directory
Get your webpage/working directory ready. I assume you have a simple website ready that works fine on mobile devices. Your workspace should look something like this:
- index.html
- images
- scripts
- styles

### Step two: serviceworker.js
The serviceworker is a JavaScript file that runs separately from the main browser thread, intercepting network requests, caching or retrieving resources from the cache, and delivering push messages. It is possible to build a serviceworker yourself from sratch. I decided to use [Service worker Toolbox](https://github.com/GoogleChromeLabs/sw-toolbox) wich is a collection of service worker tools. Sw-toolbox provides some simple helpers for use in creating your own service workers. It makes building a service worker a lot easier.

Download sw-toolbox and install the sw-toolbox-master map in your root directory of the app.

Follow [this](https://www.youtube.com/watch?v=gfHXekzD7p0&t=424s) tutorial. The tutorial will help you step by step building the service worker using sw-toolbox. The following steps will be executed:
1. Register the service worker
2. Install sw-toolbox
3. Precache
4. Serve from cache

In the end your service worker file looks something like this:

```markdown
importScripts('sw-toolbox-master/sw-toolbox.js'); // Update path to match your own setup

console.log('Hello from service worker');

toolbox.options.debug = true;
// not necessery but shows usefull log extra's in console

toolbox.precache([
    '/', 
    '/service-worker.js', 
    '/index.html', 
    '/styles/style.css', 
    '/styles/lemonade.min.css', 
    '/scripts/script.js', 
    '/scripts/jquery-3.2.1.min.js']);

toolbox.router.get('/', toolbox.fastest);
// checks either cache or network load is faster and uses the fastest, wich is most of the time cache.
```

### Step three: Web app manifest
Another important step to make your website more app-like is adding a manifest. A web app manifest is a json file that provides information about the app. It gives you the ability to control how your web app appears on devices, gives the app a icon, adds a loading icon and it adds default display characterstics to the browser.

Create a file manifest.json and add it to the root of your directory. Add this to manifest.json:
```markdown
{
  "name": "Name of your app",
  "short_name": "Shortname",
  "icons": [
  {
    "src": "images/icons/icon-192x192.png",  
      "sizes": "192x192",  
      "type": "image/png"  
    },  
    {  
      "src": "images/icons/icon-256x256.png",  
      "sizes": "256x256",  
      "type": "image/png"  
    },  
    {  
      "src": "images/icons/icon-384x384.png",  
      "sizes": "384x384",  
      "type": "image/png"  
    },  
    {  
      "src": "images/icons/icon-512x512.png",  
      "sizes": "512x512",  
      "type": "image/png"  
    }
    ],
  "start_url": "/",
  "display": "standalone",
  "background_color": "#FFFFFF",
  "theme_color": "#FFFFFF"
}
```
When a user adds your site to their home screen, you can define a set of icons for the browser to use. You can define them with a type and size. Build your own icons using the default sizes, add them to your directory and edit the manifest.json to match the location of the icons.

```markdown
  "src": "images/icons/icon-512x512.png",  
  "sizes": "512x512",  
  "type": "image/png"  
```
Next tell your browser about the manifest by adding a link tag in the head section of your index file.
```markdown
<link rel="manifest" href="manifest.json">
```
### Step four: HTTPS
Progressive web apps require a secure HTTPS connection instead of the unsecure HTTP. HTTPS helps prevent intruders from tampering with the communications between your websites and your users’ browsers. How you force HTTPS depends on your workflow, webserver and domain. Use [this](https://www.smashingmagazine.com/2017/06/guide-switching-http-https/) guide to use HTTPS.

### Lighthouse
By following all the previous steps your PWA should be about 90% ready. It's not bad if there are several errors or your website is not fully functioning as a web app. Make sure you check your web app for errors using Chrome's Devtools.

The next step is running Google Lighthouse. Lighthouse is an open-source, automated tool for improving the quality of web pages. You can run it against any web page, public or requiring authentication. It has audits for performance, accessibility, progressive web apps, and more. You can run Lighthouse in Chrome DevTools, from the command line, or as a Node module.

![Image](https://i334115.hera.fhict.nl/images/lighthouse2.png)

### Useful links
- [PWA stats](https://www.pwastats.com/?utm_source=syndicate&utm_medium=post&utm_campaign=scotch-jun172510)
- [PWA Gallery](https://outweb.io/)
- [Another PWA Gallery](https://pwa.rocks/?utm_source=syndicate&utm_medium=post&utm_campaign=scotch-jun172510)
- [PWA generator](http://preview.pwabuilder.com/generator)

