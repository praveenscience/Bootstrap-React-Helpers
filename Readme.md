# Bootstrap Helpers

These are my own versions of components that I use for my React Applications, where these snippets might help me by reducing the repetitive stuff that I need to do.

## Card Element

This creates a card element.

```react
import React from "react";

const Card = ({
  Image,
  ImgAlign,
  Header,
  TextHeader,
  Title,
  Text,
  children,
  Footer,
  className
}) => {
  return (
    <div className={"card" + (className ? " " + className : "")}>
      {Image && (
        <img
          className={"card-img-" + ImgAlign}
          src={Image}
          alt={Header && Title}
        />
      )}
      {Header &&
        (TextHeader ? (
          <div className="card-header">{Header}</div>
        ) : (
          <h5 className="card-header">{Header}</h5>
        ))}
      {(Title || Text || children) && (
        <div className="card-body">
          {Title && <h5 className="card-title">{Title}</h5>}
          {Text && <p className="card-text">{Text}</p>}
          {children}
        </div>
      )}
      {Footer && <div className="card-footer text-muted">{Footer}</div>}
    </div>
  );
};

export default Card;
```

## Containers

### Container with a Single Row

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

### Container Element

This creates a generic container element.

```react
import React from "react";

const Container = ({ fluid, className, children }) => {
  return (
    <div
      className={
        "container" +
        (fluid ? "-fluid" : "") +
        (className && className.length > 0 ? " " + className : "")
      }
    >
      {children}
    </div>
  );
};

export default Container;
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

### Headers with Items

Possibly send a button with an `onClick` handler.

```react
import React from "react";

const Header = ({ dark, children, className, items }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `Header navbar navbar-${dark} bg-${dark}` +
        (className ? " " + className : "") +
        (items && items.length ? " navbar-expand-lg" : "")
      }
    >
      <span className="navbar-brand">{children}</span>
      {items && items.length > 0 && (
        <div className="collapse navbar-collapse">
          <ul className="navbar-nav mr-auto">
            {items.map((item, key) => (
              <li className="nav-item" key={key}>
                {item}
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

For a right aligned buttons, use this...

```react
import React from "react";

const Header = ({ dark, children, className, items }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `Header navbar navbar-${dark} bg-${dark}` +
        (className ? " " + className : "") +
        (items && items.length ? " navbar-expand-lg" : "")
      }
    >
      <span className="navbar-brand">{children}</span>
      {items && items.length > 0 && (
        <div className="collapse navbar-collapse">
          <ul className="navbar-nav ml-auto">
            {items.map((item, key) => (
              <li className="nav-item" key={key}>
                {item}
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
