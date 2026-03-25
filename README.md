# Tang Nano 9K Pinout

A zsh script that prints the pin reference for the Tang Nano 9K FPGA board
(Sipeed GW1NR-9C) directly in your terminal, with ANSI color coding.

## Requirements

- zsh
- A terminal with 256-color support for the color-coded output (optional)

## Installation

Make the script executable and optionally place it on your PATH:

    chmod +x tangnano9k-pinout.zsh
    mv tangnano9k-pinout.zsh ~/.local/bin/tangnano9k-pinout

## Usage

    zsh tangnano9k-pinout.zsh [--j5] [--j6] [--no-color]

Run with no arguments to display the full reference, including both pin
headers and the onboard peripherals table.

## Options

    --j5          Show the J5 header only (left side, USB-C end, pins 1-24)
    --j6          Show the J6 header only (right side, HDMI end, pins 25-48)
    --no-color    Disable ANSI colors (plain text output)

The --j5 and --j6 flags are non-exclusive and can be combined. Passing both
is equivalent to passing neither: both headers are shown. When either flag is
used on its own, the onboard peripherals table is hidden and the legend is
filtered to show only the signal types present in the selected header.

## Output

### Default (no flags)

Both headers are shown side by side as they appear physically on the board,
with J5 on the left and J6 on the right. Below the headers, the onboard
peripherals table lists the dedicated pins for the clock oscillator, user
LEDs, buttons, UART bridge, and JTAG interface. A full color legend is
printed at the bottom.

### --j5 or --j6

Only the selected header table is printed. --j5 shows J5, --j6 shows J6,
and using both flags together shows both headers side by side (same layout
as the default view, but without the onboard peripherals). In all cases the
onboard peripherals table is omitted, and the legend is trimmed to only the
signal categories that appear in the selected header(s).

### --no-color

Colors are suppressed. This is also applied automatically when the TERM
variable is unset or set to "dumb", making the output safe to redirect to a
file or pipe to other tools.

## Color legend

Signal categories are color-coded as follows:

    Gold      Power rails (3.3 V, 5 V)
    Grey      Ground
    Blue      General-purpose GPIO
    Orange    SPI bus and TF-card interface (J5)
    Pink      HDMI differential pairs (J6)
    Green     27 MHz clock oscillator
    Yellow    User LEDs (LED1-LED6)
    Violet    User buttons (S1, S2)
    Cyan      UART bridge via BL702
    Lilac     RGB LCD signals
    Red       1.8 V IO bank (J6)
    Silver    JTAG interface

## Board reference

Connector J5 covers the USB-C side of the board and carries the TF-card SPI
interface, general-purpose IO, and RGB LCD signals. Connector J6 covers the
HDMI side and carries the HDMI differential pairs, the 1.8 V IO bank, and
additional SPI/RGB signals. Onboard peripherals such as the LEDs, buttons,
clock, UART, and JTAG are not routed through either header and are shown
separately in the full view.

## References
Sipeed documentation: https://wiki.sipeed.com/hardware/en/tang/Tang-Nano-9K/Nano-9K.html
