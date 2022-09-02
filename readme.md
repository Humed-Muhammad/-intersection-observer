# react-intersections

#### Using npm

```cmd
  npm install react-intersections
```

#### Using yarn

```cmd
  yarn add react-intersections
```

In the past, determining an element's visibility or the relative visibility of two elements in relation to one another has been a challenging problem for which solutions have been unreliable and prone to slowing down the user's browser and the websites they are browsing. The demand for this kind of information has increased as the web has developed. There are several reasons why intersection information is necessary, including:

1. Lazy loading of pictures or other content as you scroll the page.
2. For "infinite scrolling" websites, where content loads and is displayed as you scroll, this eliminates the need for the user to turn pages.
3. Reporting on the presence of ads so that ad revenues can be calculated.
4. Choosing whether or not to perform tasks or animation processes based on whether or not the result will be seen by the user.

======= Support both both esm and cjs modules =======

#### The hook for now returns a targetRef for your target, inView boolean, entry and a visibilityTime for how long the target was visible (best for calcualting ad revenues)

=== More will be added in a future releases ===

```ts
 interface Options {
  root: RefObject<any> | Document;
  callback: (data: InViewDataTypes) => void;
  rootMargin: string;
  threshold: number;
  observeOnce: boolean;
  getLastVisibleData?: boolean;
};

Options used for constrolling the behavoir of the observer;

callback is a function that will be called
when the observer is fired use it for your own logic.

```

# Example

## Hooks

```tsx
import React from "react";
import { useInViewTrigger } from "react-intersections";

export const App = () => {
  const rootRef = React.useRef<HTMLDivElement>(null);
  const { targetRef, inView, visibilityTime, entry } = useInViewTrigger({
    root: rootRef, // optional defualt to document or viewport
    threshold: 1, // optional
  });
  return (
    <div ref={rootRef}>
      <p ref={targetRef}></p>
    </div>
  );
};
```

## API

### Options

Provide these as the options argument in the `useInViewTrigger` hook

| Name               | Type               | Default        | Description                                                                                                                                                     |     |
| ------------------ | ------------------ | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| root               | Element            | document       | The Intersection Observer interface's read-only root property identifies the Element or Document                                                                |     |
| rootMargin         | string             | 0px            | Margin around the root (css margin property )                                                                                                                   |     |
| threshold          | number or number[] | 0.5            | Number between `0` and `1` indicating the percentage that should be visible before triggering. Can also be an array of numbers, to create multiple trigger      |     |
| observeOnce        | boolean            | false          | Only trigger the observer once (i.e. when the target is appear for first time)                                                                                  |     |
| callback           | function           | (data) => void | A function that will be called when the observer is fired, the callback will give you the data as a parameter to use for your logic (use it for your own logic) |     |
| getLastVisibleData | boolean            | false          | Boolean flag for getting the last visible time of the target element when it is no longer in view, (best for when the user is navigate to an other route)       |     |
