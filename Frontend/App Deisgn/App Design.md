## 1. General Requirements
## 2. Non-functional Requirements
## 3. Components Architecture and Design
## 4. Data Entities
## 5. Data API
## 6. Data Store
## 7. Optimization
1. Network
   1. Reduce number of requests
      1. BFF
         1. GraphQL
   2. Compress
      1. GZIP
      2. Brotli
      3. Minify resources
   3. Bundle Splitting
      1. User flow 
      2. Micro Frontend
      3. Utility function
      4. Vendor
   4. Image
      1. webp/png
      2. Image optimizer
   5. Cache 
      1. server cache
      2. client cache
   6. lazy loading non-critical resources
   7. API Monitor
      1. Datadog synthetics test
2. Render
   1. Inline critical resources
   2. Defer non-crit resources
      1. analytic script
   3. Avoid reflow
      1. CSS Animation
      2. CSS Naming
   4. Lazy Loading
      1. skeleton / placeholder / loader
      2. Infinite scroll
      3. Error state
3. JavaScript
   1. Do not block main thread
      1. Do less stuff
      2. Do stuff async
         1. web worker
         2. Cache API, IndexedDB instead of local storage 
## 8. Accessibility
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