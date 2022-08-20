# Grub Theme Definition Properties

## Global property

The global property statement which appears only once

```conf
global_props: <value>
```

The following table describes each item of the global property statement:

| Item Name          | Description                                                    | Value Type               | Default Value      |
| ------------------ | -------------------------------------------------------------- | ------------------------ | ------------------ |
| `title-text`       | Sets a title for the text                                      | String                   | Grub Boot Menu     |
| `title-font`       | Font used for the title text                                   | Font name(pf2 extension) | Unknown Regular 16 |
| `title-color`      | Color of the title text                                        | Color value              | Black              |
| `message-font`     | Font used for GRUB messages                                    | Font name                | Unknown Regular 16 |
| `message-color`    | Color used for GRUB messages                                   | Color value              | White              |
| `message-bg-color` | Background color for GRUB messages                             | Color value              | Black              |
| `desktop-image`    | Background image for the menu                                  | Image file               |                    |
| `desktop-color`    | Color of the background if a background image is not specified | Color value              | White              |
| `terminal-box`     | Image used for the terminal box                                | Styled Box               | Plain black box    |
| `terminal-font`    | Font used for the terminal box                                 | Font name                | Fixed 10           |

> **🔹 NOTE 🔹** The default value is applied if an item name is not specified.  


## Components

The component statement which must be prefixed with `+`. The properties of this statement must be enclosed within braces.

```conf
+ component_props {
  prop_1 = <value>
  prop_2 = <value> 
}
```

We have a total of 8 components that we can use in the theme definition file.

### Common options

The following properties are supported by all components:

| Property name | Description                                                                                                                                       | Value Type                                                                                                                                                                                                                                                               |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `left`        | The distance from the left border of container to left border of the object.                                                                               | `<value>` in pixel, `<value>%` in percent, or a mix of both                                                                                                                                                                                                              |
| `top`         | The distance from the left border of container to left border of the object                                                                                | Same as `left`                                                                                                                                                                                                                                                           |
| `width`       | The width of the object.                                                                                                                                   | Same as `left`                                                                                                                                                                                                                                                           |
| `height`      | The height of the object.                                                                                                                                  | Same as `left`                                                                                                                                                                                                                                                           |
| `id`          | The identifier of the component. This can be any arbitrary string. The ID can be used by scripts to refer to various components in the GUI component tree. | Currently, there is one special ID value that GRUB recognize: `__timeout__`. Component with this ID will be updated by GRUB and will indicate time elapsed to an automatic boot of the default entry. Affected components: “label“, “circular_progress“, “progress_bar“. |


### Boot Menu

*Component name: `boot_menu`*

The `boot_menu` component sets the visual style of the boot menu. This component must be included in the theme definition file. The table below describes each item of the boot menu's property list:

| Property Name                | Description                                                                                       | Value Type  | Default Type       |
| ---------------------------- | ------------------------------------------------------------------------------------------------- | ----------- | ------------------ |
| `item_font`                  | Font used for the menu items.                                                                     | Font name   | Unknown Regular 16 |
| `selected_item_font`         | Font used for the selected menu items. If not set, this will inherit the font used by `item_font` | inherit     |                    |
| `item_color`                 | Color of the menu items.                                                                          | Color value | Black              |
| `selected_item_color`        | Color of the selected item menu. If not set, this will inherit the color used by `item_color`     | Color value | inherit            |
| `item_height`                | Height of each menu item.                                                                         | Numeric     | 42 (pixels)        |
| `item_padding`               | Amount of space to leave on either side of the menu items.                                        | Numeric     | 14 (pixels)        |
| `item_spacing`               | Amount of space between menu items.                                                               | Numeric     | 16 (pixels)        |
| `icon_width`                 | Width of the menu item icons.                                                                     | Numeric     | 32 (pixels)        |
| `icon_height`                | Height of the menu item icons.                                                                    | Numeric     | 32 (pixels)        |
| `item_icon_space`            | Space to leave between a menu item's icon and its text.                                           | Numeric     | 4 (pixels)         |
| `menu_pixmap_style`          | Image used for the menu background.                                                               | Styled Box  |                    |
| `selected_item_pixmap_style` | Image used to highlight the selected item.                                                        | Styled Box  |                    |
| `scrollbar`                  | Show or hide the scrollbar.                                                                       | Boolean     | false              |
| `scrollbar_frame`            | Image used for the scrollbar's frame.                                                             | Styled Box  |                    |
| `scrollbar_thumb`            | Image used for the scrollbar's thumb.                                                             | Styled Box  |                    |
| `visible`                    | Show or hide the boot menu.                                                                       | Boolean     | true               |

