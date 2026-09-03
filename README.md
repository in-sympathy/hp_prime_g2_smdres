# SMD Resistor Code Decoder — HP Prime G2

`SMDRES.hpprgm` is a small PPL program that converts SMD resistor markings
into an Ohm value. It's plain text, so you can open it to read or tweak the
source, and it runs the same way any of your other programs do (like
Meshtastic) — no separate "app install" step needed.

## What it decodes

- **3-digit codes** — two significant figures + multiplier: `103` → 10 kΩ
- **4- and 5-digit codes** — three/four significant figures + multiplier: `4702` → 47 kΩ
- **R / K / M notation** (letter stands in for the decimal point): `4R7` → 4.7 Ω, `R47` → 0.47 Ω, `4K7` → 4.7 kΩ, `1M0` → 1 MΩ, `10R0` → 10.0 Ω
- **EIA-96 codes** (2-digit index + multiplier letter, used on 1%/precision parts): `01A` → 1.00 Ω, `68C` → 499 Ω. A 4th trailing tolerance letter (e.g. `01AF`) is accepted and ignored.
- **Zero-ohm links**: `0`, `000`, `0000` → 0 Ω

Multiplier letters for EIA-96: Z=×0.001, Y=×0.01, X/S=×0.1, A=×1, B/H=×10, C=×100, D=×1000, E=×10000, F=×100000.

## Installing on the calculator

The Prime G2 has no SD card slot (that's a feature it dropped compared to
older HP calculators like the 50g) — file transfer is either over USB or by
typing the program in directly:

1. **HP Connectivity Kit + USB cable (easiest)** — Connect the Prime G2, open the Connectivity Kit on your computer, and drag `SMDRES.hpprgm` onto the calculator in the file browser (it'll sit under Programs, next to Meshtastic).
2. **Type it in by hand** — Open the Program Catalog (`Shift` + `1`), create a new program named `SMDRES`, and type in the contents of the file. It's plain ASCII, no special characters needed.

## Running it

Same as Meshtastic: open it from the Program Catalog (`Shift` + `1` → select `SMDRES` → `Run`), or from Toolbox → User → Program Functions.

The screen is a custom-drawn entry form, not the calculator's usual pop-up dialog, so the controls are:

- **0–9** — type digits directly into the code line.
- **ALPHA** — opens a small picker listing the letters resistor codes actually use (`R`, `K`, `M`, and the EIA-96 multiplier letters `A B C D E F H S X Y Z`). Pick one to insert it — no need to fumble with the calculator's alpha-shifted keyboard.
- **Backspace** — deletes the last character.
- **ENTER** — decodes whatever's typed and shows the result.
- **ESC** — exits the program. This is the *only* way out — after every conversion (success or error) it brings you straight back to a fresh `Code:` prompt so you can keep converting values one after another.

Two example lines are drawn as plain static text right under the title, and a one-line key legend sits at the bottom of the screen.

## Notes

- The decoding logic was verified against a set of known reference codes (`103`→10 kΩ, `4702`→47 kΩ, `01A`→1.00 Ω, `68C`→499 Ω, and the R/K/M forms) before being written into PPL.
- Because the code line is built up one keystroke at a time rather than typed into the calculator's own CAS-aware input box, there's no need to wrap letter codes in quotes — `4R7` just works as typed.
- If you'd ever like a fancier splash graphic, different colors, or additional multiplier letters, the drawing calls are all in the `SMDRES()` function near the bottom of the file and are easy to adjust.
