# RF prototyping boards

When designing radio frequency (RF) circuits, we cannot rely on traditional perfboards or breadboards. Suitable boards need a [ground plane](https://en.wikipedia.org/wiki/Ground_plane#Printed_circuit_boards)  (essential for reducing noise in RF circuits), and should have minimal parasitic capacitances and inductances. Breadboards are especially unsuited, due to their RF circuit altering parasitics (mainly created by the horizontal signal rails, and the vertical power rails).

In the same vein, RF protoboards should support SMT components, which have less parasitic inductance compared to their leaded counterparts.

*This repository presents boards suitable for prototyping RF circuits, ready to be sent to a PCB manufacturer.*

## Original work (ExpressPCB only)

[MegawattKS](https://www.youtube.com/@MegawattKS) gives an accessible [radio design lecture (YouTube)](https://www.youtube.com/watch?v=r_p7AHsSOdw&list=PL9Ox3wpnB0kqekAyz6blg4YdvoEMoJNJY), with [matching slides](https://ecefiles.org/radio-design-101-slides/), and an accompanying guide detailing [how to prototype RF circuits](https://ecefiles.org/rf-circuit-prototyping/).
It's quite a useful course for getting hands on experience and a non-math heavy intuition, using (comparatively) affordable tools: [NanoVNA and TinySA for radio design (YouTube)](https://www.youtube.com/watch?v=B7DFOq9rM_M&list=PL9Ox3wpnB0koBGofotI4xS8R0ct0FeYfv).

When you don't happen to have access to the very expensive RF equipment of a university laboratory, this course is ideal, as it was designed to measure and characterize the built RF circuits with the NanoVNA and the TinySA in mind. (Tools which are widely used in DIY/amateur communities, and accordingly have lots of documentation, tutorial videos, and useful addons available online.)

There is also a more advanced university level course ["Designing and Building Transmitters and Receivers"](https://ecefiles.org/rf-circuits-course-notes/) and its [part list](https://ecefiles.org/wp-content/uploads/2023/01/000b_ECE662_PartsList_F19.pdf).

Finally, MegawattKS kindly provided his [original design for ExpressPCB Plus](RFprotoboard_Rev2_17nov22.rrb), which I used to take measurements of the various footprints and layout dimensions.

## Derived work (KiCad, many PCB manufacturers)

I faithfully redesigned the RF protoboard in KiCad, based on those measurements, to enable fabricating them with pretty much any PCB manufacturer.
The manual conversion was necessary, since the original boards are made for ExpressPCB, which uses a format exclusive to this manufacturer, with no export/import options. 

This resulted in two boards (out of the many variations I tried):

- The [standard version], with all the original dimensions and features being kept.

- The [extended version], with the following changes compared to the standard version:
  - **added**: screw terminal for power
  - **added**: mounting holes
  - **extended**: complete 4 pad U.FL connector footprints with silkscreen (for easier alignment)
  - **changed**: ground rings instead of a fully exposed ground plane
    - solder mask only exposes ground rings around the backside of plated through holes; ground rings should form nicer solder joints and hopefully ease solderability to the ground plane
  
The screw terminal on the extended version reduces the amount of loose wires going off the board. Now, all the power wires from the sub-boards can be routed to the centrally positioned pair of power pads, which have traces leading to the single central power screw terminal. The power pads on the backside of the board allow to add a decoupling/bulk capacitor.

TODO: add 3d renderings of the boards, front and back side

## Other RF prototyping board designs

While doing some research on the topic, I found the following alternatives, you might find useful as well:
Several alternative designs exists (TODO: add references). 
