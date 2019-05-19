

# Responsive Web Design Fundamentals

Course notes from the class by Udacity.



### DIPs and Hardware Pixels

Device Independent Pixels (DIPS) - what the browser reports . It relates pixels to a real distance. It will take up the same amount of space on a display regardless of the pixel density of that display.

Hardware Pixels - the physical, hardware pixels

Device Pixel Ratio (DPR) - ratio of Hardware Pixels to DIPs



### Meta Viewport Tag

`<meta name="viewport" content="width=device-width, initial-scale=1">`

`name="viewport"` - setting the viewport

`width=device-width` - instructs the page to match the screens width in DIPs - allows the page to reflow content to match the screen sizes, whether small or large

`initial-scale=1` - instructs browser to establish a 1:1 relationship between DIPs and CSS pixels (what we usually work with, and all we need to worry about)



### Max-Width

It is often best to set images to `max-width: 100%;`



### Tappable Elements on Mobile Devices

Tappable elements themselves should be at least 48px height and 48px width, since this is about how much our finger take up.

