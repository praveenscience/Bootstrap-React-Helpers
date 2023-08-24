# Bootstrap Helpers

These are my own versions of components that I use for my React Applications, where these snippets might help me by reducing the repetitive stuff that I need to do. All these components are based out of **Bootstrap 4 version** and they might need an upgrade.

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

const Header = ({ dark, children, className, to, Link }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `navbar navbar-${dark} bg-${dark}` + (className ? " " + className : "")
      }
    >
      {to ? (
        <Link to={to} className="navbar-brand">
          {children}
        </Link>
      ) : (
        <span className="navbar-brand">{children}</span>
      )}
    </nav>
  );
};

export default Header;
```

### Headers with Links

```react
import React from "react";

const Header = ({ dark, children, className, pages, to, Link }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `Header navbar navbar-${dark} bg-${dark}` +
        (className ? " " + className : "") +
        (pages && pages.length ? " navbar-expand-lg" : "")
      }
    >
      {to ? (
        <Link to={to} className="navbar-brand">
          {children}
        </Link>
      ) : (
        <span className="navbar-brand">{children}</span>
      )}
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

const Header = ({ dark, children, className, items, to, Link }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `Header navbar navbar-${dark} bg-${dark}` +
        (className ? " " + className : "") +
        (items && items.length ? " navbar-expand-lg" : "")
      }
    >
      {to ? (
        <Link to={to} className="navbar-brand">
          {children}
        </Link>
      ) : (
        <span className="navbar-brand">{children}</span>
      )}
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

const Header = ({ dark, children, className, items, to, Link }) => {
  dark = !!dark ? "dark" : "light";
  return (
    <nav
      className={
        `Header navbar navbar-${dark} bg-${dark}` +
        (className ? " " + className : "") +
        (items && items.length ? " navbar-expand-lg" : "")
      }
    >
      {to ? (
        <Link to={to} className="navbar-brand">
          {children}
        </Link>
      ) : (
        <span className="navbar-brand">{children}</span>
      )}
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

## Forms

### Form Group

For all the `<input />` based elements, we have a `FormGroup` component here.

```react
import React from "react";

const FormGroup = ({
  Id,
  Label,
  Type,
  onChange,
  Value,
  defaultValue,
  Checked,
  defaultChecked,
  Placeholder,
  Desc
}) => {
  return (
    <div className="form-group">
      <label htmlFor={Id}>{Label}</label>
      <input
        type={Type}
        className="form-control"
        id={Id}
        name={Id}
        onChange={onChange}
        value={Value}
        placeholder={Placeholder}
        defaultValue={defaultValue}
        checked={Checked}
        defaultChecked={defaultChecked}
        aria-describedby={Id + "Help"}
      />
      {Desc && (
        <small id={Id + "Help"} className="form-text text-muted">
          {Desc}
        </small>
      )}
    </div>
  );
};

export default FormGroup;
```

## Modal Window & Utilities

### Cancelling Propagation

It’s noted that Modal Windows have multiple layers and some of the events need to be cancelled. I created a generic `CancelPropagation` to combat this problem. This can be currently stored inside the `utils` directory as `GenUtils.js` and it has been exposed and exported.

```javascript
export const CancelPropagation = (e, next) => {
  e.stopPropagation();
  if (next && typeof next === "function") next();
};
```

### Modal

```react
import { CancelPropagation } from "../../utils/GenUtils";

const Modal = ({
  children,
  Confirm,
  Cancel,
  Title,
  CancelButton,
  ConfirmButton
}) => {
  return (
    <>
      <div className="Modal modal d-block" role="dialog" onClick={Cancel}>
        <div
          className="modal-dialog"
          role="document"
          onClick={CancelPropagation}
        >
          <div className="modal-content">
            <div className="modal-header">
              <h5 className="modal-title">{Title}</h5>
              <button
                type="button"
                className="close"
                aria-label="Close"
                onClick={Cancel}
              >
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div className="modal-body">{children}</div>
            <div className="modal-footer">
              <button
                type="button"
                className="btn btn-secondary"
                onClick={Cancel}
              >
                {CancelButton}
              </button>
              <button
                type="button"
                className="btn btn-primary"
                onClick={Confirm}
              >
                {ConfirmButton}
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="modal-backdrop fade show"></div>
    </>
  );
};

export default Modal;
```
