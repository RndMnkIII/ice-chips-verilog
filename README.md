<img src="images/proj_icon_a.svg" title="IceChips" align="right" width="6.124%">
<img src="images/proj_icon_b.svg" title="IceChips" align="right" width="3.484%">
<img src="images/proj_icon_c.svg" title="IceChips" align="right" width="3.453%">
<br />

# ice-chips-verilog

[![Build Status][ico-travisci]][link-travisci]

The 74LS, 74HC, 74HCT family of chips in Verilog for Electronic Design Automation

    Fully validated by test bench · Parametrized code · DELAY parameters for timing simulation

IceChips is built to support the [Icestudio][link-icestudio] and [FPGAwars][link-fpgawars] manifesto:

    <Open Hardware driven by Open Source>

## Getting Started

The easiest way to use these devices is [download the collection](/releases/latest) and open it in the Icestudio design environment.

In Icestudio, go to `Tools > Collections > Add` and select the downloaded .zip file. Place and wire up your components, run and test the result. There's a variety of ways to provide inputs and view outputs; but no need for actual parts, wires or power supply.

Alternatively, you can download an individual device (.v file) and use it in your own simulation in Verilog. This is the way to go if you wish to set the parameters for #bits, #inputs per gate, #blocks in a device. See the Index to browse devices.

## Index

&ensp;&ensp;[Devices by type and name](device-index.md)

#### What are the 7400-series TTL chips?

&ensp;&ensp;They are digital logic: Gates, multiplexers, counters, registers, adders, multipliers and more

&ensp;&ensp;[7400-series integrated circuits (Wikipedia)][link-wiki-7400]

## Icestudio Design Flow

Welcome to virtual breadboarding.

Icestudio provides circuit simulation (for digital circuits) that's arbitrarily scalable. Explore, build and create, but most importantly, get near-instant feedback in testing your real hardware design. Each time you add a new input or a gate, hit "Build" and "Upload". In the parlance of a silicon fab, you've gone through a "spin". But you're actually programming a reusable and fairly inexpensive FPGA.

    CAD-style layout using drag and drop
        -> Full Verilog model
            -> Validation of design rules & connectivity
                -> Synthesis of circuit
                    -> Bitstream to FPGA
                        -> Live circuit to test or put in-situ

It's done with entirely open source tools (the IceStorm toolchain); and most of the magic is due to the representation in Hardware Description Language, i.e. Verilog, because HDL is translatable to H:

- Once you have a system fully modelled in HDL, you have everything. The HDL is used to generate hardware in any way you require, in a process called [logic synthesis][link-wiki-synth]

- The toolchain can synthesize the circuit onto an expanding selection of FPGAs; see [Icestudio][link-icestudio] for details

- What's cool about the Icestudio graphical editing, with internal Verilog, is the hierarchy, encapsulation and layering that it makes easy and explicit; this promotes compositional design; it means scalability and testability

## Tests and Validation

A test bench accompanies every device (74xx-tb.v file with 74xx.v file) and the tests are run automatically. Click on the “tests|passed” icon near the top of the page to see the log of the validation run.

Tests are a definitive feature of this library. They must be:

1. Comprehensive
2. Meaningful (each test adding value)
3. Annotated with descriptions
4. Pass/Fail when run

The tests are for documentation and transparency and create a kind of audit trail - that's in addition to their role in correctness!

The tests are actively Pass/Fail, because they "assert" and they log a failure message if the stated condition is not met. They are not just doing a demonstration run of the device, with a waveform output. See more details in the Validation Contract and in the project code.

Coverage will continue at the highest standard as the library expands going forward.

You have to "trust but verify" when scaling up a hardware design from lower-layer components.

#### Validation Contract

The stamp of approval comes from the test bench code, but more is involved: Scripts and templates generate the code files of IceChips, and also ensure they are validated reliably and completely.

