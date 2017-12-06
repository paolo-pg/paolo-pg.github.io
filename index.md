## Progressive Web Apps and building your own.

A progressive web app (PWA) is a (mobile) website, acting like a native app. It can be installed on your device and works offline even if you don't have an internet connection. 

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
3. Force HTTPS

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





### Usefull links
[PWA stats](https://www.pwastats.com/?utm_source=syndicate&utm_medium=post&utm_campaign=scotch-jun172510)
[PWA Gallery](https://outweb.io/)
[Another PWA Gallery](https://pwa.rocks/?utm_source=syndicate&utm_medium=post&utm_campaign=scotch-jun172510)
[PWA generator](http://preview.pwabuilder.com/generator)


**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)

