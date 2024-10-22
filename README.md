![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/test/badge.svg) ![](../../workflows/fpga/badge.svg)

![](clock.png)

# Analog Clock using a beam-racing triangle render

The VGA timing is based directly on VEGA 640x480 @ 75 Hz.

Using a tile-based beam-racing triangle render has always seemed like
a good way to deal with the lack of a framebuffer. Tiny Tapeout gave
me an opportunity to play with it.  However as this effort is pretty
much defined by a mad-scramble to get SOMETHING done for Nov 4th
everything is a consequence of that, so the design is very simple and
not very ambitious.

Every frame the 640x480 VGA matrix is scanned, advancing the state of
the intersecting lines of the three triangles.  If the (x,y)
coordinate of the "beam" lines on the positive side of each line, the
beam is inside the triangle.  Among the visible triangles, the highest
priority triangle sets the color, else we default to a grey color.
Twelve dots are also marked, to make it easier to read the clock.

The algorithm might be easily understood by examining the software
model in Rust, in the `sw` directory.

The main "UI" is two buttons to advance hour and minutes respectively.
The least significant two bits selects which outputs are routed to the
bidirectional port (frame number, seconds * 4 + hz-strobe * 2 +
vs-strobe, minute * 4, hour * 4).

## What is Tiny Tapeout?

Tiny Tapeout is an educational project that aims to make it easier and cheaper than ever to get your digital and analog designs manufactured on a real chip.

To learn more and get started, visit https://tinytapeout.com.

## Set up your Verilog project

1. Add your Verilog files to the `src` folder.
2. Edit the [info.yaml](info.yaml) and update information about your project, paying special attention to the `source_files` and `top_module` properties. If you are upgrading an existing Tiny Tapeout project, check out our [online info.yaml migration tool](https://tinytapeout.github.io/tt-yaml-upgrade-tool/).
3. Edit [docs/info.md](docs/info.md) and add a description of your project.
4. Adapt the testbench to your design. See [test/README.md](test/README.md) for more information.

The GitHub action will automatically build the ASIC files using [OpenLane](https://www.zerotoasiccourse.com/terminology/openlane/).

## Enable GitHub actions to build the results page

- [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## Resources

- [FAQ](https://tinytapeout.com/faq/)
- [Digital design lessons](https://tinytapeout.com/digital_design/)
- [Learn how semiconductors work](https://tinytapeout.com/siliwiz/)
- [Join the community](https://tinytapeout.com/discord)
- [Build your design locally](https://www.tinytapeout.com/guides/local-hardening/)

## What next?

- [Submit your design to the next shuttle](https://app.tinytapeout.com/).
- Edit [this README](README.md) and explain your design, how it works, and how to test it.
- Share your project on your social network of choice:
  - LinkedIn [#tinytapeout](https://www.linkedin.com/search/results/content/?keywords=%23tinytapeout) [@TinyTapeout](https://www.linkedin.com/company/100708654/)
  - Mastodon [#tinytapeout](https://chaos.social/tags/tinytapeout) [@matthewvenn](https://chaos.social/@matthewvenn)
  - X (formerly Twitter) [#tinytapeout](https://twitter.com/hashtag/tinytapeout) [@tinytapeout](https://twitter.com/tinytapeout)
