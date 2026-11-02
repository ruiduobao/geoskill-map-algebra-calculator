---
name: geoskill-map-algebra-calculator
description: 'Evaluate band math expressions like NDVI on rasters with a safe expression parser'
---

# 地图代数计算器 | Map Algebra Calculator

Perform map algebra on multiband rasters using a **safe expression evaluator** based on Python ast, supporting band references b1..bN, arithmetic, powers and common math functions, with built-in presets for NDVI/NDWI/SAVI/EVI and other indices.

Expressions are validated against a whitelist: attribute access, imports and non-whitelisted calls are rejected; division by zero is automatically set to 0, so the results contain no inf/nan.

## Core Algorithm / 核心算法

ast.parse(mode='eval') → whitelisted recursive evaluation (numbers/bands/pi,e/whitelisted functions/+-*/% **) → division-by-zero set to 0 → float32 raster.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## Usage / 使用方法

### Example 1 (synthetic data, offline)

```bash
python geoskill-map-algebra-calculator.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (custom expression)

```bash
python geoskill-map-algebra-calculator.py --input scene.tif --expr "(b4-b3)/(b4+b3)"
```

### Example 3 (NDWI preset)

```bash
python geoskill-map-algebra-calculator.py --input scene.tif --preset ndwi --green 2 --nir 4
```

### Example 4 (ratio + scaling)

```bash
python geoskill-map-algebra-calculator.py --input scene.tif --expr "b2/b1 * 100"
```

### Example 5 (synthetic NDVI)

```bash
python geoskill-map-algebra-calculator.py --bbox 116 39 117 40 --synthetic --preset ndvi
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `result.tif` | GeoTIFF | Result raster of the operation (main/verifiable deliverable) |
| `expression_meta.json` | JSON | Expression and result statistics |

Each run also produces `output-manifest.json` (run manifest).

## Data Source / 数据源 / Source

Local GeoTIFF / vector files; `--synthetic` mode generates physically consistent simulated data, fully offline.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is performed locally; no user data is uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
