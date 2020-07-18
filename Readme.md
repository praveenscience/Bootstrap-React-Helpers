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

## Headers

```react
import React from "react";

const Header = ({ dark, children, className }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `navbar navbar-${dark} bg-${dark}` + (className ? " " + className : "")
      }
    >
      <span className="navbar-brand">{children}</span>
    </nav>
  );
};

export default Header;
```

### Headers with Links

```react
import React from "react";
import { Link } from "react-router-dom";

const Header = ({ dark, children, className, pages }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `Header navbar navbar-${dark} bg-${dark}` +
        (className ? " " + className : "") +
        (pages && pages.length ? " navbar-expand-lg" : "")
      }
    >
      <span className="navbar-brand">{children}</span>
      {pages && pages.length > 0 && (
        <div className="collapse navbar-collapse">
          <ul className="navbar-nav mr-auto">
            {pages
              .filter(a => !a.DontShow)
              .map((item, key) => (
                <li className="nav-item" key={key}>
                  <Link to={item.Path} className="nav-link">
                    {item.Name}
                  </Link>
                </li>
              ))}
          </ul>
        </div>
      )}
    </nav>
  );
};

export default Header;
```
