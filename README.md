# Blackbody Radiation, Interactively

An interactive, single-page web demo of photon statistics: the electromagnetic field in a hot box treated as a gas of photons, leading to the Planck spectrum, Stefan's law, the cosmic background radiation, and the temperature of the Earth.

Created by **Claude Opus 5.5**, based on the lecture notes by **Sang Hoon Lee** (Chapter 7, Quantum Statistics; Section 7.4, Blackbody Radiation). It is a companion to the demos for Section 7.1 (the grand canonical ensemble), Section 7.2 (bosons and fermions), and Section 7.3 (degenerate Fermi gases).

## What's inside

**The ultraviolet catastrophe.** Equipartition gives every electromagnetic mode an energy k<sub>B</sub>T, and with infinitely many short-wavelength modes the total diverges. Planck's quantized oscillator gives instead

```
Ē = hf / (e^(hf/k_B T) − 1),     n̄_Pl = 1 / (e^(hf/k_B T) − 1)
```

Two charts compare the classical and Planck average energy per mode and the Rayleigh–Jeans and Planck spectra, with a slider for the mode energy hf/k<sub>B</sub>T showing how high-frequency modes are "frozen out."

**Photons as bosons.** Why μ = 0 for photons, how the two polarizations and the eighth-sphere of *n*-space lead to the spectrum u(ε) = (8π/(hc)³) ε³/(e<sup>ε/k<sub>B</sub>T</sup> − 1), and Wien's law.

**The spectrum at any temperature.** A log-scale spectrum, per wavelength or per energy, for any temperature from 2.73 K to 30,000 K, with presets for the cosmic background, room temperature, a kiln, a light bulb, the Sun, and a hot star. The visible band is shown in color, a swatch shows the color of the glow (computed from the spectrum with an analytic fit to the CIE 1931 color-matching functions), and curves can be pinned for comparison. The panel shows why the peak of u(λ), at 0.2014 hc/k<sub>B</sub>T, is not at hc/ε<sub>max</sub> (Problem 7.39).

**Totals.** U/V = 8π⁵(k<sub>B</sub>T)⁴/15(hc)³, the heat capacity, entropy, photon number N = 16πζ(3)V(k<sub>B</sub>T/hc)³, entropy per photon S/N ≈ 3.6 k<sub>B</sub>, radiation pressure P = U/3V, and free energy F = −U/3 (Problems 7.40, 7.44, 7.45, 7.46), with a calculator for any temperature including the Sun's core. It reproduces the lecture's photon densities:

| Temperature | Photons per m³ |
| --- | --- |
| 300 K | 5.5 × 10<sup>14</sup> |
| 1500 K (kiln) | 6.8 × 10<sup>16</sup> |
| 2.73 K (cosmic background) | 4.1 × 10<sup>8</sup> |

It also works out the "do it yourself" comparison in Problem 7.45: radiation pressure in a 1500 K kiln is about 1.3 × 10<sup>−3</sup> Pa, while at the center of the Sun it is about 1.3 × 10<sup>13</sup> Pa, roughly 2000 times less than the pressure of the ionized hydrogen gas there.

**The cosmic background radiation.** The 2.73 K spectrum filling the universe, peaking near 1 mm.