&ensp;&ensp;[Validation scheme](docs/validation-scheme.md) · How the the code files and .ice components are validated

#### Running the tests on your machine

<details>
<summary>Details</summary>
<br />

The test benches can be run using the open source simulator Icarus Verilog: [Installation][link-iverilogi], [Getting Started][link-iverilogs].

With it installed, you can run a command like the following that specifies the required input files and one output file (.vvp):
```
> iverilog -g2012 -o 7400-tb.vvp ../includes/helper.v ../includes/tbhelper.v 7400-tb.v 7400.v
```

It then requires a second step: Run the Icarus Verilog simulator/runtime to see the tests run, with results logged to the console:
```
> vvp 7400-tb.vvp
```

If you're interested in looking even closer, the above "vvp" run stores all signal and timing data - inputs, outputs, and the connection paths between them - in a .vcd file, so run GTKWave viewer to see the run as a waveform: [Installation][link-gtkwavei], [Getting Started][link-gtkwaves].

With GTKWave installed, just click on the .vcd file to open.

<img src="images/GTK.png" title="Simulation waveform" width="50%" height="50%">

</details>

## Technical Notes

&ensp;&ensp;[Implementation info, quirks, challenges in the technology, usage notes, and some bibliographic and specialty interest links](docs/technical-notes.md)

## Other Resources for your Digital Project

To brush up on digital logic design, or get started with an EDA flow to create, test out and tape-out your project:

<details>
<summary>Topics to get started</summary>
<br />

- [Combinational Circuit versus Sequential Circuit][link-web-comb-seq]
- [RTL Description][link-web-rtl] · Register Transfer Level Description
- [HDLs][link-web-hdls] · Hardware Description Languages
- [Logic Simulation][link-web-logic-sim]
- [Logic Synthesis][link-web-logic-synth]
- [Logic Friday (Program)][link-web-logic-friday]
- [Espresso Logic Minimizer (Program)][link-web-esp-logic-min]
- [EDA][link-web-eda] · Electronic Design Automation
- [FPGAs][link-web-fpgas] · Field-Programmable Gate Arrays

</details>
<br />

Clarification about this design flow versus PCB (Printed Circuit Board) flow:

<details>
<summary>PCB design flow</summary>
<br />

Simulating and testing your design can put you in a position to populate your components onto a custom PCB (Printed Circuit Board) to be manufactured.

You have a head start because you have a digital circuit that you know meets all its specs.

However, it's a different workflow area that you'll have to get into for a PCB: A different type of visual editing ("schematic capture"); placing, routing and design of layout for manufacture; verification of design rules - this time for geometric/electrical properties - for manufacture.

Note: Having said that, using 74xx standard parts will set you up well for using PCB software, since the parts are well-known and modelled for geometric/electrical properties.

The following keywords are related to PCBs and are **not** part of the present workflow:

- Ngspice
- SPICE
- Eagle
- Gerber format
- Most software programs that have CAD in them (KiCAD) and the ones that have PCB in them (LibrePCB)
- gEDA suite (for the most part)

</details>

## This project gains inspiration from

[www.homebrewcpuring.org][link-homebrew] · Amazing Homebrew CPUs

[Hackaday Homebrew CPU projects][link-hackbrew] · More Homebrew CPUs

[FPGAwars list of projects][link-fpgawarsp] developed with Open Source FPGAs, including CPUs

## Acknowledgments

Juan González-Gómez [@Obijuan], Jesús Arroyo Torrens, Salvador E. Tropea, Democrito · for Icestudio collections

Warren Toomey [@DoctorWkt] · for inspiration because he builds real CPUs, and for using early versions of these devices

Eddie Hung [@FPGeh] · for Yosys advice and feedback

