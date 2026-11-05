TWITTER BOOTSTRAP
=================

Bootstrap is Twitter's toolkit for kickstarting CSS for websites, apps, and more. It includes base CSS styles for typography, forms, buttons, tables, grids, navigation, alerts, and more.

To get started -- checkout http://twitter.github.com/bootstrap!


Usage
-----

You can use Twitter Bootstrap in one of two ways: just drop the compiled CSS into any new project and start cranking, or run LESS on your site and compile on the fly like a boss.

Here's what the LESS version looks like:

    <link rel="stylesheet/less" type="text/css" href="lib/bootstrap.less">
    <script src="less.js" type="text/javascript"></script>

Or if you prefer, the standard css way:

    <link rel="stylesheet" type="text/css" href="bootstrap-1.1.1.css">

For more info, refer to the docs!


Retrostrap (modern raw-CSS port)
--------------------------------

`retrostrap.css` is a single-file, preprocessor-free port of Bootstrap 1.1.1 for modern browsers. It uses `--retro-*` custom properties on `:root`, native CSS nesting, `color-mix()` and relative color syntax (`hsl(from ...)`), and CSS flexbox for the unchanged `.row` / `.spanN` / `.offsetN` grid.

    <link rel="stylesheet" href="retrostrap.css">

The source is organized like `lib/` in `css/`, and `css/retrostrap.css` plays the role of `lib/bootstrap.less` by `@import`ing the modules in cascade order (you can link it directly, no build needed):

    css/reset.css        Meyer reset + normalize
    css/preboot.css      --retro-* design tokens (LESS variables)
    css/scaffolding.css  grid, containers, links, focus
    css/type.css         headings, text, lists, code
    css/forms.css        inputs, add-ons, states
    css/tables.css       zebra, bordered, condensed
    css/patterns.css     buttons, topbar, alerts, tabs/pills/pagination, labels/badges, modals, twipsy, popovers
    css/responsive.css   breakpoints (940 / 767 / 480px), reduced motion, forced colors

The root `retrostrap.css` is those files concatenated in the same order. Regenerate it after editing `css/` (PowerShell):

    $h=(gc -raw css/retrostrap.css); $h=$h.Substring(0,$h.IndexOf('*/')+2)
    $h + "`n`n" + ((echo reset preboot scaffolding type forms tables patterns responsive | % { (gc -raw "css/$_.css").TrimEnd() }) -join "`n`n`n") | sc retrostrap.css -Encoding utf8

Re-theme at runtime by changing tokens on `:root`; derived colors (hover, tints, error shades) follow automatically:

    document.documentElement.style.setProperty('--retro-primary', '#ff6600');
    document.documentElement.style.setProperty('--retro-primary-dark', '#aa3300');

Light and dark modes: surfaces, text, lines, bevels and shadows are `light-dark()` tokens, so the whole framework switches with the color scheme. By default it follows the OS (`prefers-color-scheme`); pin a mode with `data-theme` on `<html>` or on any container (a scoped dark panel on a light page works too):

    <html data-theme="dark">     <!-- "light" | "dark"; omit to follow the system -->

Brand color: to drive the whole blue family from one value, opt in to derived mode and set only `--retro-primary`. The dark gradient stop, focus glow, link color and pagination tint are then derived from it (and adapt to light/dark):

    <html data-retro-brand="derived">
    document.documentElement.style.setProperty('--retro-primary', '#2e8b57');

Without `data-retro-brand="derived"` the original Bootstrap 1.1.1 hex values are used exactly.

Responsive: include `<meta name="viewport" content="width=device-width, initial-scale=1">` in your `<head>`. At ≤940px the container becomes fluid, at ≤767px the grid stacks to one column, the topbar stops being fixed and wraps, and tables scroll horizontally; at ≤480px spacing and headings tighten further.

Open `retrostrap-demo.html` for every component plus a live theme editor.


Bug Tracker
-----------

Have a bug? Please create an issue here on GitHub!

https://github.com/twitter/bootstrap/issues


Mailing List
------------

Have a question? Ask on our mailing list!

twitter-bootstrap@googlegroups.com

http://groups.google.com/group/twitter-bootstrap


Developers
----------

We have included a makefile with convenience methods for working with the bootstrap library.

+ **build** - `make build`
This will run the less compiler on the bootstrap lib and generate a bootstrap.css and bootstrap.min.css file.
The lessc compiler is required for this command to run.

+ **watch** - `make watch`
This is a convenience method for watching your less files and automatically building them whenever you save.
Watchr is required for this command to run.


AUTHORS
-------

**Mark Otto**

+ http://twitter.com/mdo
+ http://github.com/markdotto

**Jacob Thornton**

+ http://twitter.com/fat
+ http://github.com/fat


Copyright and License
---------------------

Copyright 2011 Twitter, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this work except in compliance with the License.
You may obtain a copy of the License in the LICENSE file, or at:

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.