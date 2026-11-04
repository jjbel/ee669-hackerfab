# Litho systems: spec comparison

| Model name | Resolution (nm) | Throughput (wafers/hr) | Cost (USD) |
|---|---|---|---|
| HackerFab litho (projection direct-write) | 3000 | ~0.003 (100 mm wafer, calc.) | ~$2k |
| ASML TWINSCAN EXE:5200B (High-NA EUV) | 8 | 175 (@ 50 mJ/cm²) | ~$380M |
| Durham Magneto Optics MicroWriter ML3 Pro | 600 (400 option) | ~0.1–0.4 (100 mm wafer, est.) | ~$10⁵ (est. $0.2–0.5M) |
| Raith VOYAGER (50 kV EBL) | ≤8 | ≲0.02 (full 100 mm wafer, est.) | ~$10⁶ (est. $1–5M) |
| IMS Nanofabrication MBMW-101 / -301 (multi-beam mask writer) | 14 (MBMW-101); <14 for -301 | ~0.1 *masks*/hr (<10 h per mask) | ~$10⁷ ($30–80M) |

"est." = my own estimate. I couldn't find a published number, so this is an order of magnitude or a bound. Derivations are below.

## Notes and sources

### 0. HackerFab litho
- The resolution (3 µm) and cost (<$2k) are the user's figures; see [content_my.md](content_my.md) and [media_my/04_lab_photos/litho 3um resolution.jpg](<media_my/04_lab_photos/litho 3um resolution.jpg>).
- Slide 3 uses the user's [media_my/microwriter.png](media_my/microwriter.png) for the MicroWriter and a crop of the Raith render, [media_claude/raith_voyager_crop.jpg](media_claude/raith_voyager_crop.jpg).
- Throughput (calc.): one exposure covers a 1 mm wide patch at 16:9, so 1 × 0.5625 mm = 0.5625 mm², and takes 90 s. That works out to ≈0.375 mm²/min.
  - A 100 mm wafer is 7,854 mm², or ~13,960 patches. At 90 s each that is ~349 h, about 14.5 days, so ≈0.003 wph.
  - This ignores stage stepping and alignment overhead, so it is an upper bound.
  - For comparison, the MicroWriter at 1 µm writes 50 mm²/min, ~130× faster.

