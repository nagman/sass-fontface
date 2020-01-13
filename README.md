# SASS @font-face mixin

A simple mixin to load your fonts without the `@font-face` boilerplate.

## Install

1. `yarn add @nagman/sass-fontface`

2. **Rename your fonts** following this format: `name-weight-style.woff`, and put them in a folder in your project:

```
project
└── fonts
  ├── foobar-400-normal.woff
  ├── foobar-400-normal.woff2
  ├── foobar-400-italic.woff
  ├── foobar-400-italic.woff2
  ├── foobar-700-normal.woff
  └── foobar-700-normal.woff2
```

3. Import the mixin into your SCSS code:

```scss
@import "@nagman/sass-fontface/mixin";
```

4. Include fonts by providing every variant of it:

```scss
@include fontFace(
  $name: "foobar",
  $variants: (
    (weight: 400, style: normal),
    (weight: 400, style: italic),
    (weight: 700, style: normal)
  )
);
```

5. Enjoy your webfonts:

```scss
html {
  font-family: "foobar", sans-serif;
}

strong {
  font-weight: 700;
}

em {
  font-style: italic;
}
```

## Output

```css
@font-face {
  font-family: "foobar";
  src: url("/fonts/foobar-400-normal.woff2") format("woff2"), url("/fonts/foobar-400-normal.woff")
      format("woff");
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: "foobar";
  src: url("/fonts/foobar-400-italic.woff2") format("woff2"), url("/fonts/foobar-400-italic.woff")
      format("woff");
  font-weight: 400;
  font-style: italic;
  font-display: swap;
}

@font-face {
  font-family: "foobar";
  src: url("/fonts/foobar-700-normal.woff2") format("woff2"), url("/fonts/foobar-700-normal.woff")
      format("woff");
  font-weight: 700;
  font-style: normal;
  font-display: swap;
}
```

## Options

The mixin takes 4 parameters:

- `$name`: a name for the font. Will be used in your `font-family` properties ;
- `$variants`: a list of variants for this font. Each item is a map with two keys:
  - `weight`: `100`, `200`, `300`, `400`, `500`, `600`, `700`, `800` or `900` ;
  - `style`: `normal`, `italic` or `oblique` ;
- `$dir`: the path to your fonts' files. This is optional and the default value is `/fonts`. You can end it with or without a trailing slash (it will be trimmed) ;
- `$swap`: `true` or `false`. If `true`, it will set the `font-display` property to `true`.

## Weights in numbers

Most of the time, your font file will be named like this: `FooBar Regular.woff`.

You must convert the `Regular` to a number in order for this package to work.

Find out which `font-weight` number corresponds to your font: https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight#Common_weight_name_mapping

## Font optimization

I highly recommend you to **subset** your fonts before serving them. They will load faster because they will only contain the characters you need.

You can do this with [Transfonter](https://transfonter.org/).

Here are my recommended settings for French (remove the accented characters if you only want English):

- Family support: `On`
- Add local() rule: `Off`
- Fix vertical metrics: `Off`
- Autohint font: `Off`
- Base64 encode: `Off`
- Formats: `WOFF` and `WOFF2`
- Subsets: _leave blank_
- Characters: `` !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~¢£¥¨©«®´¸»ÀÂÆÇÈÉÊËÎÏÔÙÛÜàâæçèéêëîïôùûüÿŒœŸˆ˚˜–—‘’‚“”„•…‹›€™ ``
- Unicode ranges: _leave blank_
