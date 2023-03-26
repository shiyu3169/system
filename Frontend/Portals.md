# createPortal
createPortal lets you render some children into a different part of the DOM.

```
<div>
  <SomeComponent />
  {createPortal(children, domNode)}
</div>
```

React portals are used when you want to render a component outside of the parent component's DOM tree. This can be useful in situations where you have a component that should be positioned somewhere else in the document, but still be a part of the React component hierarchy. Here are a few examples of when you might want to use a React portal:

1. Modals: If you have a modal component that should cover the entire screen and be positioned on top of other elements, a portal can be used to render the modal outside of the parent component's tree, allowing it to be positioned in the root of the document and cover all other elements.

2. Tooltips and Popovers: Similarly to modals, tooltips and popovers can be positioned absolutely and relative to the trigger element, which might not be within the parent component's tree. A portal allows these components to be positioned correctly, while still being part of the React component hierarchy.

3. Third-party Library Integrations: If you're using a third-party library that renders its content outside of the parent component's tree, you can use a portal to render the content within the React component hierarchy and manage it within your own React components.

In general, if you have a component that needs to be positioned somewhere else in the document and should be part of the React component hierarchy, a React portal is a good solution.

## react portal vs css position

React portals and CSS positioning are both ways to position elements in a web page, but they have some key differences:

1. React Portals: React portals are part of the React library and provide a way to render a component outside of its parent component's DOM tree. This can be useful in situations where you have a component that needs to be positioned elsewhere in the document, but still be part of the React component hierarchy. React portals allow you to manage and manipulate the positioned elements within your React components, making it easier to integrate with other parts of your React application.

2. CSS Positioning: CSS positioning is a way to position elements using CSS styles. You can use CSS positioning to position elements relative to their parent container, the viewport, or other elements on the page. CSS positioning is more flexible and works for any type of element, not just React components. However, if you are working with React, you will have to manage the positioning of elements outside of the React component hierarchy, making it harder to integrate with other parts of your React application.

In general, you can use either React portals or CSS positioning depending on your needs and the specific requirements of your project. If you want to position elements within your React application and maintain the ability to manage and manipulate them as part of your React components, React portals are a good option. If you need more flexibility in positioning elements and don't mind managing them outside of the React component hierarchy, CSS positioning is a good choice.


ref: https://beta.reactjs.org/reference/react-dom/createPortal