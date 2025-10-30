## 1. Introduction

This dataset is designed for training generative models for the purpose of physics-constrained antenna design. Each data sample consists of an antenna image (`.png`) and a corresponding metadata file (`.json`) that details its physical properties, performance metrics, and descriptive captions.

## 2. Directory Structure

The dataset is organized as follows:

```
antenna_dataset/
├── README.md             <-- This documentation file
├── images/
│   ├── sample_001.png
│   └── ...
└── metadata/
    ├── sample_001.json
    └── ...
```
Each image in the `images/` directory has a corresponding JSON file with the same base filename in the `metadata/` directory.

## 3. Metadata JSON File Structure

Each `.json` file contains a single object with the following top-level keys:

---

### `id`
- **Type:** `String`
- **Description:** A unique identifier for the data sample. It matches the base filename of the corresponding image and metadata files.
- **Example:** `"patch_antenna_001"`

---

### `topology`
- **Type:** `String`
- **Description:** The fundamental engineering classification of the antenna.
- **Possible Values:** `"Microstrip Patch"`, `"Monopole"`, `"Vivaldi"`, `"Horn"`, `"Yagi-Uda"`, etc.

---

### `style`
- **Type:** `List of Strings`
- **Description:** A list describing the visual or conceptual style, crucial for creative generation.
- **Example:** `["standard"]`, `["fractal", "bio-inspired:leaf"]`

---

### `performance`
- **Type:** `Object`
- **Description:** Contains precise, quantitative performance metrics obtained from electromagnetic simulations. These are the ground truth values for calculating physics-based loss.

  - #### `center_frequency_ghz`
    - **Type:** `Number (Float)`
    - **Description:** The primary resonant frequency in Gigahertz (GHz).

  - #### `fbw_percent`
    - **Type:** `Number (Float)`
    - **Description:** Fractional Bandwidth in percent (%), calculated as `(Bandwidth / Center Frequency) * 100`.

  - #### `gain_dbi`
    - **Type:** `Number (Float)`
    - **Description:** The antenna gain in dBi (decibels relative to an isotropic radiator).

---

### `classes`
- **Type:** `Object`
- **Description:** Contains qualitative, categorical labels derived from the quantitative `performance` data. Useful for simplified text prompts and classification tasks.

  - #### `bands`
    - **Type:** `List of Strings`
    - **Description:** A list of the frequency bands of operation. Designed as a list to support multi-band antennas. UHF：0.3–1 GHz, L：1–2 GHz, S：2–4 GHz, C：4–8 GHz, X：8–12 GHz, Ku：12–18 GHz, K：18–26.5 GHz, Ka：26.5–40 GHz, V：40–75 GHz, W：75–110 GHz.
    - **Possible Values:** `"L"`, `"S"`, `"C"`, `"X"`, `"Ku"`, `"Ka"`, `"mmW"`

  - #### `fbw_class`
    - **Type:** `String`
    - **Description:** The categorical classification of the Fractional Bandwidth. UltraNarrow (<2%), Narrow (2–5%), Medium (5–10%), Wide (10–20%), UltraWide (>20%)
    - **Possible Values:** `"UltraNarrow"`, `"Narrow"`, `"Medium"`, `"Wide"`, `"UltraWide"`

  - #### `pattern`
    - **Type:** `String`
    - **Description:** The primary direction of radiation.
    - **Possible Values:** `"Broadside"`, `"Endfire"`, `"Omnidirectional"`, `"MultiBeam"`

  - #### `pol`
    - **Type:** `String`
    - **Description:** The polarization of the radiated wave.
    - **Possible Values:** `"Linear"`, `"Circular"`, `"Dual"`, `"Elliptical"`

  - #### `gain_class`
    - **Type:** `String`
    - **Description:** The categorical classification of the antenna's gain. Low (<2 dBi), Mid (2–8 dBi), High (8–15 dBi), Very-High (>15 dBi).
    - **Possible Values:** `"Low"`, `"Mid"`, `"High"`

---

### `physical`
- **Type:** `Object`
- **Description:** Describes key physical properties and environmental constraints.

  - #### `diameter_mm`
    - **Type:** `Number (Float)`
    - **Description:** The largest bounding box dimensions of the antenna in millimeters (mm).

  - #### `Height_mm`
    - **Type:** `Number (Float)`
    - **Description:** The bounding box height dimensions of the antenna in millimeters (mm).

---

### `training_captions`
- **Type:** `List of Strings`
- **Description:** Pre-generated, natural language sentences describing the antenna. These are fed to the text encoder of the generative model during training. Multiple variations enhance model robustness.
- **Example:** `["A photo of a Microstrip Patch antenna...", "High-performance antenna design..."]`
