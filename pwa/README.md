# PWA

1. What is an app
   * findable in app store
   * icons in their home screen
   * work offline
   * push notifications
   * backgrounds processing
   * access to features of devices they are running on

2. What is the web
   * urls and links
   * markup and styling for humans and machines
   * progressive enhanced features
   * free to implement

3. What makes a pwa
   * responsive
   * work offline
   * app like native
   * fresh
   * safe
   * discoverable
   * re-engageable with push notifications
   * installable
   * linkable

4. pwa capabilities
   * network proxy
   * app packaging
   * push notifications
   * background sync
   * local storage
   * gamepad (joystick or controllers on the device)
   * page visibility
   * media capture
   * media playback
   * device vibration
   * battery status
   * integrated payments
   * credential management
   * network streams
   * peer to peer
   * bluetooth
   * web share

5. development cycle
   * use lighthouse to see how our web page is doing
   * precaching: download files in the cache to use offline (instant loading)
   * Promise: an object that will contain a result (or an error) and implement a .then
   * you use catch to catch an error at the end

6. fetch api

    ```javascript
    fetch('/examples/example.json')
    .then(response => response.json())
    .catch(err => console.log(`Fetch failed: ${err}`));
    ```

    * fetch doesn't throw an error when a file is not found so we need to write extra code to handle that case `response.ok == false` if file not found.

    ```javascript
    fetch('non-existent.json')
    .then(response => {
      if (!response.ok) throw response.statusText;
      return response;
    })
    .then(response => response.json())
    ```

    * use async/await

    ```javascript
    let result = await fetch('non-existent.json');
    if (!response.ok) throw response.statusText;
    let json = await response.json();
    catch(err) {
      json = {error: (err)};
      console.log(`Fetch failed: ${err}`);
    }
    ```

    * get the HEAD

    ```javascript
    let response = await fetch(
      'examples/video.mp4',
      {method: 'HEAD'});
    let length = response.headers.get('content-lenght');
    ```

    * make a post request

    ```javascript
    fetch('sommeur/comment', {
      method: 'POST',
      body: 'title=hello&message=world'
    });
    ```

    * POST with formData

    ```javascript
    let commentForm = document.getElementById('comment-form');
    let form = new FormData(commentForm);

    fetch('sommeur/comment', {
      method: 'POST',
      body: form
    });
    ```

    * setting costum headers

    ```javascript
    let myHeaders = new Headers({
      'Content-type': 'text/plain'
    });

    fetch('sommeur/comment', {
      method: 'POST',
      body: 'title=hello&message=world',
      headers: myHeaders
    });
    ```

    * reading headers

    ```javascript
    fetch(myRequest)
    .then(response => response.headers.get('content-type'))
    .then(type => console.log(type));
    ```

    * running multiple promises at the same time

7. add home screen icon for pwa
   * link web app manifest in the head of our html
   * Manifest properties
       * Identity
           * name
           * short_name
           * for apple: set the metatag `apple-mobile-web-app-title`
       * Presentation
           * start_url
           * theme_color: used in the chrome
           * background_color: used on launch of app
           * in ios you can use a link tag with rel value `apple-touch-startup-image`
           * orientation
           * display: `standalone` makes the app feel native
               * on ios: metatag `apple-mobile-web-app-capable`
       * Icons
           * arrays of icons to use based on the device of the user
           * on ios: `apple-touch-icon` tag
       * dir (direction: ltr (left to right), rtl (right to left))
       * lang (language)
       * description
       * scope: "/" make our app access all the urls, "/foo" make the app access only url starting with /foo and other urls are opened in the browser
       * service worker
