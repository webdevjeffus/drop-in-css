# Themes for _drop-in.css_

Because developers get tired of looking at the same design project after project, **drop-in.css** now offers themes&mdash;prepared combinations of fonts and colors that change up the look of your app without changing the layout. Essentially, a **drop-in.css** theme simply overrides the font and color choices in the Design Styles section of the **drop-in** stylesheet.

## Contents

- [Installing a theme](#installing-a-theme)
- [Default theme](#default)
- [Great Pumpkin](#great-pumpkin)
- [Old Glory](#old-glory)

## Installing a theme
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

### Default

![Default Theme](https://github.com/webdevjeffus/drop-in-css/blob/master/img/default_theme.png "Default theme screenshot")

The color scheme is built into the basic **drop-in.css** file, so no **drop-in-XX.css** file is necessary.

```html
<!-- Google Fonts link for default theme -->

<link href='https://fonts.googleapis.com/css?family=Alegreya:700|Open+Sans:400,700,400italic,700italic' rel='stylesheet' type='text/css'>
```

### Great Pumpkin

![Great Pumpkin Theme](https://github.com/webdevjeffus/drop-in-css/blob/master/img/great_pumpkin_theme.png "Great Pumpkin theme screenshot")

Great Pumpkin theme stylesheet: [**drop-in-gp.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/css/drop-in-gp.css "Great Pumpkin theme screenshot")

```html
<!-- Google Fonts link for Great Pumpkin theme -->

<link href='https://fonts.googleapis.com/css?family=Amatic+SC:700|Josefin+Sans:400,400italic,700,700italic' rel='stylesheet' type='text/css'>
```

### Old Glory

![Old Glory Theme](https://github.com/webdevjeffus/drop-in-css/blob/master/img/old_glory_theme.png "Old Glory theme screenshot")

Old Glory theme stylesheet: [**drop-in-og.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/css/drop-in-og.css "Old Glory theme screenshot")

```html
<!-- Google Fonts link for Old Glory theme -->

<link href='https://fonts.googleapis.com/css?family=Playfair+Display+SC:700|Open+Sans:400,700,400italic,700italic' rel='stylesheet' type='text/css'>
```


#### Licenses

The documentation in this repo is Copyright &copy; 2016 by Jeff George.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Documentation for <b>Drop-In CSS</b></span> by <a xmlns:cc="http://creativecommons.org/ns#" href="webdevjeff.us" property="cc:attributionName" rel="cc:attributionURL">Jeff George</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The code files in this repo, including **drop-in.css**, **demo.html**, and all **drop-in.css** themes, may be used under the terms of the [MIT License](https://opensource.org/licenses/MIT).