> **🔹 NOTE 🔹** The boot menu items will not be shown if the boot menu component is not included in the theme definition file.  


### Label

*Component name: `label`*

The `label` component displays a single line of text on the screen. The table below describes each item of the label's property list:

| Property Name | Description                                                                  | Value Type  | Default Value      |
| ------------- | ---------------------------------------------------------------------------- | ----------- | ------------------ |
| `text`        | Text to display.                                                             | String      |                    |
| `align`       | Horizontal alignment of the text. Possible values are left, center or right. | String      | left               |
| `font`        | Font used for the text.                                                      | Font name   | Unknown Regular 16 |
| `color`       | Color of the text.                                                           | Color value | Black              |
| `visible`     | Show or hide the text.                                                       | Boolean     | true               |


### Image

*Component name: `image`*

The `image` component displays an image on the screen. The image is scaled to fit the size specified by the width and height properties. The table below describes each item of the image's property list:

| Property Name | Description                | Value Type | Default Value |
| ------------- | -------------------------- | ---------- | ------------- |
| `file`        | Absolute path to the image | String     |               |


### Progress Bar

*Component name: `progress_bar`*

Displays a solid color or styled horizontal progress bar that indicates the time remaining until the
highlighted menu item is booted. The table below describes each item of the progress bar's property list:

| Property Name     | Description                                                                                                                                                         | Value type  | Default value      |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------------ |
| `bg_color`        | Background color for a solid color progress bar.                                                                                                                    | Color value | Gray               |
| `fg_color`        | Foreground color for a solid color progress bar.                                                                                                                    | Color value | Light Gray         |
| `border_color`    | Border color for a solid color progress bar.                                                                                                                        | Color value | Black              |
| `show_text`       | Show or hide the countdown text.                                                                                                                                    | Boolean     | true               |
| `text`            | Text to show on the progress bar. Possible values are: @TIMEOUT_NOTIFICATION_SHORT@ @TIMEOUT_NOTIFICATION_MIDDLE@ @TIMEOUT_NOTIFICATION_LONG@, or any valid string. | String      |                    |
| `text_color`      | Color of the text.                                                                                                                                                  | Color value | Black              |
| `font`            | Font used for the text.                                                                                                                                             | Font name   | Unknown Regular 16 |
| `bar_style`       | Background image for the styled progress bar. If this is not specified, a solid color progress bar is displayed.                                                    | Styled Box  |                    |
| `highlight_style` | Foreground image for the styled progress bar. If this is not specified, a solid color progress bar is displayed.                                                    | Styled Box  |                    |
| `start`           | Start value of the progress bar. Should not be set manually.                                                                                                        | Numeric     |                    |
| `end`             | End value of the progress bar. Should not be set manually.                                                                                                          | Numeric     |                    |
| `value`           | Current value of the progress bar. Should not be set manually                                                                                                       | Numeric     |                    |
| `visible`         | Show or hide the progress bar                                                                                                                                       | Boolean     | true               |


### Circular Progress Bar

*Component name: `circular_progress`*

Displays a circular progress bar that indicates the time remaining until the highlighted menu is booted. The table below describes each item of the progress bar's property list:

