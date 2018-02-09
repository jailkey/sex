# **S**emantical **E**lement e**X**tension
is an easy method to style your markup in a human readable way, by using custom attributes, attribute selectors and custom properties.

## Attributes
The new attributes are:
* **is** - describes a component
  - this attribute can only contain one component name. 
  - To extend an existing component use a hyphen ("component-supercomponent") and make your component extandable.
* **has** - describes special modifiers which overwrites the default style 
  - this attribute can contain a list of properties seperated by spaces.
* **currently** - describes the current state of the module 
  - can contain a list of properties seperated by spaces.
* **on** - describes possible behaviour
   - can contain a list of properties seperated by spaces.
   - if you use 

## Markup
If the attributes are implemented, we can use it in this way:

```html
    <div is="component" has="primary-borders secondary-background" currently="loading" on="touch->grow"></div>
```

## CSS implementation
To implement it in simple, plain CSS we need to use custom properties and we have to define some default names for them:


```css
/*
    set default values
*/
    :root {
        --primary-color: green;
        --secondardy-color: red;
        --default-component-background: #eee;
    }

/*
    define the component
    if you want an extandable component add also the 'extandable' selector ([is*="-component"]):
*/
    [is="component"],
    [is*="-component"] {
        /*set default values for variable properties*/
        --background : var(--default-component-background); 
        --borders : 1px red solid;
        --paddings : 10px 20px;

        background: var(--background);
        border: var(--borders);
        padding: var(--paddings);
        transition: transform .5s;
    }

/*
    define component states
    use the ~= operator to allow a list of states
*/
    [is="component"][currently~="loading"]:before,
    [is*="-component"][currently~="loading"]:before  {
        content: 'loading...';
    }

/*
    define component behaviour
*/
    [is="component"][on~="touch->grow"]:hover,
    [is*="component"][on~="touch->grow"]:hover{
        transform: scale3d(1.2, 1.2, 1.2);
    }

/*
    define modifiers
    use the ~= operator to allow a list of states
    its importend to
*/
    [has~="primary-border"] {
        --borders : 1px var(--primary-color) solid;
    }

    [has~="secondary-background"] {
        --borders : 1px var(--secondary-color) solid;
    }
``` 
## Order
It is import to keep the order of the definitions, otherwise you get into problems with the cascade:
  1. component definitions
  2. component states
  3. component behaviours
  4. modifiers
  5. globale states
  6. global behaviours

## Default custom property names
We need a set of default custom property names to stay compatible.
Here is a list of them:
* --background
* --borders
* --margins
* --paddings
* --font



