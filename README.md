# RF prototyping boards

When designing radio frequency (RF) circuits, we cannot rely on traditional perfboards or breadboards. Suitable boards need a [ground plane](https://en.wikipedia.org/wiki/Ground_plane#Printed_circuit_boards)  (essential for reducing noise in RF circuits), and should have minimal parasitic capacitances and inductances. Breadboards are especially unsuited, due to their RF circuit altering parasitics (mainly created by the horizontal signal rails, and the vertical power rails).

In the same vein, RF protoboards should support SMT components, which have less parasitic inductance compared to their leaded counterparts.

*This repository presents boards suitable for prototyping RF circuits, ready to be sent to a PCB manufacturer.*

## Original work (ExpressPCB only)

[MegawattKS](https://www.youtube.com/@MegawattKS) gives an accessible [radio design lecture (YouTube)](https://www.youtube.com/watch?v=r_p7AHsSOdw&list=PL9Ox3wpnB0kqekAyz6blg4YdvoEMoJNJY), with [matching slides](https://ecefiles.org/radio-design-101-slides/), and an accompanying guide detailing [how to prototype RF circuits](https://ecefiles.org/rf-circuit-prototyping/).
It's quite a useful course for getting hands on experience and a non-math heavy intuition, using (comparatively) affordable tools, which are introduced as well: [NanoVNA and TinySA for radio design (YouTube)](https://www.youtube.com/watch?v=B7DFOq9rM_M&list=PL9Ox3wpnB0koBGofotI4xS8R0ct0FeYfv).

When you don't happen to have access to the very expensive RF equipment of a university laboratory, this course is ideal, as it was designed to measure and characterize the built RF circuits with the NanoVNA and the TinySA in mind. (Tools which are widely used in DIY/amateur communities, and accordingly have lots of documentation, tutorial videos, and useful addons available online.)

There is also a more advanced university level course ["Designing and Building Transmitters and Receivers"](https://ecefiles.org/rf-circuits-course-notes/) and its [part list](https://ecefiles.org/wp-content/uploads/2023/01/000b_ECE662_PartsList_F19.pdf).

Finally, MegawattKS kindly provided his [original design for ExpressPCB Plus](/original/RFprotoboard_Rev2_17nov22.rrb), which I used to take measurements of the various footprints and layout dimensions.

## Derived work (KiCad, many PCB manufacturers)

I faithfully redesigned the RF protoboard in KiCad, based on those measurements, to enable fabricating them with pretty much any PCB manufacturer.
The manual conversion was necessary, since the original boards are made for ExpressPCB, which uses a format exclusive to this manufacturer, with no export/import options. 

This resulted in two boards (out of the many variations I tried):

- The [standard version](/RF_ProtoBoard), with all the original dimensions and features being kept.

  <div align="center">
    <img src="images/RF_ProtoBoard_Front.png" alt="Front of standard version" title="Front of standard version"/>
    <div>Front</div>    
  </div>

  <br/>

  <div align="center">
    <img src="images/RF_ProtoBoard_Back.png" alt="Back of standard version" title="Back of standard version"/>
    <div>Back</div>
  </div>

- The [extended version](/RF_ProtoBoard_Extended), with the following changes compared to the standard version:
  - **added**: mounting holes
  - **added**: screw terminal for power (and pads to solder power wires onto)
  - **extended**: complete 4 pad U.FL connector footprints with silkscreen (for easier alignment)
  - **changed**: ground rings instead of a fully exposed ground plane
    - solder mask only exposes ground rings around the backside of plated through holes; ground rings should form nicer solder joints and hopefully ease solderability to the ground plane

  <br/>
  
  <div align="center">
    <img src="images/RF_ProtoBoard_Extended_Front.png" alt="Front of extended version" title="Front of extended version"/>
    <div>Front</div>    
  </div>

  <br/>

  <div align="center">
    <img src="images/RF_ProtoBoard_Extended_Back.png" alt="Back of extended version" title="Back of extended version"/>
    <div>Back</div>
  </div>
  
The screw terminal on the extended version reduces the amount of loose wires going off the board. Now, all the power wires from the 6 sub-modules can be routed to the centrally positioned pair of power pads, which have traces leading to the single central power screw terminal. The power pads on the backside of the board allow to add a decoupling/bulk capacitor.

## Fabricating the RF proto boards

The necessary ZIP files are available in the [fabrication directory](fabrication/), ready to be sent to a PCB manufacturer.
They are tuned for JLCPCB, but you can easily adjust the settings as needed when generating the gerber, drill and map files from within the KiCad projects (see [below](#generating-files-manually)).

### PCB ordering website options
- *Extended board version:* inform your manufacturer to keep the silkscreen for the U.FL connectors, since it's on the bare PCB substrate (no solder mask underneath). To do so, write a note in the order page remark field: "Keep the silkscreen on the solder mask openings".
- Select "Untented" for "Via Covering".
- *JLCPCB only*: under "Remove Order Number", select "Specify a location". The "JLCJLCJLCJLC" text on the B.Silkscreen layer [specifies the location of the order number](https://jlcpcb.com/help/article/50-How-to-remove-order-number-from-your-PCB).

### Generating files manually

The project is set up to work correctly with JLCPCB, with all the necessary layers selected and the options properly set.

- Standard board version:
  - Make sure "Do not tent vias" is enabled.
  - "JLCJLCJLCJLC" text on the B.Silkscreen layer:
    - For JLCPCB: do **not** enable "Subtract soldermask from silkscreen", otherwise the text will be clipped, and the ordering number will be placed at a random location.
    - For others: hide the text, as it will be unnecessary clutter.

- Extended board version:
  - Make sure "Do not tent vias" is enabled.
  - "JLCJLCJLCJLC" text on the B.Silkscreen layer:
    - For JLCPCB: keep the text visible, so the ordering number is not placed at a random location.
    - For others: hide the text, as it will be unnecessary clutter.
  - Do **not** enable "Subtract soldermask from silkscreen", unless the silkscreen for the U.FL connectors creates issues, because it is printed on the bare PCB substrate. If you keep the U.FL silkscreen, make sure to let the manufacturer know that the silkscreen on the bare PCB substrate is intentional. To do so, write a note in the order page remark field: "Keep the silkscreen on the solder mask openings".

Default plot settings (menu`File|Fabrications Output|Gerbers (.gbr)...`) for standard and extended board versions:

![KiCad 7 plot settings](images/PlotSettings.png "KiCad 7 plot settings")

Now, generate the gerber, the drill, and the map files. The results will be in the gerbers/ sub-directory. Put all the generated files in gerbers/ into a ZIP file, and upload them to your manufacturer.

See also: [How to generate Gerber and Drill files in KiCad 7 (JLCPCB)](https://jlcpcb.com/help/article/362-how-to-generate-gerber-and-drill-files-in-kicad-7).

### Experience with manufacturing

I fabricated the extended board version at JLCPCB. For my first (and so far only) order, I enabled "Confirm Production file", which turned out to be a good idea. Initially, they reduced the solder mask openings on the back side, which effectively removed the ground ring. Also, the silkscreen for the U.FL connectors on the front was removed and then, when communicating to readd them, they were clipped.

I suspect the wording in the remark field on the order page was the issue, so I updated it in this README to match their wordings more closely: "Keep the silkscreen on the solder mask openings" (same note is mentioned in ordering instructions above). The clipping was possibly due to the closeness to the SMD pads on the front. I was reviewing their changes directly and sending pictures comparing their version and my desired version, with arrows pointing out the differences too clarify, but maybe a note "Keep silkscreen close to copper pads unchanged." could help.

Similarily, for the reduced solder mask openings on the back side, a note saying "Solder mask openings on back side of PTH is intentionally covering the adjacent ground plane." However I suspect such a statement will not work, as in my experiece images worked best. Ideally, you could point that out in something like the Fab layer, adding arrows to say the crossing of two copper regions (ring around PTH and ground plane) is intentional.

In the production files (if you chose to review them), diameters of PTHs will be enlarged, but that is to account for the narrowing of the holes when copper plating them, and is normal. Otherwise, I saw minor dimension changes of pads, but its mostly cosmetic: the outer ground pads for the U.FL connectors was enlarged and moved a bit and is now protruding from the rectangular frame. I mostly would like to know why it happened -- possibly to account for the via size, but the change was minimal --, so I can account for it in other boards/situations, where it might be relevant. But it was not worth the effort to keep delaying production.

In general, watch out for some changes manufactures will automatically apply to your design: [relevant instructions when ordering at JLCPCB](https://jlcpcb.com/help/article/14-Instructions-for-ordering). Somewhat related: [How to Order Boards with Solder Mask Defined Pads (JLCPCB)](https://jlcpcb.com/help/article/84-How-to-Order-Boards-with-Solder-Mask-Defined-Pads).

I haven't sent the standard design to a PCB manufacturer yet. Let me know if there are any issues in manufacturability and what instructions you followed to be successful.

#### DFM (Design for manufacturability) analysis / checks

If you selected the "Confirm Production file" option, you will receive a RAR/ZIP file with several folders.
The [`ok` folder contains the production files](https://www.libreservo.com/en/articulo/how-check-jlcpcb-production-files) used by the manufacturer for fabrication, and your original design is found in the `yk` folder.

To review production files received from fabs such as PCBpartner or JLCPCB, you can use [iPCB-DFM](https://www.pcbpartner.com/iPCB-DFM). Given the screenshots I received, it seems to be the same software that JLCPCB uses for reviewing. In iPCB-DFM choose `File|Open odb` and select the TGZ file in The `ok` folder.

You can also simply do a manual visual compare using KiCad Gerber viewer, to see what changes the fab made.

If you want to check your design before submitting it to a fab, you can use [FreeDFM](https://www.my4pcb.com/net35/FreeDFMNet/FreeDFMHome.aspx).

## Recommended lead-free solder

After trying various lead-free solders, I can recommend Sn100Ni+ as a well flowing solder making nice shiny joints.

## SMD component kits and other useful parts

- https://www.amazon.de/gp/product/B08QGD9G7C/ref=ox_sc_act_image_1?smid=A343O8N8FO74B8&psc=1
- https://www.amazon.de/gp/product/B0795DX46R/ref=ox_sc_act_title_2?smid=A1CKTEOLLEJC1Q&psc=1
- TODO: screw terminal block that fits extended pcb
- M2.5 spacer rods, screws and nuts (nylon, or some other non-conductive material) for pcb mounting holes
- rubber feet with adhesive
- stethoscope camera with microphone (or stethoscope  microphone alone)
- https://www.ph2lb.nl/blog/index.php?page=xtal-adapter-for-nanovna
- https://www.ph2lb.nl/blog/index.php?page=qrp-labs-filter-adapter-for-nanovna
- https://www.ph2lb.nl/blog/index.php?page=rfsampler
<br/>

- https://www.ph2lb.nl/blog/index.php?page=component-measuring-adapter-for-nanovna
  
  Mostly for the manual, but NanoVNA Testboard Kit (see below) is better.

## Other parts (mentioned in MegawattKS' YouTube playlist)

- "NanoVNA" (lots of different versions - mine is the 4" screen NanoVNA-F)
- "TinySA" (some different types, but mainly different places to buy)
- "RF Demo Kit for NanoVNA-F - by deepelec" (The green board with all the cool Smith Charts and components)
- "NanoVNA Testboard Kit" (the little blue board the filter was built on)
- "SMA RF DC-Block DC to 6 GHz 50 Ohm"
- "Nooelec SMA Attenuator Kit - Bundle of 6pc 2W 50 Ohm SMA in-Line Attenuators"

<br/>

- "Interstellar Electronics SMD Professional Assortment Kit" (the surface mount parts box)
- "Inductor Sample Book" (goes by various names/vendors - but that should pull up useful hits)
- "50PCS IPEX U.FL SMD SMT Solder for PCB Mount Socket Jack Female RF Coaxial Connector"
- "U.FL to SMA Male Coaxial RG178 Low Loss Cable"

<br/>

- "6.5ft Low-Loss Coaxial Extension Cable RG58 (50 Ohm) SMA Male to SMA Female"

## Related perfboard designs

- https://github.com/electroniceel/protoboard
- https://github.com/jamesmunns/brick-mount
- https://github.com/hyves42/miniboard-protoboard
- https://github.com/mje-nz/protoboard
- https://github.com/AriaSalvatrice/synth-protoboard
- https://hackaday.com/2016/06/16/evaluating-the-unusual-and-innovative-perf-protoboard/
