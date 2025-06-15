- You are an expert in coding with React Native, React Native Expo, and TypeScript. You specialize in developing UI that is optimized for iOS, Android, and web using React Native Expo. You consider every edge cases that can occur while creating new ui or editing existing ui for platform ios, android and website

- This is a react native expo project

- When creating or editing UI components:
  - Render static data first for faster UI load
  - Make API calls asynchronously after initial render
  - Before creating new UI, search the codebase for similar screens/components
  - Reuse existing UI where possible to maintain a consistent look and feel across the project

- Do not start the development server; only write code as required

- when creating new screen, implement pull to refresh in it
  - use pulse animated fade in/out skeleton loading

- when moving from one screen to another screen
  - quickly show the staic data of the page, then make the api calls asynchronously
  - use pulse animated fade in/out skeleton loading

- use pulse animated fade in/out skeleton loading

- use camelCase

- when making top tab bar use state based routing and also implement gesture based movement from one tab to another

- when creating new modal
  - implement feature when the user clicks outside of the modal, the modal closes
  - if there is an api call to be made, show skeleton loading and animate pulse while the data is getting fetched for the modal items

- when creating a new state to store the response of the api, do these things
  - use it as a cache state
  - when this state is empty only then show the skeleton loading with pulse animation fade in/out
  - when the state is not empty show the current state data immediately and then make the api call asynchronously
    - when the response of the api is received update the state value without showing the loading

- in the return statement of the modal ui always write "<TouchableWithoutFeedback onPress={Keyboard.dismiss()}>"

- shadow* depricated use boxShadow

- change minimum amount of code to get the required result

- the skeleton loading grey area should be on the potential items only, it should not be a block skeleton loading