# Pimp my GRUB

<img src="https://user-images.githubusercontent.com/46305144/185753718-b48f0e74-f289-414d-892b-bb7071f9fcab.png" />

<p align="center">
  <img src="https://github.com/GalsenDev221/made.in.senegal/blob/master/assets/badge.svg" />
</p>

In this tutorial, I'll show you how we can change the default appearance of the GRUB.


## 🤔 What is GRUB?

GNU GRUB is a very powerful bootloader, which can load a wide variety of free operating systems, as well as proprietary operating systems. GRUB stands for **GRand Unified Bootloader** and is designed to address the complexity of booting a personal computer.
Currently we are on version 2.0.6, a complete upgrade of the previous version. In this version, we have some new features like a graphical menu.


## 💄 Theme file definition

GRUB's graphical menu can be customized using a theme definition file. This is a plain text file (usually named `theme.txt`). This file generally has two types of statements:
- **global property**  
These are properties defined at the top level of our theme file definition. This syntax is: `title-text: "Hello World"`
- **component property**  
They are created by prefixing the type of component with a ’+’ sign: `+ label { text="GRUB" font="aqui 11" color="#8FF" }`


## 📹 Install Grub2-theme-preview

[grub2-theme-preview](https://github.com/hartwork/grub2-theme-preview) is a very handy tool to test your new grub theme without having to reboot your machine every time you make a change.

It takes a theme folder, creates a temporary bootable image using `grub2-mkrescue` and launches that image in a virtual machine using KVM/QEMU.

First we need to make sure to install these dependencies:

```bash
sudo apt install grub-common qemu-system-x86 ovmf mtools xorriso
```

To install the package

```bash
pip3 install --user grub2-theme-preview
```  

> **🔹 NOTE 🔹** For this command to work, you obviously need to install `python3` and `python3-pip` on your system.  

Now we can preview our grub theme with this command.

```bash
grub2-theme-preview <path_of_theme_folder> --resolution 1024x640
```  

> **🔹 NOTE 🔹** By default the resolution of the QEMU virtual machine is `800x600`. That's why in the command we specified a resolution of `1024x640`. If you want to know which resolution are accepted you can check this [link](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions#Linux_video_mode_numbers).


## 🤯 Morphin Time

Now that all the boring theory is done, we can get to the fun part.

![galsen-grub](https://user-images.githubusercontent.com/46305144/185755552-6be51616-6f81-418c-a0d4-6f45249ba850.png)

This is what we want to achieve. We first need to create a folder for our theme and a theme definition file `theme.txt`

```bash
mkdir galsen_grub
cd galsen_grub
touch theme.txt
```

Now let's add some properties to our theme definition file.


### Global properties

We need to change the background image and the title of our GRUB.

The GRUB uses [PFF2 font format](http://grub.gibibit.com/New_font_format). `grub-mkfont` utility should be used to convert BDF, PCF or TTF fonts to PFF2 format. Output file should have `pf2` extension and should be placed inside the theme directory. The font used in this demo is [Permanent Marker](https://fonts.google.com/specimen/Permanent+Marker).

To convert the font, we input

```bash
grub-mkfont PermanentMarker-Regular.ttf -o ./PermanentMarker_40.pf2 -v --size 40

# Output of this command
Font name: Permanent Marker Regular 40
Max width: 50
Max height: 45
Font ascent: 44
Font descent: 13
Number of glyph: 229
```

> **🔹 NOTE 🔹** You need to run this command again to create another font with the size of 20


In the output we can see the font name. This will be useful in the theme definition file.


The last step is to copy the background file into the `galsen_grub` folder and add these line to `theme.txt`.

```conf
title-text: "Grubu Kanaa"
title-color: "#fff"
title-font:  "Permanent Marker Regular 40"
desktop-image: "background.png"
```

> **🔹 NOTE 🔹** I named my image `background.png` but you can choose whatever you like for the name.  


For now your `galsen_grub` folder should like this.

```bash
./galsen_grub
├── PermanentMarker_20.pf2
├── PermanentMarker_40.pf2
├── background.png
└── theme.txt
```

### Boot Menu component

Now come the most difficult part of this demo (or maybe not 😄), the boot menu. The tricky part is the **Styled Box Format** (we use it to set the background of our boot menu to multiple images).

![image_slices](https://user-images.githubusercontent.com/46305144/185755821-f2da095a-c152-4026-88e3-bef0fb6be86c.gif)

A styled box is composed of 9 rectangular (and potentially empty) regions, which are used to seamlessly draw the styled box on screen based on an image.

![grub-theme-slices](https://user-images.githubusercontent.com/46305144/185755835-1a114b21-8349-47ec-ad3d-07ad80e04435.png)

To create these slices you can use something like **Inkscape** or **Figma**. (Maybe I'll record a video on how to do it on Figma).

We just need to add these lines to our theme definition file.

```conf
+ boot_menu {
  left = 50%-300
  top = 50%-160
  width = 600
  height = 320
  menu_pixmap_style = "boot_menu_*.png"
  item_color = "#fff"
  item_spacing = 5
  selected_item_color = "#035AC4"
  scrollbar = true
  item_height = 40
  item_padding = 15
  item_spacing = 15
  item_font =  "Permanent Marker Regular 20"
}
```

Now don't forget to copy the slices into the `galsen_grub` folder.


By now the structure of `galsen_grub` should like this.

```bash
./galsen_grub
├── PermanentMarker_20.pf2
├── PermanentMarker_40.pf2
├── background.png
├── boot_menu_c.png
├── boot_menu_e.png
├── boot_menu_n.png
├── boot_menu_ne.png
├── boot_menu_nw.png
├── boot_menu_s.png
├── boot_menu_se.png
├── boot_menu_sw.png
├── boot_menu_w.png
└── theme.txt
```

### Progress Bar component

The final part is the progress bar, a horizontal bar that indicates the time remaining until the highlighted menu item is booted.

We will also another Stylex Box image for this component.

```conf
+ progress_bar {
  id = "__timeout__"
  width = 400
  top = 90%
  left = 50%-200
  bar_style = "progress_bar_*.png"
  highlight_style = "progress_highlight_*.png"
  highlight_overlay = true
}
```

The final structure of `galsen_grub`

```bash
./galsen_grub
├── PermanentMarker_20.pf2
├── PermanentMarker_40.pf2
├── background.png
├── boot_menu_c.png
├── boot_menu_e.png
├── boot_menu_n.png
├── boot_menu_ne.png
├── boot_menu_nw.png
├── boot_menu_s.png
├── boot_menu_se.png
├── boot_menu_sw.png
├── boot_menu_w.png
├── progress_bar_c.png
├── progress_bar_e.png
├── progress_bar_w.png
├── progress_highlight_c.png
├── progress_highlight_e.png
├── progress_highlight_w.png
└── theme.txt
```


To preview the final result

```bash
grub2-theme-preview . --resolution 1024x640
```

> **🔹 NOTE 🔹**  To run this command you need to be inside of `galsen_grub` folder.


## 🔚 Last step

Now that we've written our theme and previewed it, we need to tell our system to use it.

Create a `themes` directory in `/boot/grub/`. This is where our themes will live (we can store multiple themes here).

```bash
sudo mkdir /boot/grub/themes
```

Copy our theme into the newly created folder

```bash
sudo mv galsen_grub /boot/grub/themes/
```

To make the `bootloader` use our theme, we should add a `GRUB_THEME` parameter in file `/etc/default/grub`. We need to edit this file as **root**.

```conf
GRUB_THEME=/boot/grub/themes/galsen_grub/theme.txt
```

Every time we update this file, we need to run `update-grub2` in order to regenerate the `bootloader` configuration file (`/boot/grub/grub.cfg`).

```bash
sudo update-grub2
```

> **🔹 NOTE 🔹**  In case there is no `update-grub` in your system, you can run `grub2-mkconfig -o /boot/grub/grub.cfg`.


## 📚 Resources

- [Grub2 Documentation](https://www.gnu.org/software/grub/manual/grub/grub.html#Theme-file-format)
- [Browse other GRUB themes](https://www.pling.com/browse?cat=109&ord=latest)
- [Getting started with GRUB Theming](https://github.com/VandalByte/grub-tweaks)


## TODO

- [x] Documentation
- [x] Preview image of the GRUB
- [x] Resource links
- [ ] Link to the slides
- [ ] Make an install script
