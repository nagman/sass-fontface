# SASS @font-face mixin

A simple mixin to load your fonts without the `@font-face` boilerplate.

## Install
1. `yarn add sass-fontface`
2. Import it into your SCSS code:
```scss
@import "sass-fontface";
```
3. Include required fonts
```scss
@include fontFace('Roboto', 100, normal);
@include fontFace('Roboto Condensed', 300, normal);
```

## Output
```css
@font-face {
  font-family: "Roboto";
  font-weight: 100;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: "Roboto Condensed";
  font-weight: 300;
  font-style: normal;
  font-display: swap;
}
```