[digitaljs.tilk.eu](http://digitaljs.tilk.eu) Marek Materzok [@tilk] · for helpful feedback and has an amazing convenient simulator "DigitalJS Online"

[www.edaboard.com](https://www.edaboard.com/threads/two-dimensional-input-output-ports-in-verilog.208692) "mrflibble" · provided solution for 2-dimensional inputs to a module

["Inside the vintage 74181 ALU chip"](http://www.righto.com/2017/03/inside-vintage-74181-alu-chip-how-it.html) Ken Shirriff · invaluable info on the 74181 and a fabulous simulator in the browser

Marcus Lindholm · SVG graphic design help

[www.msarnoff.org/chipdb](http://www.msarnoff.org/chipdb/list) Matt Sarnoff · chip and pin info

["TTL_74xx_DIL.m4"](https://fossies.org/linux/pcb/lib/TTL_74xx_DIL.m4) Thomas Nau, "diplib" in PCB for Linux distribution · chip and pin info

[www.referencedesigner.com/tutorials](http://www.referencedesigner.com/tutorials/verilog/verilog_01.php) · practical intro to Verilog with examples, tutorials, quizzes

[www.doulos.com/knowhow](https://www.doulos.com/knowhow/verilog_designers_guide/sequential_always_blocks) · practical intro to design and concepts in Verilog

[www.verilogpro.com](https://www.verilogpro.com/verilog-generate-configurable-rtl) · practical intro to generate loops and elaboration

#### And to these supporting pieces of technology:

[Icestudio][link-icestudio] and Apio built on top of IceStorm, Yosys, Arachne-pnr

[Yosys][link-yosys] synthesis by Clifford Wolf

[Icarus Verilog][link-iverilog] simulator by Stephen Williams

[GTKWave][link-gtkwavei] for viewing waveforms

## <!-- -->

© 2018-2020 Tim Rudy

[ico-travisci]: images/passed.svg

[link-travisci]: https://travis-ci.com/TimRudy/ice-chips-verilog "See the latest build and test report"
[link-icestudio]: https://icestudio.io
[link-icestudiob]: https://github.com/FPGAwars/icestudio-blocks/wiki
[link-openfpgat]: https://github.com/Obijuan/open-fpga-verilog-tutorial/wiki
[link-fpgawars]: https://fpgawars.github.io
[link-fpgawarsp]: https://fpgawars.github.io/#projects
[link-wiki-7400]: https://en.wikipedia.org/wiki/List_of_7400_series_integrated_circuits
[link-wiki-synth]: https://en.wikipedia.org/wiki/Logic_synthesis
[link-web-comb-seq]: https://www.google.com/search?q=Combinational+versus+Sequential+Circuit
[link-web-rtl]: https://www.google.com/search?q=RTL+Description
[link-web-logic-sim]: https://www.google.com/search?q=Logic+Simulation+in+HDL
[link-web-logic-synth]: https://www.google.com/search?q=Logic+Synthesis
[link-web-logic-friday]: https://www.google.com/search?q=Logic+Friday
[link-web-esp-logic-min]: https://www.google.com/search?q=Espresso+Logic+Minimizer
[link-web-hdls]: https://www.google.com/search?q=Hardware+Description+Languages
[link-web-eda]: https://www.google.com/search?q=Electronic+Design+Automation
[link-web-fpgas]: https://www.google.com/search?q=Field-Programmable+Gate+Arrays
[link-coinmining]: http://whattomine.com
[link-homebrew]: https://www.homebrewcpuring.org/ringhome.html
[link-hackbrew]: https://hackaday.io/list/25846-homebrew-cpu
[link-yosys]: http://www.clifford.at/yosys
[link-iverilog]: http://iverilog.icarus.com
[link-iverilogi]: https://iverilog.fandom.com/wiki/Installation_Guide
[link-iverilogs]: https://iverilog.fandom.com/wiki/Getting_Started
[link-iverilogu]: https://iverilog.fandom.com/wiki/User_Guide
[link-gtkwavei]: http://gtkwave.sourceforge.net
[link-gtkwaves]: https://iverilog.fandom.com/wiki/GTKWAVE