### 1. ASML TWINSCAN EXE:5200B
- 0.55 NA High-NA EUV. Intel completed acceptance testing in Dec 2025, so this is the newest EUV tool in production. ASML lists 8 nm resolution and 175 wph at a 50 mJ/cm² dose. [ASML product page](https://www.asml.com/en/products/euv-lithography-systems/twinscan-exe-5200b)
- ~$380M is a third-party estimate; ASML publishes no list price. [Tom's Hardware](https://tomshardware.com/tech-industry/semiconductors/asml-lithograpy-roadmap-examined-from-duv-to-hyper-na), [TrendForce (Intel acceptance)](https://www.trendforce.com/news/?p=50149)
- For context, ASML's low-NA workhorse is the NXE:3800E: 13 nm resolution, ~220 wph, ~$200M.
- Image: [media_claude/asml_exe5200b.png](media_claude/asml_exe5200b.png)

### 2. Durham Magneto Optics MicroWriter ML3 Pro
- Maskless, LED/laser direct write at 385 nm (405/365 nm optional). Spot sizes are 0.6, 1, 2 and 5 µm, with 0.4 µm as an option. Write speed is 50 mm²/min at 1 µm and 15–17 mm²/min at 0.6 µm. Maximum write area is 195 × 195 mm. [NUS E6 Nanofab](https://cde.nus.edu.sg/e6nanofab/microwriter-durham-magneto-optics-ml3-pro-class-10), [QD Europe datasheet (PDF)](https://qd-europe.com/fileadmin/Mediapool/products/photo-lithography/_pdf/MicroWriter_ML_3_Pro.pdf)
- Throughput (est.): a 100 mm wafer is 7,854 mm². At 1 µm that takes ~157 min (≈0.4 wph). At 0.6 µm it takes ~8 h (≈0.1 wph).
- Cost: no public price. The vendor only says it is "realistically priced for university R&D budgets". The order of magnitude is my estimate.
- Image: [media_claude/dmo_ml3_pro_ntu_install.jpg](media_claude/dmo_ml3_pro_ntu_install.jpg) (ML3 Pro installed at NTU, from the [DMO site](https://www.durhammagnetooptics.com/?product=microwriter))

### 3. Raith VOYAGER
- 50 kV EBL. Guaranteed linewidth is ≤8 nm. Beam current goes up to 40 nA. Stitching and overlay are ≤20 nm. The stage handles 150 mm, and the tool takes samples up to 8 in. [Raith product page](https://raith.com/products/voyager/), [PoliFab](https://www.polifab.polimi.it/equipment/ebl-system-raith-voyager/), [Colorado School of Mines](https://www.mines.edu/shared-facilities/project/ebl/)
- Throughput (est.): for 100% coverage of a 100 mm wafer (78.5 cm²) at a dose of 100 µC/cm² and 40 nA, the charge is 7.85 mC, which takes ~55 h (≈0.02 wph). Real throughput scales with fill factor, and at high-resolution currents (~1 nA) it is ~40× slower.
- Cost: no public price. Raith only says "attractive price/performance ratio". Research EBL tools typically cost $1–5M.
- Images: [media_claude/raith_voyager.jpg](media_claude/raith_voyager.jpg), [media_claude/raith_voyager_sub7nm_lines_hsq.jpg](media_claude/raith_voyager_sub7nm_lines_hsq.jpg) (sub-7 nm lines in HSQ)

### 4. IMS Nanofabrication multi-beam mask writer (MBMW)
- IMS is the Vienna company named in [media_my/asianometry_multi_ebeam.txt](media_my/asianometry_multi_ebeam.txt). TSMC uses its writers for masks. The tool splits one beam into many beamlets that are blanked individually.
- MBMW-101 official specs: 50 keV, 512 × 512 = 262,144 programmable beams, 82 × 82 µm beam field, 14 nm resolution / 0.1 nm positional accuracy, up to 1 µA total current, mask write time under 10 h. Write time does not depend on pattern complexity, which suits curvilinear ILT. [IMS products page](https://www.ims.co.at/en/products/)
- MBMW-301 is the newest model (2023). It targets 2 nm-node and High-NA EUV masks. IMS has not published a full spec sheet. [SPIE PC12751](https://opticalengineering.spiedigitallibrary.org/conference-proceedings-of-spie/PC12751/PC127510R/MBMW-301--paving-the-way-towards-the-angstrom-era/10.1117/12.2688204.full)
- Throughput: it writes **masks, not wafers**, at ~10–12 h per 6" mask (≈0.1 masks/hr). [Semiconductor Engineering](https://semiengineering.com/multi-beam-mask-writing-finally-comes-of-age)
- Cost: a market report puts multibeam mask writers at $30–80M per unit. [Dataintelo](https://dataintelo.com/report/global-multi-beam-mask-writer-market)
- Image: [media_claude/ims_mbmw101.jpg](media_claude/ims_mbmw101.jpg)

## Optics (HackerFab litho)

- **Objective:** Edmund Optics 10X DIN Plan Commercial Grade. NA 0.25, EFL 15.37 mm, WD 1.5 mm. [Edmund Optics](https://www.edmundoptics.in/p/10x-din-plan-commercial-grade-objective/5386)
- **DMD (TI DLPDLCR471TPEVM, uses the DLP471TP):** 5.4 µm mirror pitch, 1920 × 1080 mirrors, ±17° tilt, 0.47" diagonal (10.37 × 5.83 mm). [TI DLP471TP datasheet](https://www.ti.com/lit/gpn/DLP471TP). Image: [media_my/ti_dlp.png](media_my/ti_dlp.png)
  - At ≈10x demagnification the DMD maps to ≈0.54 µm per pixel and a ≈1.04 × 0.58 mm field on the wafer. That matches the 1 mm 16:9 patch used for the throughput number.
- **Diffraction limit at λ = 405 nm:**
  - Airy disk diameter: 1.22 λ/NA = 1.98 µm
  - Rayleigh resolution: 0.61 λ/NA = 0.99 µm
  - The measured 3 µm CD gives k1 = CD·NA/λ ≈ 1.85, so the optics are not the limiting factor.
- **Is 1.22 λ/NA the right formula?**
  - 1.22 λ/NA is the Airy disk *diameter*. The Rayleigh two-point resolution is the radius, 0.61 λ/NA. Lithography writes it as CD = k1 λ/NA.
  - The 1.22 comes from 3.832/π, the first zero of the Bessel function J1, for a uniformly lit circular pupil.
  - It changes with the pupil shape (a slit gives 1.0), the criterion used (Rayleigh 0.61, Abbe 0.5, Sparrow 0.47), and the illumination coherence. Coherent illumination resolves a half-pitch of 0.5 λ/NA; off-axis illumination reaches 0.25 λ/NA.
- **Slide 3 table:** ranges are replaced by their upper limits, as the user asked.
