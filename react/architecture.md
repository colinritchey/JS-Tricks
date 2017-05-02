source: [How to better build your react applications](https://medium.com/@alexmngn/how-to-better-organize-your-react-applications-2fd3ea1920f1)

Author: Alexis Mangin

"To work properly, they should follow these rules:
 - A component can define nested components or services. It cannot use or define scenes.
 - A scene can define nested components, scenes or services.
 - A service can define nested services. It cannot use or define components or scenes.
 - A data feature is standalone.
 - Nested features can only use from its parent."


Suggested file structure:

```
/src
  /components
    /Button
    /Notifications
      /components
        /ButtonDismiss  
          /images
          /locales
          /specs
          /index.js
          /styles.scss
      /index.js
      /styles.scss

  /data
    /users
      /actions.js
      /api.js
      /reducer.js

  /scenes
    /Home
      /components
        /ButtonLike
      /services
        /processData
      /index.js
      /styles.scss

    /Sign
      /components
        /FormField
      /scenes
        /Login
        /Register
          /locales
          /specs
          /index.js
          /styles.scss

  /services
    /api
    /geolocation
    /session
      /actions.js
      /index.js
      /reducer.js

  index.js
  store.js
```
