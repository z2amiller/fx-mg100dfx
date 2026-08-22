# fx-mg100dfx

## MG100DFX Distortion (OD1/OD2)

A pedal port of the overdrive channel from the Marshall MG100DFX solid-state
amp, built for a [PedalPCB forum request][post]. The +/-15V bipolar original is
re-biased for single-supply operation.

### The circuit

Input stage (x11 non-inverting) into a high-gain summing stage that clips into
an antiparallel red/green LED pair across its feedback — even quiet playing
comes out almost as a square wave. The OD1/OD2 switch adds two extra input
branches (more gain, fuller voicing). Marshall-style treble/bass/middle stack,
contour, volume, then a x11 recovery stage.

### Power and headroom

- 9V: fully functional but not completely true to the original tone. The input stage rail-clips hot transients (above roughly 350mV peaks) before the LED clipper.
- 18V: reproduces the original amp's front-end dynamics essentially exactly (sim-verified: identical stage-1 swing to the +/-15V original). Electrolytics are 25V-rated for this.

### No-cap-mult (purist) build

Aggressive power rail filtering is done through a capacitor multiplier at the voltage input. This drops ~1V total between the reverse polarity protection diode and the capacitor multiplier.

If you have a clean supply and want to recover some of the headroom, you can
omit Q1 jumper Q1 pads 2-3 (B and E on the BC547 footprint), and fit 47R at
R23 (Just above the 4-pin connector at the south of the board) instead of 10k.
you get a plain RC filter (47R into ~200uF) — about 34dB less ripple filtering,
about 0.5V less drop. At 18V the saved drop is meaningless — this option is
parts-count preference, not tone.

### Parts notes

- D2/D3 clipping LEDs: use old-school GaP green (Vf ~2.0-2.2V). A modern InGaN green (2.6-2.9V) hits the op-amp rail before the LED clamps at 9V and kills the intended red/green asymmetric clipping.
- Q1 is BC547C (C-B-E). If substituting 2N5088, its pinout is E-B-C — check before soldering.
- Film caps in the signal path, ceramic disc for pF values, per the BOM.
- Hybrid I/O: populate EITHER the JST-PH headers (daughterboard style) OR the PedalPCB-style wire pads (IN at the bottom edge, VIN/GND at top). The daughterboard layout that supports this is at the [pedalfx repo][repo].

[post]: https://forum.pedalpcb.com/threads/help-needed-to-design-od1-od2-pedal-from-mg100dfx-amp.27087/
[repo]: https://github.com/z2amiller/pedalfx/tree/main/template
