## 1. General Requirements
## 2. Non-functional Requirements
## 3. Components Architecture
## 4. Props Design
## 5. Store Design
## 6. Optimization
1. Network
   1.  Minify resources
   2. Debounce
   3. Cache
   4. Loader, Placeholder, Skeleton, Error State
   5 . NPM Registry
2. Render
   1. DOM
      1. Maintain constant number of nodes
         1. Update nodes data instead of deleting and inserting
   2. Avoid reflow
      1. CSS Animation
      2. CSS Naming
   3. skeleton / placeholder / loader
3. JavaScript
   1. Do not block main thread
      1. Do less stuff
      2. Do stuff async
         1. web worker
         2. Cache API, IndexedDB instead of local storage 
## 7. Accessibility
  1. Custom settings
     1. Rem instead of px
  2. Hot keys
     1. Navigation between fields, buttons, pages
     2. submit form, click button, delete message
     3. open help menu
  3. color scheme
     1. color blind
     2. dark mode
  4. Screen reader
     1. aria attributes
        1. aria-live
        2. aria-label
        3. aria-description
     2. alt attributes for images
  5. Localization
  6. A/B test