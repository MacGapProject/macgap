#MacGap

The MacGap project aims to provide HTML/JS/CSS developers an Xcode project for developing Native OSX Apps that run in OSX's WebView and take advantage of WebKit technologies. The project also exposes a basic JavaScript API for OS integration, such as display Growl notifications. The MacGap project is extremely lightweight and nimble, a blank application is about 0.3mb. 
 
##Pre-requisites

Lion is required to build and run MacGap applications.

To build, make sure you have installed the latest Mac OSX Core Library. Download at [http://developer.apple.com/](http://developer.apple.com/).

Alternatively use the [macgap generator](http://github.com/maccman/macgap-rb).

    gem install macgap    
    macgap --name MyApp --output ./build ./public

##Usage

Just clone the repository and build in Xcode. The file `public/index.html` is loaded on startup.

##API

MacGap exposes an object called `macgap` inside JavaScript. You can use it to alter the Dock icon and display Growl notifications, amongst other things. The API is documented below:

    // Quit application
    macgap.app.terminate();

    // Activate application (bring to front)
    macgap.app.activate();
    
    // Hide application
    macgap.app.hide();
    
    // Un-hide application
    macgap.app.unhide();

    // Change application's window size and location
    macgap.app.setWindowFrame({x:0,y:0,width:100,height:200})
    
    // System bell
    macgap.app.beep();

    // Path to application
    macgap.path.application;
    
    // Path to application's resources
    macgap.path.resource;

    // Set the Dock's badge
    macgap.dock.badge = "10";

    // Play a sound
    macgap.sound.play("./my/sound.mp3")
    
    // Play a system sound
    macgap.sound.playSystem("funk");

    // Send a Growl notification
    macgap.growl.notify({
      title: "Notify",
      content: "New Message!"
    });
    
##Offline Patterns

Desktop apps load immediately and work offline, whilst web apps have the advantage of being easily updated and remotely managed. MacGap gives you the best of both worlds via HTML5's offline APIs. 

First you can define a refresh tag in `index.html`, which will immediately forward your WebView to a given address.

    <meta http-equiv="refresh" content="0;url=http://example.com">

Then use [HTML5 offline APIs](http://www.w3.org/TR/html5/offline.html) to cache your application locally. The first time your application launches, it'll download all the remote resources for use offline. Then during subsequent launches the locally cached resources will be used, and the application will fully function offline. If your remote application changes, then the cache manifest will be updated and application re-cached.

##Attributes

MacGap was forked/ported from Phonegap-mac. It's under the same license (MIT).