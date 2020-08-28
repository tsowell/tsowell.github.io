---
layout: post
title:  "A custom Dreamcast keyboard"
---
I bought a custom mechanical keyboard from [WASD Keyboards][1] to use with my Dreamcast.

![A custom WASD V3 keyboard.](/assets/posts/dreamcast-usb-keyboard/keyboard.jpg){:width="60%" height="60%"}
![Keys on a keyboard.  The meta key has a Dreamcast swirl logo printed on it.](/assets/posts/dreamcast-usb-keyboard/swirl.jpg){:width="30%" height="30%"}

(I sent WASD [this SVG file][2] to use as the image for the custom Meta keys.
It's just the [Dreamcast logo from Wikipedia][3] with the text removed.)

[1]: https://www.wasdkeyboards.com/
[2]: /assets/posts/dreamcast-usb-keyboard/Dreamcast_logo_no_text.svg
[3]: https://commons.wikimedia.org/wiki/File:Dreamcast_logo.svg

When I ordered the keyboard I didn't have a plan for how to connect it to a
Dreamcast, but I wanted a solution that would fit inside the keyboard somehow
so that it would be a true Dreamcast keyboard.  My initial research was
pointing in the direction of a tiny FPGA board to do the USB-Maple translation,
but I stumbled on a much simpler way which I describe below.  I imagine it
could also work on other models of keyboards with detachable USB cables.

&nbsp;  

* TOC
{:toc}

&nbsp;  

### Total Control 5 with USB to PS/2 adapter

I had a [Total Control 5][4] PS/2 to Dreamcast adapter laying around which I
assumed would work with a USB to PS/2 adapter.  USB to PS/2 adapters are purely
mechanical and only work with keyboards that natively support PS/2.  Because my
keyboard is a WASD V3, I had to [downgrade to the V2 firmware][5] before it
would work with a USB to PS/2 adapter.  One downside to the V2 firmware is that
it doesn't support programming the Num/Caps/Scroll Lock indicator LED colors
(which in this case should be orange, of course), but I'm not sure that the
Dreamcast can even turn on the keyboard LEDs as the official Dreamcast
keyboards don't have any.

[4]: https://segaretro.org/Total_Control_5
[5]: https://support.wasdkeyboards.com/hc/en-us/articles/360018518874-Keyboard-Firmware-Updates

The keyboard to USB cable to USB to PS/2 adapter to Total Control 5 to
Dreamcast setup works, but it is not pretty.

![A Dreamcast with a Total Control 5 PS/2 adapter plugged into the controller port.  A USB to PS/2 controller is plugged into the Total Control 5, and a USB cable is plugged into the USB to PS/2 controller.](/assets/posts/dreamcast-usb-keyboard/stack.jpg){:width="75%" height="75%"}

&nbsp;  

### Total Control 5 with a Dreamcast controller cable

The aesthetics could be improved by putting a cable between the Dreamcast and
the Total Control 5.

What's inside a Total Control 5 anyway?  There isn't much more than two
connectors, an IC, and a crystal.  The IC is a [Parallax SX20AC/SS][6]
configurable communications controller (it would be interesting to try to dump
the EEPROM).

[6]: https://www.parallax.com/sites/default/files/downloads/SX20AC-SX28AC-Datasheet-v1.7.pdf

![A Total Control 5 adapter with the plastic shell removed](/assets/posts/dreamcast-usb-keyboard/tc50.jpg){:width="40%" height="40%"}
![A Total Control 5 adapter PCB viewed from the side](/assets/posts/dreamcast-usb-keyboard/tc51.jpg){:width="40%" height="40%"}

I harvested the cable from a Dreamcast controller and soldered it in place of
the Total Control 5's controller connector.  You can see in the third image
below how it needs to be wired (the "green" wire is soldered to the same pad as
the black ground wire, but on bottom of the PCB).

![A Dreamcast controller cable plugged into a Dreamcast controller PCB](/assets/posts/dreamcast-usb-keyboard/controller0.jpg){:width="20%" height="20%"}
![A Dreamcast controller cable with the stress relief cut off](/assets/posts/dreamcast-usb-keyboard/controller1.jpg){:width="20%" height="20%"}
![A Total Control 5 adapter PCB with a Dreamcast controller cable soldered in place of the Dreamcast controller connector](/assets/posts/dreamcast-usb-keyboard/tc5_dc0.jpg){:width="50%" height="50%"}

This is a slight improvement as this way the adapter stack can be moved out of
sight.

![A Total Control 5 adapter with a Dreamcast controller in place of the Dreamcast controller connector connected to a USB to PS/2 adapter and a USB cable](/assets/posts/dreamcast-usb-keyboard/tc5_dc2.jpg){:width="80%" height="80%"}

&nbsp;  

### Fitting it all "inside" the keyboard

While I initially wanted to put everything completely inside the case, I became
hesitant to do so because the USB port would no longer be accessible for
firmware updates and because WASD's cases are difficult to open.

In search of a compromise, I realized that there might be room to hide the
Total Control 5 PCB in the base of the keyboard where the USB cable plugs in.
The PS/2 connector would have to be removed, and the PCB would need to be wired
directly to a male USB connector instead.

(In this photo the keyboard's female USB Type-C connector is barely visible at
the bottom of the depression.)

![The back of a keyboard showing the USB cable space](/assets/posts/dreamcast-usb-keyboard/usb_empty.jpg){:width="60%" height="60%"}

I ordered from eBay this little USB Type-C connector that breaks the pins out
to solder pads, and it fit perfectly into the depression with the Total Control
5 PCB once the PS/2 connector was removed.

![A USB Type-C connector with solder pads](/assets/posts/dreamcast-usb-keyboard/usb_plug.jpg){:width="40%" height="40%"}
![The back of a keyboard with a Total Control 5 PCB and a USB Type-C connector wedged into the USB cable space](/assets/posts/dreamcast-usb-keyboard/fit.jpg){:width="40%" height="40%"}

Here are the USB connections to the Total Control 5 PCB.  On a USB Type-C
connector, pin A7 is D-, and pin A6 is D+.  I added a little tape to the side
of the Total Control 5 PCB to prevent the USB connector from shorting to it.

![A Total Control 5 adapter PCB with the PS/2 connector removed and with the USB pads labelled](/assets/posts/dreamcast-usb-keyboard/tc5_labels.jpg){:width="50%" height="50%"}
![A Total Control 5 adapter PCB with a USB Type-C connector soldered in place of the PS/2 connector](/assets/posts/dreamcast-usb-keyboard/tc5_dc_usb.jpg){:width="40%" height="40%"}

The USB connector and the Dreamcast controller cable wires keep it wedged
securely in place, and none of the components are tall enough to stick out of
the depression.  It's pretty snug, so I don't think anything extra needs to be
done to secure it.

![The back of a keyboard with a Total Control 5 PCB and a wired-up USB Type-C connector wedged into the USB cable space](/assets/posts/dreamcast-usb-keyboard/complete_plug.jpg){:width="60%" height="60%"}

&nbsp;  

### The finished product

![The back of a keyboard with a Total Control 5 PCB and a wired-up USB Type-C connector wedged into the USB cable space from farther away](/assets/posts/dreamcast-usb-keyboard/complete_back.jpg)

![The front of a keyboard with a Dreamcast cable coming out of it](/assets/posts/dreamcast-usb-keyboard/complete_front.jpg)

![A Dreamcast connected to a monitor, keyboard, and mouse](/assets/posts/dreamcast-usb-keyboard/complete.jpg)

Now I just need to find a way to prematurely yellow the white plastic so that
it matches the rest of my peripherals.  Or leave it out in the sun for a decade
or two.