| Property Name    | Description                                                    | Value Type | Default Type |
| ---------------- | -------------------------------------------------------------- | ---------- | ------------ |
| `center_bitmap`  | Image to show at the center of the progress bar                | Image file |              |
| `tick_bitmap`    | Image to use for the tick marks                                | Image file |              |
| `num_ticks`      | Number of ticks for a full circle                              | Numeric    | 64           |
| `start_angle`    | Position of first tick mark to disappear or appear             | Numeric    | -64          |
| `tick_disappear` | Sets whether ticks should disappear or appear.                 | Boolean    |              |
| `start`          | Start value of the progress bar. Should not be set manually.   | Numeric    |              |
| `end`            | End value of the progress bar. Should not be set manually.     | Numeric    |              |
| `value`          | Current value of the progress bar. Should not be set manually. | Numeric    |              |
| `visible`        | Show or hide the progress bar.                                 | Boolean    | true         |


### Vertical Box

*Component name: `vbox`*

The `vbox` component is a container which lays out other components within it vertically staring at the top. It sets the width of each component to the width of the widest component. The components retain their respective height.

`vbox` has all the common options except `width` and `height` which are ignored.


### Horizontal Box

*Component name: `hbox`*

The `hbox` component is a container component which lays out other components within it horizontally starting from the left. It sets the height of each component to the height of the tallest component. The components retain their respective width.

`hbox` has all the common options except `width` and `height` which are ignored.


### Canvas

*Component name: `canvas`*

The `canvas` component is a container component which allows for the placement of other components within it according to their individual positions and sizes. Unlike the `vbox` and `hbox` components, it does not change the components sizes.

`canvas` has all the common options .

> **🔹 NOTE 🔹** A component property's default value is applied only it the respective property is excluded from the component statement line.  


## Data Types

### Theme colors

There are three ways to specify a color value in the theme file:

- HTML-style - "#RRGGBB" or "#RGB", where R, G, B are hexadecimal values (e.g. "#D4E0EC")
- Comma separated decimal RGB values. e.g. "(127,127,255)"
- [SVG 1.0](http://www.w3.org/TR/css3-color/#svg-color) color names. e.g. cornflowerblue. Written in lowercase.


### Font name

Grub2 uses [PFF2 font format](http://grub.gibibit.com/New_font_format). `grub-mkfont` utility should be used to convert BDF, PCF or TTF fonts to PFF2 format. Output file should have `pf2` extension and should be placed to the theme directory.

In the theme file full font name and size should be used. (e.g. "Droid Sans Mono Regular 11")


### Numeric

Coordinates and lengths are specified using numeric format.  There are three ways to specify a numeric value:

- Absolute value - in pixels (e.g. 340)
- Relative value - in percentages of parent container's width/height (or screen if parent is root element) (e.g. 40%)
- Combined value - combination of two previous types (e.g. 50%-120). No white spaces are allowed.


### String

A string is a sequence of characters enclosed in double-quotes, e.g.: "Edit entry"


### Boolean

A boolean value can be: true or false


### Image file

An absolute path to a valid image file. Allowed formats are: PNG, TGA, JPG; transparency is supported. The image should be at the theme directory.


### Styled box

One of the most important features for customizing the layout is the use of *styled boxes*. A styled box is composed of 9 rectangular (and potentially empty) regions, which are used to seamlessly draw the styled box on screen based on an image.


```
Northwest Slice      North Slice        Northeast Slice
    (nw)                 (n)                (ne)

West Slice           Center Slice       East Slice
    (w)                  (c)                (e)

Southwest Slice      South Slice        Southeast Slice
    (sw)                 (s)                (se)
```

Any missing slice is left empty. Files with slices should be placed in the theme directory. The slices must be named according to this format `FILENAME_SLICE.EXT`, where

-   FILENAME - the name of graphical element, the same for all parts of one element ("boot_menu")
-   SLICE - slice's name ("sw")
-   EXT - extension ("png")

So, the filename for our example (South-west region of the "boot_menu" element) will be `boot_menu_sw.png`. 

To support any size of box on screen, the center slice and the slices for the top, bottom, and sides are all scaled to the correct size for the component on screen, using the following rules:

1.  The edge slices (north, south, east, and west) are scaled in the direction of the edge they are adjacent to. For instance, the west slice is scaled vertically.
2.  The corner slices (northwest, northeast, southeast, and southwest) are not scaled.
3.  The center slice is scaled to fill the remaining space in the middle.

