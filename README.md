# Bedrock Horizons

<div align="center">
  <img width="1024" height="256" alt="Bedrock Horizons Title Banner" src="https://github.com/user-attachments/assets/b0198334-7d8a-4357-a586-50829b753fad" />

### A cinematic visual overhaul for Minecraft: Bedrock Edition

  [![Minecraft](https://img.shields.io/badge/Minecraft-Bedrock%20v1.26.0+-5E9C31?style=for-the-badge&logo=minecraft&logoColor=white)](https://minecraft.net)
  [![Pipeline](https://img.shields.io/badge/Pipeline-Vibrant%20Visuals%20(Deferred)-8B5CF6?style=for-the-badge)](https://minecraft.net)
  [![Code License](https://img.shields.io/badge/Code-MPL--2.0-orange?style=for-the-badge)](LICENSE)
  [![Textures License](https://img.shields.io/badge/Textures-CC%20BY--NC--SA%204.0-blue?style=for-the-badge)](LICENSE)

</div>

---

Bedrock Horizons is a complete art and lighting pass for Bedrock's
**Vibrant Visuals** deferred renderer: a Catppuccin-flavoured PBR texture
set for the whole game, plus per-biome atmosphere, water and colour
grading built on top of it.

Everything in the pack is **generated from source**. `tools/` contains a
build pipeline that recolours real Minecraft artwork into the Catppuccin
palette, derives every PBR map from those actual pixels, and writes all
6,590 textures and 2,261 settings files in about 13 seconds.
`tools/validate.py` then checks the result for the structural mistakes
Bedrock fails silently on.

---

## What's in it

### God rays

The headline effect, and the one the whole atmosphere system is tuned
around. Crepuscular rays are not a single toggle — they come out of four
numbers acting together, set per biome family:

| Knob | What it does |
| :--- | :--- |
| `max_density` | how much participating medium there is to light |
| `scattering` (RGB) | the colour of the shaft |
| `absorption` (RGB) | what the shaft loses with distance, per wavelength |
| `henyey_greenstein_g` | how tightly scattering hugs the light direction |

`g` is the one that actually makes a shaft. At 0 the medium scatters
evenly and you get flat haze; pushed towards 0.91 the lobe tightens
around the sun, so the air only lights up where you are looking nearly
into it — which is exactly a beam through a canopy or a cave mouth.

Absorption is what *colours* the shaft. Open air extinguishes blue
fastest, so what survives the long slant path into the camera is warm —
that is why the beams read as sunlight rather than as grey haze. Caves,
the Deep Dark, the Nether and the End invert that deliberately.

The coefficients are calibrated against a maxed-out reference fog, not
against the conservative values in Mojang's sample packs. The difference
is roughly twenty-fold, and it is the whole difference between "there is
fog here" and a visible shaft.

Each environment gets its own character rather than one global fog:

| | density | `g` | |
| :--- | ---: | ---: | :--- |
| **Jungle** | 0.245 | 0.91 | solid columns through the canopy |
| **Swamp** | 0.245 | 0.80 | thick, sour, heavily absorbed |
| **Forest** | 0.213 | 0.88 | the canonical god-ray look |
| **Peaks** | 0.104 | 0.88 | long thin beams in thin air |
| **Desert** | 0.088 | 0.72 | glare haze, not defined shafts |
| **Deep Dark** | 0.245 | 0.67 | absorption far exceeding scattering — a torch lights a small sphere and the rest stays genuinely black |

Rain and snow get their own participating medium, so a storm thickens the
volume and catches light without leaving the world permanently fogged
once it passes, and clouds get their own scattering pair so a low sun can
light them from beneath.

### Water, and caustics that match it

Nine water types, each with its own absorption spectrum, wave geometry
**and its own caustics flipbook**. The caustics are not a stock texture —
they are solved from the physics:

> Light through a wavy surface focuses where the surface is concave. A ray
> bundle covering area `dA` lands on `dA · |1 + k∇²h|`, and irradiance is
> the inverse of that. So `I = 1 / |1 + k · ∇²h|` — and the bright
> filaments, the cusps where two cross, and the dark cells between them
> all fall out of that one expression.

The surface is a sum of sinusoids on integer spatial and temporal
frequencies, so every sheet tiles seamlessly and the 32-frame loop closes
exactly. Red is refracted slightly less than blue, so the filaments carry
real chromatic fringing.

| Water | Look |
| :--- | :--- |
| `tropical` | finest, hardest, highest-contrast net; strong dispersion |
| `glacial` | fine crystalline mesh, cold and slow |
| `ocean` | long swell, big slow cells stretched along the swell |
| `river` | smeared downstream instead of forming closed cells |
| `murky` | suspended matter blurs it almost to nothing |
| `deep`, `clear`, `default`, `void` | between those extremes |

### Textures

Every block and item gets colour, **MER**, **normal** and **heightmap**,
plus a `.texture_set.json`.

The pixels are **real Minecraft artwork, recoloured** — not generated
patterns. At 16×16 there is nowhere for a noise field to hide, and
hand-drawn art carries decisions (which pixel is the highlight, where the
crack runs, how a plank's grain breaks) that noise does not reproduce.

Each pixel keeps its position in the image's own tonal order; only the
colour that position maps to changes. Palette is **Catppuccin**: Mocha's
violet-leaning greys for the neutrals, the named accents at full strength
for anything that should pop. Ramps are built in **OKLab** with gamut
mapping, so chroma can be pushed hard without the midtones going muddy or
a saturated blue clipping to `#0000FF`.

Whether hue is replaced outright or merely pushed is decided *per texture*
by measuring the source's hue spread — so stone takes the ramp's hue
while a bookshelf keeps its multicoloured books. The inclusion pixels in a
texture (the mineral in an ore, the turf on a grass side) are found by
perceptual distance from the tile's median colour and recoloured through
their own ramp, which is why gold ore stays gold, coal ore stays black,
and grass side keeps green grass on brown dirt.

Blocks added after the source set borrow a structurally similar texture —
deepslate takes stone's grain, cherry planks take oak's boards, oxidised
copper takes the iron block's plate — and then get their own palette and
material class.

All four maps are co-registered by construction, so the height the normal
is differentiated from is the height that shaded the albedo. A mortar
line is dark *because* it is recessed.

Mobs and particles get a texture set with **inline MER values** rather
than an invented colour map — mob art is UV-atlased per model, so the art
stays and gains a correct material response (a wet fleshy zombie, a
metallic iron golem, a glowing warden).

### Everything else

* **90 client biomes**, each wired to one of 36 lighting / atmosphere /
  fog / grading families.
* **Physically-shaped day cycle** — sun illuminance and colour temperature
  curves anchored on golden hour, blue hour and civil twilight, with
  Rayleigh strength peaking at the horizon crossings so a low sun reddens
  for the right reason.
* **Local lighting** for 90+ emissive blocks, coloured by source physics:
  flame at ~1850 K, soul fire's copper-ion blue, redstone's narrow red
  band, sculk's cyan bioluminescence, and copper lamps that shift green as
  they oxidise.
* **Six quality subpacks** — Performance → Cinematic — scaling shadow
  resolution, volumetric density *and* media coefficients, wave octaves
  and caustics.
* **ACES tone mapping** with per-family lift/gamma/gain across shadows,
  midtones and highlights.

---

## Installing

1. Download the latest `.mcpack` from **Releases**, or build one with
   `python3 tools/package.py`.
2. Open the file to import it into Minecraft: Bedrock Edition.
3. Turn on **Vibrant Visuals** in video settings.
4. Enable **Bedrock Horizons** under `Global Resources` or the world's
   resource packs, and move it to the top of the list.
5. Pick a quality subpack in the pack's settings (**High** is the default
   recommendation; the game preselects one from device memory).

Requires Bedrock **1.26.0+** with Vibrant Visuals available and enabled.
Without Vibrant Visuals the textures still apply — you get the Catppuccin
art with vanilla lighting, but none of the atmosphere or water work.

---

## Building

No third-party Python packages. Python 3.10+.

Textures are recoloured from a Minecraft source set. Point
`BH_VANILLA_TEXTURES` at any Bedrock pack's `textures/` directory; without
one the build still completes using the procedural fallback generators,
but the result is markedly worse.

```bash
python3 tools/build.py            # everything (~13s on 10 cores)
python3 tools/build.py json       # rendering config only (fast iteration)
python3 tools/build.py textures   # textures only
python3 tools/build.py caustics   # caustics flipbooks only

python3 tools/validate.py         # check the built pack
python3 tools/package.py          # -> bedrock_horizons.mcpack

python3 tools/preview.py stone /tmp/out.png          # contact sheet
python3 tools/preview.py glow /tmp/out.png normal    # ...of the normal maps
```

Everything is seeded off the texture name, so a rebuild is byte-identical
and the whole pack diffs cleanly.

See [`docs/`](docs/) for how the pipeline fits together
([ARCHITECTURE](docs/ARCHITECTURE.md)) and which knob to turn for a given
visual change ([TUNING](docs/TUNING.md)).

---

## Licensing

| Component | License |
| :--- | :--- |
| Build pipeline & JSON configs | [MPL-2.0](LICENSE) |
| Generated textures & artwork | [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) |

Palette derived from [Catppuccin](https://github.com/catppuccin/catppuccin)
(MIT).

Contributions and issue reports are welcome — see
[CONTRIBUTING.md](CONTRIBUTING.md).

---

<div align="center">

**Created and maintained by Draco12191712 (Vivaan Bobade)**

*If you enjoy Bedrock Horizons, consider giving this repository a star.*

</div>
