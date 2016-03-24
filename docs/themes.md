# Themes for _drop-in.css_

Because developers get tired of looking at the same design project after project, **drop-in.css** now offers themes&mdash;prepared combinations of fonts and colors that change up the look of your app without changing the layout. Essentially, a **drop-in.css** theme simply overrides the font and color choices in the Design Styles section of the **drop-in** stylesheet.

## Installing a _drop-in.css_ theme
It's easy to install a new theme for **drop-in.css** by following these simple steps:


1. Fully install the core **drop-in.css** files:
    * Save copies of **normalize.css** and **drop-in.css** in the appropriate folders in your app.
    * Insert the necessary links to Google Fonts, **normalize.css** and **drop-in.css**.
2. Save the Drop-In theme file in your app's css folder. Theme files are named **drop-in-XX.css**, where "XX" is replaced by initials that identify the particular theme.
3. Replace the default Google Fonts link with the Google Fonts link for the theme you've chosen.
4. Link in the theme stylesheet (**drop-in-XX.css**) _immediately after_ the regular **drop-in.css** stylesheet in the \<head> element of your HTML file, and before your **application.css** file.
5. Open your web page or app, and be sure the new theme is displaying properly.
6. (Optional) Once you are sure the theme is working properly, you _can_ delete the Design Styles section of the basic **drop-in.css** file. You don't _have_ to do this&mdash;**drop-in.css** doesn't care&mdash;but you will slightly reduce the total size of your **.css** files by doing so.

## The themes

### Default, aka "Dracula on Broadway"
Black and white with splashes of red (inspired by Edward Gorey's design for the 1977 Broadway production of _Dracula_). The color scheme is built into the basic **drop-in.css** file, so no **drop-in-XX.css** file is necessary.

```html
<!-- Google Fonts link for default theme -->

<link href='https://fonts.googleapis.com/css?family=Alegreya:700|Open+Sans:400,700,400italic,700italic' rel='stylesheet' type='text/css'>
```

### Great Pumpkin
Orange with green, reminding one of a big, old pumpkin.


Great Pumpkin theme stylesheet: [**drop-in-gp.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/css/drop-in-gp.css)

```html
<!-- Google Fonts link for Great Pumpkin theme -->

<link href='https://fonts.googleapis.com/css?family=Amatic+SC:700|Josefin+Sans:400,400italic,700,700italic' rel='stylesheet' type='text/css'>
```