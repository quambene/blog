<!-- markdownlint-disable MD001 -->

# CSS

- [Selectors](#selectors)
- [CSS function](#css-function)
- [SCSS](#scss)
- [Flexbox](#flexbox)
- [Box sizing](#box-sizing)
- [BEM](#bem)

### Selectors

```css
p {}

/* Element selector */
#para1 {}

/* ID selector */
.center {}

/* Class selector */
p.center {}

/* Class selector */
selector:pseudo-class {}

/* Pseudo-class */
selector::pseudo-element {}

/* Pseudo-element */
/* Attribute selector */
a[attribute] {}

a[attribute="value"] {}

a[attribute~="value"] {}

a[attribute|="value"] {}

a[attribute^="value"] {}

a[attribute$="value"] {}
```

### CSS function

```css
/* var() function */
.text {
    color: var(--text-color, black);
}
```

### SCSS

```css
/* SCSS variable in function */
$footer-height: 3.5vh calc(100vh - #{$footer-height})
```

### Flexbox

```css
.flex-column-center {
    display: flex;
    flex-direction: column;
    justify-content: center; /* center items vertically */
    align-items: center; /* center items horizontally */
    height: inherit;
    border: 1px solid blue;
}

.flex-column-space-between {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: inherit;
    border: 1px solid blue;
}

.flex-row-center {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center; /* center items horizontally */
    border: 1px solid blue;
}

.flex-row-baseline {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: baseline; /* align items to baseline */
    border: 1px solid blue;
}
```

### Box sizing

```css
html {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}

*,
*:before,
*:after {
    -webkit-box-sizing: inherit;
    -moz-box-sizing: inherit;
    box-sizing: inherit;
}
```

### BEM (block, element, modifier) methodology

```css
/* Scoping styles in SCSS */
.block {
    @at-root #{&}__element {}

    @at-root #{&}--modifier {}
}

/* in CSS */
.block {
}
.block__element {
}
.block--modifier {
}
```