**Photons escaping through a hole.** Two illustrations accompany the derivation of the power per unit area, cU/4V = σT⁴ (Stefan's law). A geometry diagram, after the figure in the lecture notes, shows a chunk of the hemispherical shell at angle θ and the hole's apparent area A cos θ, with a slider for θ. A live simulation sends 2000 photons bouncing around a 3D box and counts those escaping through a hole in one wall: the measured rate converges to ¼(N/V)cA, and the histogram of escape angles follows sin θ cos θ. Escaped photons are replaced by photons entering through the hole with a cosine-weighted (Lambertian) direction, as if the hole opened onto radiation at the same temperature, which keeps the radiation inside uniform and isotropic. The section closes with why a blackbody must emit the same spectrum as the hole, and with emissivity.

**The Sun and the Earth.** An animated orbit diagram shows the Earth going around the Sun (with Venus's and Mars's orbits for reference), the sunlight it intercepts, and the solar constant at its distance; a close-up inset shows why the average input is a quarter of the solar constant, since the Earth absorbs over its disk, πr<sub>E</sub>², but radiates over its whole surface, 4πr<sub>E</sub>². The diagram follows the sliders below it, and the orbital period follows Kepler's third law. Below it is an energy-balance calculator with sliders for the Sun's surface temperature, the distance from the Sun, and the albedo, plus a single-layer greenhouse atmosphere. A diagram shows the flows in W/m². The presets reproduce the lecture's numbers: 279 K for a perfect blackbody Earth, 255 K with 30% of sunlight reflected, and 303 K with the greenhouse layer, against a measured average of 288 K.

## Running it

There is nothing to build or install. The whole demo is one self-contained file, `index.html`, with all CSS and JavaScript inline.

Open it locally by double-clicking `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Publishing with GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and the `/ (root)` folder, then save.
4. After a minute or so, the demo will be live at `https://<your-username>.github.io/<repository-name>/`.

## Technical notes

- Plain HTML, CSS, and vanilla JavaScript drawn on `<canvas>`. No frameworks, no build step.
- The escape simulation and the orbit animation pause when scrolled off screen and starts paused when the system asks for reduced motion.
- Glow and visible-band colors use the multi-lobe Gaussian fit to the CIE 1931 color-matching functions by Wyman, Sloan, and Shirley (2013), converted to sRGB. Temperatures below about 800 K (the Draper point) are shown as not visibly glowing.
- Equations are typeset with [MathJax 3](https://www.mathjax.org/) (SVG output, loaded from cdnjs), so they need no extra web fonts.
- The only other external resources are the Newsreader and Instrument Sans fonts from Google Fonts, with system font fallbacks if they fail to load.
- Opening the page requires an internet connection for MathJax; offline, the equations appear as raw TeX.
- Supports light and dark mode: it follows `prefers-color-scheme`, and a sun/moon button in the top-right corner switches by hand (the choice is remembered across pages); and is responsive down to phone widths.
- Constants used: h = 6.626 × 10<sup>−34</sup> J s, k<sub>B</sub> = 1.381 × 10<sup>−23</sup> J/K, c = 2.998 × 10<sup>8</sup> m/s, σ = 5.670 × 10<sup>−8</sup> W m<sup>−2</sup> K<sup>−4</sup>.

## Caveats

- The Earth model is the lecture's: a uniform blackbody (or a single, perfectly infrared-opaque atmospheric layer). It deliberately overshoots with the greenhouse layer, as the lecture notes.
- The default solar surface temperature is 5772 K with a solar radius of 6.96 × 10<sup>8</sup> m, which gives a solar constant within about 1% of the lecture's 1370 W/m². The lecture's round values (5800 K, 7.0 × 10<sup>8</sup> m) give nearly the same results.
- The "light bulb" and "hot star" presets (2800 K and 20,000 K) are representative values, not taken from the lecture.

## Credits

- Demo: Claude Opus 5.5
- Physics content and examples: lecture notes by Sang Hoon Lee
- The lecture follows Daniel V. Schroeder, *An Introduction to Thermal Physics* (Problems 7.39, 7.40, 7.44, 7.45, and 7.46).
- Color-matching fit: C. Wyman, P.-P. Sloan, and P. Shirley, "Simple Analytic Approximations to the CIE XYZ Color Matching Functions," *Journal of Computer Graphics Techniques* 2(2), 2013.

## License

No license has been chosen yet. Add a `LICENSE` file (for example, MIT or CC BY 4.0) before sharing or reusing this project publicly, and confirm that any use of the lecture material is permitted by its author.
