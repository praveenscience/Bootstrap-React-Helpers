# Bootstrap Helpers

These are my own versions of components that I use for my React Applications, where these snippets might help me by reducing the repetitive stuff that I need to do.

## Containers & Rows

This creates a container with a row.

```react
import React from "react";

const ContainerRow = ({ fluid, className, children }) => {
  return (
    <div
      className={
        "container" +
        (fluid ? "-fluid" : "") +
        (className && className.length > 0 ? " " + className : "")
      }
    >
      <div className="row">{children}</div>
    </div>
  );
};

export default ContainerRow;
```


