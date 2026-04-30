# Crystal Types Reference

SPDCalc includes a set of built-in crystals with validated Sellmeier equations, and also supports defining custom crystals via tabulated data.

## List of Built-in Crystals

| Crystal ID | Name |
|---|---|
| [BBO_1](#bbo-beta-barium-borate) | BBO (Beta Barium Borate) |
| [KTP](#ktp-potassium-titanyl-phosphate) | KTP (Potassium Titanyl Phosphate) |
| [BiBO_1](#bibo-bismuth-borate) | BiBO (Bismuth Borate) |
| [LiNbO3_1](#linbo3-lithium-niobate) | LiNbO₃ (Lithium Niobate) |
| [LiNb_MgO](#linbmgo-magnesium-doped-lithium-niobate) | LiNb:MgO (Magnesium-Doped Lithium Niobate) |
| [KDP_1](#kdp-potassium-dihydrogen-phosphate) | KDP (Potassium Dihydrogen Phosphate) |
| [AgGaSe2_1](#aggase2-silver-gallium-selenide) | AgGaSe₂ ref 1 (Silver Gallium Selenide) |
| [AgGaSe2_2](#aggase2-silver-gallium-selenide) | AgGaSe₂ ref 2 (Silver Gallium Selenide) |
| [LiIO3_1](#liio3-lithium-iodate) | LiIO₃ ref 1 (Lithium Iodate) |
| [LiIO3_2](#liio3-lithium-iodate) | LiIO₃ ref 2 (Lithium Iodate) |
| [AgGaS2_1](#aggas2-silver-gallium-sulfide) | AgGaS₂ (Silver Gallium Sulfide) |

---

### BBO (Beta Barium Borate)

| Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|
| Uniaxial negative | Yes | [Newlight Photonics](http://www.newlightphotonics.com/v1/bbo-properties.html) | [bbo_1.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/bbo_1.rs) |

$$
n_o(\lambda, T) = \sqrt{2.7359 + \frac{0.01878}{\lambda^2 - 0.01822} - 0.01354\,\lambda^2} - 9.3 \times 10^{-6}\,\Delta T
$$

$$
n_e(\lambda, T) = \sqrt{2.3753 + \frac{0.01224}{\lambda^2 - 0.01667} - 0.01516\,\lambda^2} - 16.6 \times 10^{-6}\,\Delta T
$$

where $ \lambda $ is in µm and $ \Delta T = T - 20\,^\circ\mathrm{C} $.

---

### KTP (Potassium Titanyl Phosphate)

| Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|
| Biaxial positive | Yes | [doi:10.1063/1.1668320](http://dx.doi.org/10.1063/1.1668320) | [ktp.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/ktp.rs) |

> Sellmeier coefficients from [Red Optronics](https://web.archive.org/web/20240225020609/http://www.redoptronics.com/KTP-crystal.html):

$$
n_x(\lambda, T) = \sqrt{2.10468 + \frac{0.89342\,\lambda^2}{\lambda^2 - 0.04438} - 0.01036\,\lambda^2} + 1.1 \times 10^{-5}\,\Delta T
$$

$$
n_z(\lambda, T) = \sqrt{1.9446 + \frac{1.3617\,\lambda^2}{\lambda^2 - 0.047} - 0.01491\,\lambda^2} + 1.6 \times 10^{-5}\,\Delta T
$$

$ n_y $ is split by wavelength region:

$$
n_y(\lambda, T) = \begin{cases}
\sqrt{2.14559 + \dfrac{0.87629\,\lambda^2}{\lambda^2 - 0.0485} - 0.01173\,\lambda^2} + 1.3 \times 10^{-5}\,\Delta T & \lambda < 1.2\,\mu\mathrm{m} \\[10pt]
\sqrt{2.0993 + \dfrac{0.922683\,\lambda^2}{\lambda^2 - 0.0467695} - 0.0138408\,\lambda^2} + 1.3 \times 10^{-5}\,\Delta T & \lambda \geq 1.2\,\mu\mathrm{m}
\end{cases}
$$

where $ \lambda $ is in µm and $ \Delta T = T - 20\,^\circ\mathrm{C} $.

---

### BiBO (Bismuth Borate)

| Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|
| Biaxial positive | No | [Newlight Photonics](http://www.newlightphotonics.com/v1/bibo-properties.html) | [bibo_1.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/bibo_1.rs) |

$$
n_x = \sqrt{3.0740 + \frac{0.0323}{\lambda^2 - 0.0316} - 0.01337\,\lambda^2}
$$

$$
n_y = \sqrt{3.1685 + \frac{0.0373}{\lambda^2 - 0.0346} - 0.01750\,\lambda^2}
$$

$$
n_z = \sqrt{3.6545 + \frac{0.0511}{\lambda^2 - 0.0371} - 0.0226\,\lambda^2}
$$

where $ \lambda $ is in µm.

---

### LiNbO3 (Lithium Niobate)

| Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|
| Uniaxial negative | Yes | [Newlight Photonics](http://www.newlightphotonics.com/v1/LN-crystal.html) | [linbo3_1.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/linbo3_1.rs) |

$$
n_o(\lambda, T) = \sqrt{4.9048 + \frac{0.11768}{\lambda^2 - 0.04750} - 0.027169\,\lambda^2} - 0.874 \times 10^{-6}\,\Delta T
$$

$$
n_e(\lambda, T) = \sqrt{4.5820 + \frac{0.099169}{\lambda^2 - 0.044432} - 0.021950\,\lambda^2} + 39.073 \times 10^{-6}\,\Delta T
$$

where $ \lambda $ is in µm and $ \Delta T = T - 20\,^\circ\mathrm{C} $.

---

### LiNb:MgO (Magnesium-Doped Lithium Niobate)

| Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|
| Uniaxial negative | Yes | [Appl. Phys. B 91, 343–348 (2008)](https://link.springer.com/article/10.1007/s00340-008-2998-2) | [linb_mgo.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/linb_mgo.rs) |

> Equation 3 of Applied Physics B May 2008, Volume 91, Issue 2, pp 343-348

Temperature enters directly into the Sellmeier equation via:

$$
f(T) = (T - T_0)(T + T_0 + 2 \times 273.16), \quad T_0 = 24.5\,^\circ\mathrm{C}
$$

$$
n_e^2 = A_{e1} + B_{e1}f + \frac{A_{e2} + B_{e2}f}{\lambda^2 - (A_{e3} + B_{e3}f)^2} + \frac{A_{e4} + B_{e4}f}{\lambda^2 - A_{e5}^2} - A_{e6}\,\lambda^2
$$

$$
n_o^2 = A_{o1} + B_{o1}f + \frac{A_{o2} + B_{o2}f}{\lambda^2 - (A_{o3} + B_{o3}f)^2} + \frac{A_{o4} + B_{o4}f}{\lambda^2 - A_{o5}^2} - A_{o6}\,\lambda^2
$$

where $ \lambda $ is in µm and $ T $ is in °C. Coefficients:

| Coefficient | Extraordinary | Ordinary |
|---|---|---|
| $ A_1 $ | 5.756 | 5.653 |
| $ A_2 $ | 0.0983 | 0.1185 |
| $ A_3 $ | 0.2020 | 0.2091 |
| $ A_4 $ | 189.32 | 89.61 |
| $ A_5 $ | 12.52 | 10.85 |
| $ A_6 $ | 1.32e-2 | 1.97e-2 |
| $ B_1 $ | 2.86e-6 | 7.941e-7 |
| $ B_2 $ | 4.7e-8 | 3.134e-8 |
| $ B_3 $ | 6.113e-8 | −4.641e-9 |
| $ B_4 $ | 1.516e-4 | −2.188e-6 |

---

### KDP (Potassium Dihydrogen Phosphate)

| Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|
| Uniaxial negative | No | [Newlight Photonics](http://www.newlightphotonics.com/v1/KDP-crystal.html) | [kdp_1.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/kdp_1.rs) |

$$
n_o^2 = 2.259276 + \frac{13.005522\,\lambda^2}{\lambda^2 - 400} + \frac{0.01008956}{\lambda^2 - 0.012942625}
$$

$$
n_e^2 = 2.132668 + \frac{3.2279924\,\lambda^2}{\lambda^2 - 400} + \frac{0.008637494}{\lambda^2 - 0.012281043}
$$

where $ \lambda $ is in µm.

---

### AgGaSe2 (Silver Gallium Selenide)

| ID | Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|---|
| `AgGaSe2_1` | Uniaxial negative | Yes | [Kildal & Mikkelsen, Opt. Commun. 9, 315 (1973)](https://www.sciencedirect.com/science/article/pii/0030401873903167) | [aggase2_1.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/aggase2_1.rs) |
| `AgGaSe2_2` | Uniaxial negative | Yes | [Bhar, Appl. Opt. 15, 305_1-307 (1976)](https://www.semanticscholar.org/paper/Refractive-index-interpolation-in-phase-matching.-Bhar/63a04ace5f192a7224faa7c36c57f6ea03b99215/figure/0) | [aggase2_2.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/aggase2_2.rs) |

**`AgGaSe2_1`** — Kildal & Mikkelsen (1973):

$$
n_o(\lambda, T) = \sqrt{3.9362 + \frac{2.9113\,\lambda^2}{\lambda^2 - 0.38821^2} + \frac{1.7954\,\lambda^2}{\lambda^2 - 40^2}} + 15 \times 10^{-5}\,\Delta T
$$

$$
n_e(\lambda, T) = \sqrt{3.3132 + \frac{3.3616\,\lambda^2}{\lambda^2 - 0.38201^2} + \frac{1.7677\,\lambda^2}{\lambda^2 - 40^2}} + 15 \times 10^{-5}\,\Delta T
$$

**`AgGaSe2_2`** — Bhar (1976):

$$
n_o(\lambda, T) = \sqrt{4.6453 + \frac{2.2057\,\lambda^2}{\lambda^2 - 0.43347^2} + \frac{1.8377\,\lambda^2}{\lambda^2 - 40^2}} + 15 \times 10^{-5}\,\Delta T
$$

$$
n_e(\lambda, T) = \sqrt{5.2912 + \frac{1.3970\,\lambda^2}{\lambda^2 - 0.53339^2} + \frac{1.9282\,\lambda^2}{\lambda^2 - 40^2}} + 15 \times 10^{-5}\,\Delta T
$$

where $ \lambda $ is in µm and $ \Delta T = T - 20\,^\circ\mathrm{C} $.

---

### LiIO3 (Lithium Iodate)

| ID | Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|---|
| `LiIO3_1` | Uniaxial negative | No | [B. F. Levine, C. G. Bethea; Appl. Phys. Lett. 15 April 1972; 20 (8): 272–275](https://aip.scitation.org/doi/abs/10.1063/1.1654145) | [liio3_1.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/liio3_1.rs) |
| `LiIO3_2` | Uniaxial negative | No | [Takizawa, Okada & Leiri, Opt. Commun. 23, 279 (1977)](https://doi.org/10.1016/0030-4018(77)90326-1) | [liio3_2.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/liio3_2.rs) |

**`LiIO3_1`**:

$$
n_o^2 = 2.03132 + \frac{1.37623\,\lambda^2}{\lambda^2 - 0.0350832} + \frac{1.06745\,\lambda^2}{\lambda^2 - 169.0}
$$

$$
n_e^2 = 1.83086 + \frac{1.08807\,\lambda^2}{\lambda^2 - 0.031381} + \frac{0.554582\,\lambda^2}{\lambda^2 - 158.76}
$$

**`LiIO3_2`**:

$$
n_o^2 = 3.4095 + \frac{0.047664}{\lambda^2 - 0.033991}
$$

$$
n_e^2 = 2.9163 + \frac{0.034514}{\lambda^2 - 0.031034}
$$

where $ \lambda $ is in µm.

---

### AgGaS2 (Silver Gallium Sulfide)

| Axis | Temp. Dependence | Reference | Source |
|---|---|---|---|
| Uniaxial negative | Yes | [Bhar, Appl. Opt. 15, 305_1-307 (1976)](https://www.semanticscholar.org/paper/Refractive-index-interpolation-in-phase-matching.-Bhar/63a04ace5f192a7224faa7c36c57f6ea03b99215/figure/0) | [aggas2_1.rs](https://github.com/spdcalc/spdcalc/blob/master/src/crystal/aggas2_1.rs) |

$$
n_o(\lambda, T) = \sqrt{3.628 + \frac{2.1686\,\lambda^2}{\lambda^2 - 0.1003} + \frac{2.1753\,\lambda^2}{\lambda^2 - 950}} + 15.4 \times 10^{-5}\,\Delta T
$$

$$
n_e(\lambda, T) = \sqrt{4.0172 + \frac{1.5274\,\lambda^2}{\lambda^2 - 0.131} + \frac{2.1699\,\lambda^2}{\lambda^2 - 950}} + 15.5 \times 10^{-5}\,\Delta T
$$

where $ \lambda $ is in µm and $ \Delta T = T - 20\,^\circ\mathrm{C} $.
