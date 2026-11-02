# Map Algebra Calculator (geoskill-map-algebra-calculator)

> Evaluate band math expressions like NDVI on rasters with a safe expression parser

---

## 1. Overview

Performs map algebra on multi-band rasters using a **safe expression evaluator** based on Python `ast`, supporting band references b1..bN, the four basic arithmetic operations, powers, and common math functions, with built-in preset indices such as NDVI / NDWI / SAVI / EVI. Expressions pass a whitelist check that rejects attribute access, imports, and non-whitelisted calls; division by zero is automatically set to 0, so results contain no inf / nan.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-map-algebra-calculator.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `result.tif` | GeoTIFF | Result raster of the operation (primary/verifiable output) |
| `expression_meta.json` | JSON | Expression and result statistics |

Each run also produces `output-manifest.json` (run manifest).


## 6. Technical Principle

ast.parse(mode='eval') → whitelist recursive evaluation (numbers / bands / pi, e / whitelisted functions / + - * / % **) → division by zero set to 0 → float32 raster.

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
