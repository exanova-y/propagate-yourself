# propagate-yourself

Acoustics scratchpad, split out of [feynmans-prism](https://github.com/TuringsBazaar/feynmans-prism)
(history preserved). Two things live here:

1. a CT viewer to sanity-check a downloaded scan, and
2. a [jwave](https://github.com/ucl-bug/jwave) focused-ultrasound run mirrored from
   OpenwaterHealth `openlifu-python`'s k-Wave flow.

## run

Install [uv](https://docs.astral.sh/uv/), then all commands from the repo root:

```bash
uv sync
uv run python view_ct.py                 # napari viewer over dataset/ct.mha
uv run python render_slices.py           # headless montages -> examples/*.png
uv run python simulation.py coronal      # jwave run + slider viewer (coronal|axial|sagittal)
```

`view_ct.py` keys: `z` axial, `y` coronal, `x` sagittal (key = scrubbed axis). Stop it with
`pkill -f view_ct.py`.

## data

`dataset/` is gitignored. Put the SynthRAD2025 sCT case there as `dataset/ct.mha`
(plus `mr.mha`, `mask.mha` if you have them).

Tissue bounding box for `1HNA013/ct.mha` from the synrad2025 sCT dataset:

```
x: 180 - 380
y: 20 - 320
z: 55 - 130
```

## files

| | |
| --- | --- |
| `view_ct.py` | napari viewer, one HU layer, on-canvas slice readout |
| `render_slices.py` | matplotlib montages of the tissue box, soft-tissue window |
| `sim_setup.py` | `SimSetup` dataclass replicated from openlifu `sim/sim_setup.py` |
| `simulation.py` | jwave mirror of openlifu `sim/kwave_if.py`; reads `sim_config.yaml` |
| `sim_config.yaml` | Open-LIFU 1x400 (evt1) transducer, materials, layered medium |
| `examples/` | representative output of `render_slices.py` |
