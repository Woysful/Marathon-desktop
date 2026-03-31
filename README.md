# Marathon-desktop

It’s important to note that this guide is intended for KDE Plasma users, but some of the content—such as desktop wallpapers or ASCII art—can also be used with other desktop environments or even other operating systems.

### 1. Taskbar
First, you should configure the top and bottom panels, because their sizes will affect the desktop grid.
I’ll list my settings as recommendations, but feel free to change them. Keep in mind that if you change the sizes, you’ll have to adjust the desktop wallpaper to fit your grid yourself (I’ll go into more detail about this below).

For the bottom panel, I use the `default panel`, and for the top panel, the `Application menu bar`. Both panels have a height of `44`

To customize the appearance, I use the third-party widgets `Panel Colorizer` and `Simple Separator`. For the clock and calendar, I use `HTML Clock for Plasma 6`

First, place the widgets you’d like to see on the panels. For the top panel, install two instances of `HTML Clock for Plasma 6` (one will serve as the clock, and the other will display the date); the remaining widgets are up to you. In my setup, I’ve also placed widgets for adjusting monitor brightness and various system monitors for CPU, GPU, and network. In the top-right corner, I’ve placed a media player and a color picker. I centered the Global Menu using two spacers.

On the bottom panel, at the bottom right, I placed a button to hide all windows, system settings, an email client (in my case, Thunderbird, which I’ve assigned a different icon to), and the system tray. In the center are the Application Launcher and Task Manager. All elements are separated using simple separator widgets with the following settings:
```
Length: 100
Thickness: 1
Custom color: #7f7f7f
Opacity: 30
```
The window hiding, settings, and mail widgets are additionally wrapped in a `Margin Separator` to reduce their size.

Let’s move on to configuring the widgets

**Panel Colorizer**.

Answering the question: why not just share presets? Because Panel Colorizer barelly hold itself together and simply refuses to save the preset configuration file for some reason. So you’ll have to configure everything manually.

You need to place one widget on the top panel and one on the bottom panel (you can place them anywhere, since the widget itself is transparent).
Go to the Panel Colorizer settings on the bottom panel, navigate to the Appearance section, select the Panel element, then enable customization for the Normal state below. On the Color tab, select `Color source: Image` and specify the path to the `background_noise.png` file.

Now for the top panel.
In the Panel Colorizer settings, hide the native panel. Pick a `Widget` from dropdown list and set `margin 6` for both top and bottom in shape menu. Then, on the Preset Overrides tab, you’ll need to create several overrides that can be applied to individual widgets.
- Disable - `Color -> Alpha 0.00` Apply to every spacer
- Round_Left / Round_Right - `Shape -> Radius 20` - Widgets in the left corner
- Round_Sharp - `Shape -> Radius 6` - Widgets in the right corner
- Color_Yellow - `Color -> Gradient #8dba07:0.875 #b1ea06:0.875` - Clock widget
- Color_Red - `#c4091f` - Date widget
- Color_Grey - `Color -> Custom #9e9eab` - Widgets in the left corner
- Color_Grey_Dark - `#25262d` - Widgets in the right corner
- Color_Bronze - `#957056`

**HTML Clock for Plasma 6**

First, let’s set up an element that will display the time.

To start, you need to enable custom presets:
`General -> [x] Use user layout -> Slot 1`

Then place the code in `User Layout 1`:
```
<html>
<body style="margin: ; padding: 0; width: 100%; height: 100%;">
  <table width="100%" height="100%" cellpadding="0" cellspacing="0" style="margin-left: 10; margin-right: 15;">
    <tr>
      <td align="center" valign="middle">
        <table cellpadding="0" cellspacing="4">
          <tr>
            <td valign="middle">
              <img src="/home/yui/Desktop/Marathon/Taskbar/Marathon_Logo_Black.svg" width="22" height="22" >
            </td>
            <td valign="middle">
              <span style="font-size: 18px; font-family: 'Marathon Shapiro'; color: #101010;">{hh}:{ii}</span>
            </td>
          </tr>
        </table>
      </td>
    </tr>
  </table>
</body>
</html>
```
Here, you need to edit the path to the marathon logo SVG file and don’t forget to install the fonts.

Do the same for the second date widget:
```
<html>
<body style="margin: ; padding: 0; width: 100%; height: 100%;">
  <table width="100%" height="100%" cellpadding="0" cellspacing="0" style="margin-left: 8; margin-right: 5;">
    <tr>
      <td align="center" valign="middle">
        <table>
          <tr>
            <td valign="middle">
              <span style="font-size: 16px; font-family: 'KH Interference'; color: #1111111;">{dd}.{MMM}</span>
            </td>
          </tr>
        </table>
      </td>
    </tr>
  </table>
</body>
</html>
```

Customize the remaining widgets as you see fit.

### 2. Desktop background
I didn’t mention the recommended sizes for the top and bottom panels for no reason, because by following these dimensions and setting the icon size to small-medium, you’ll be able to use my desktop image right away. But for those who’ve decided to change the dimensions, you’ll need to edit the image. Luckily for you, I’ve attached an Affinity project file, so this task will be much easier.

First, you’ll need to calculate the desktop grid size. To do this, I temporarily enable the top panel background display, arrange some files on the desktop vertically, and count their maximum number. Then, in the editor, I measure the distance between the top and bottom panels and divide that value by the number of items. I do the same horizontally. This way, I can build a grid and determine the size of each cell. In my case, it’s 99x96 pixels.

### 3. Terminal
I use Konsole and fastfetch, so the steps in your setup may differ.

**Konsole color palette:**
I’ve attached the profile and color scheme files, so you need to place all `.colorscheme` and `.profile` files in `~/.local/share/konsole/`. Then pick one in the settings.

**fastfetch**
First, you need to generate the fastfetch config file with `fastfetch --gen-config`. It will tell you which directory the file was created in; that’s where we’ll go. In my case, it’s `~/.config/fastfetch/`

We place the files with ASCII images in this directory, and then edit the configuration file:
```
{
  "$schema": "https://github.com/fastfetch-cli/fastfetch/raw/master/doc/json_schema.json",
  "modules": [
    "title",
    "separator",
    "os",
...
...
...
    "break",
    "colors"
  ],
  "logo": {
    "type": "file",
    "source": "/home/yui/.config/fastfetch/MIDA/Main_text.txt"
  }
}
```
This is roughly what my file looks like; at the end, I've specified the path to the image file. You'll need to change it to your own path.

---
Big thanks to discord user `@opelzafiri` for uploading fonts
