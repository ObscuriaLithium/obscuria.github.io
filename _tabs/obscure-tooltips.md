---
title: Obscure Tooltips
layout: post
icon: fas fa-book
order: 1
toc: true
comments: true
image:
  path: /assets/images/obscure-tooltips-logo.jpg
---

# Welcome to the Obscure Tooltips Wiki!

The information provided here is intended to help understand the core concepts of the mod and customize it to your needs.

> This wiki is relevant only for **version 3.0.0 and above**.<br>Older versions are incomplete and may be unstable.
{: .prompt-info }

### Core Concept

Obscure Tooltips is a fully data-driven mod with a **modular approach** to content. Tooltips are built like with a **constructor**: complex elements combine smaller blocks for flexibility, reusability, and easy customization – you can assemble existing parts or create entirely new ones.

- The smallest building blocks are [Panels](https://github.com/ObscuriaLithium/obscure-tooltips/wiki/Tooltip-Elements#panels), [Frames](https://github.com/ObscuriaLithium/obscure-tooltips/wiki/Tooltip-Elements#frames), [Slots](https://github.com/ObscuriaLithium/obscure-tooltips/wiki/Tooltip-Elements#slots), [Icons](https://github.com/ObscuriaLithium/obscure-tooltips/wiki/Tooltip-Elements#icons), and [Effects](https://github.com/ObscuriaLithium/obscure-tooltips/wiki/Tooltip-Elements#effects) – JSON files that define how each element looks. These elements are **visual definitions only**: they don’t know how or where they will be used, only how they appear.

- These elements are then combined into [Styles](https://github.com/ObscuriaLithium/obscure-tooltips/wiki/Tooltip-Styles) – JSON files containing references to a Panel, a Frame, and other constituent elements. A Style is also purely descriptive and does not contain application logic.

- To apply a Style to items, [Definitions](https://github.com/ObscuriaLithium/obscure-tooltips/wiki/Tooltip-Definitions) are used – JSON files that specify a priority, a reference to a Style, and filters determining which items the Style applies to (by ID, tags, rarity, NBT, etc.).

In summary, each layer has a **single responsibility**: either describing the visual appearance or defining application rules. This separation makes maintaining and scaling your designs straightforward and efficient.

-----

## Tooltip Elements

### Panels

Panels define the visual background of a tooltip and serve as the foundation for text and other elements.
 
> Resource Pack Directory: `assets/<modid>/tooltips/element/panel/`
{: .prompt-tip }

#### 1. [Blank Panel](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/panel/BlankPanel.java)

Essentially, it acts as an invisible placeholder.

```json
{
  "type": "obscure_tooltips:blank"
}
```

#### 2. [Color Rect Panel](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/panel/ColorRectPanel.java)

A rectangular panel with a border styled after the vanilla design. The gradient palette can be customized for both the panel surface and its border. See [Colors](#colors) for more details.

```json
{
  "type": "obscure_tooltips:color_rect",
  "background_palette": {
    "top_left": "#f0100010",
    "top_right": "#f0100010",
    "bottom_left": "#f0100010",
    "bottom_right": "#f0100010"
  },
  "border_palette": {
    "top_left": "#505000ff",
    "top_right": "#505000ff",
    "bottom_left": "#5028007f",
    "bottom_right": "#5028007f"
  }
}
```

<br>

### Frames

Frames are decorative layers drawn on top of panels in tooltips.

> Resource Pack Directory: `assets/<modid>/tooltips/element/frame/`
{: .prompt-tip }

#### 1. [Blank Frame](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/frame/BlankFrame.java)

Essentially, it acts as an invisible placeholder.

```json
{
  "type": "obscure_tooltips:blank"
}
```

#### 2. [Nine Sliced Frame](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/frame/NineSlicedFrame.java)

This frame uses a texture divided into 9 sections to automatically stretch and align the corners and edges of the tooltip. You can use the built-in [golden_frame.png](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/resources/assets/obscure_tooltips/textures/gui/golden_frame.png) as a reference for positioning your own textures.

```json
{
  "type": "obscure_tooltips:nine_sliced",
  "texture_sheet": "obscure_tooltips:textures/gui/golden_frame.png"
}
```

<br>

### Slots

> Resource Pack Directory: `assets/<modid>/tooltips/element/slot/`
{: .prompt-tip }

#### 1. [Blank Slot](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/slot/BlankSlot.java)

Essentially, it acts as an invisible placeholder.

```json
{
  "type": "obscure_tooltips:blank"
}
```

#### 2. [Color Rect Slot](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/slot/ColorRectSlot.java)

A rectangular panel with a borders.

```json
{
  "type": "obscure_tooltips:color_rect",
  "borders": "#30ffffff",
  "palette": {
    "top_left": "#20ffffff",
    "top_right": "#20ffffff",
    "bottom_left": "#20ffffff",
    "bottom_right": "#20ffffff"
  }
}
```

<br>

### Icons

> Resource Pack Directory: `assets/<modid>/tooltips/element/icon/`
{: .prompt-tip }

#### 1. [Blank Icon](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/icon/BlankIcon.java)

Essentially, it acts as an invisible placeholder.

```json
{
  "type": "obscure_tooltips:blank"
}
```

#### 2. [Static Icon](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/icon/StaticIcon.java)

See [Transform](#transform) for more details.

```json
{
  "type": "obscure_tooltips:static",
  "transform": {
    "offset": [ 0.0, 0.0, 0.0 ],
    "scale": 1.0,
    "rotation": 0.0
  }
}
```

#### 3. [Accent Icon](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/icon/AccentIcon.java)

```json
{
  "type": "obscure_tooltips:accent",
  "transform": {
    "offset": [ 0.0, 0.0, 0.0 ],
    "scale": 1.0,
    "rotation": 0.0
  }
}
```

#### 4. [Accent Spin Icon](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/icon/AccentSpinIcon.java)

```json
{
  "type": "obscure_tooltips:accent_spin",
  "transform": {
    "offset": [ 0.0, 0.0, 0.0 ],
    "scale": 1.0,
    "rotation": 0.0
  }
}
```

#### 5. [Accent Burst Icon](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/icon/AccentBurstIcon.java)

```json
{
  "type": "obscure_tooltips:accent_burst",
  "transform": {
    "offset": [ 0.0, 0.0, 0.0 ],
    "scale": 1.0,
    "rotation": 0.0
  }
}
```

<br>

### Effects

> Resource Pack Directory: `assets/<modid>/tooltips/element/effect/`
{: .prompt-tip }

#### 1. [Rim Light Effect](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/effect/RimLightEffect.java)

```json
{
  "type": "obscure_tooltips:rim_light",
  "outer_palette": {
    "top_left": "#30f00fff",
    "top_right": "#30f00fff",
    "bottom_left": "#30f00fff",
    "bottom_right": "#30f00fff"
  },
  "inner_palette": {
    "top_left": "#00ff00ff",
    "top_right": "#00ff00ff",
    "bottom_left": "#00ff00ff",
    "bottom_right": "#00ff00ff"
  }
}
```

#### 2. [Ray Glow Effect](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/effect/RayGlowEffect.java)

```json
{
  "type": "obscure_tooltips:ray_glow",
  "primary_color": "#fff00fff",
  "secondary_color": "#ffff5e0f"
}
```

#### 3. [Inward Particle Effect](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/effect/InwardParticleEffect.java)

See [Particles](#particles) for more details.

```json
{
  "type": "obscure_tooltips:inward_particle",
  "particle": {
    "type": "obscure_tooltips:line",
    "center_color": "#80ff80ff",
    "edge_color": "#00aa40aa",
    "transform": {
      "offset": [ 0.0, 0.0, 0.0 ],
      "scale": 1.0,
      "rotation": 0.0
    }
  }
}
```

#### 4. [Icon Particle Effect](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/element/effect/IconParticleEffect.java)

```json
{
  "type": "obscure_tooltips:icon_particle",
  "particle": {
    "type": "obscure_tooltips:texture",
    "texture": "obscure_tooltips:textures/gui/particle/star.png",
    "transform": {
      "offset": [ -0.5, -0.5, 0.0 ],
      "scale": 1.5,
      "rotation": 0.0
    }
  }
}
```

-----

## Tooltip Styles

Style files simply combine elements to define the visual appearance of a style. In the example below, elements are referenced from `assets/obscure_tooltips/tooltips/element/<kind>/default.json`. Here, `<kind>` can be `panel`, `frame`, `slot`, `icon`, etc.

> Resource Pack Directory: `assets/<modid>/tooltips/style/`
{: .prompt-tip }

```json
{
  "panel": "obscure_tooltips:default",
  "frame": "obscure_tooltips:default",
  "slot": "obscure_tooltips:default",
  "icon": "obscure_tooltips:default",
  "effects": []
}
```

> Note that all fields except `effects` are optional. The `effects` array **must always be included**, even if it is empty.
{: .prompt-info }

-----

## Tooltip Definitions

Definition files determine which items a style should apply to, based on the specified filter. In the example below, the style located at `assets/obscure_tooltips/tooltips/style/default.json` will be applied to **all items**:

> Resource Pack Directory: `assets/<modid>/tooltips/definition/`
{: .prompt-tip }

```json
{
  "priority": 0,
  "style": "obscure_tooltips:default",
  "filter": {
    "type": "obscure_tooltips:always"
  }
}
```

The `priority` field is used in the style merging system.

### Style Merging (Fallback)

A key feature of Obscure Tooltips is the style merging system. When an item matches multiple Definition files, the styles from these definitions are combined according to the following rules:
1. The style with the **highest priority** becomes the base.
2. Any **empty fields** (i.e., Optional elements not defined) in this base style are filled in from the next style in priority. This process continues through all matching styles, in order of priority.
3. The **effect lists** from all styles are merged together.

**Why is this useful?**
 
Suppose you create a `default.json` definition with **minimal priority**, fill in all style elements (panel, frame, slots, icons, etc.), and set its filter to `obscure_tooltips:always`. This style will apply to **all items** by default.

Next, you create an `enchanted.json` definition for enchanted items, assign a style with a fancy frame and glow effects, but leave other elements (like the panel) empty. You set a **higher priority** and a filter for enchanted items only.

**Now:**
- All items will use `default.json` as their base style.
- Enchanted items will override the base frame and gain the additional glow effect from `enchanted.json`.
- Any undefined style fields in `enchanted.json` will fall back to the corresponding fields in `default.json`.

> This system allows you to layer styles, avoid repetition, and easily create complex tooltip designs that automatically adapt to different item types.
{: .prompt-info }

-----

## Tooltip Filters

Filters are not registered as separate files – instead, they are written inline wherever they are needed:

```json
"filter": {
  "type": "obscure_tooltips:always"
}
```

Although filter fields are not arrays, you can still combine multiple filters using the aggregate types `all_of`, `any_of`, and `none_of`:

```json
"filter": {
  "type": "obscure_tooltips:all_of",
  "terms": [
    {
      "type": "obscure_tooltips:<first_filter>"
    },
    {
      "type": "obscure_tooltips:<second_filter>"
    }
  ]
}
```

You can also nest aggregate filters inside one another to create more advanced filtering logic.

<br>

### 1. [Always Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/AlwaysFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:always"
}
```

### 2. [Never Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/NeverFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:never"
}
```

### 3. [All Of Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/AllOfFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:all_of",
  "terms": []
}
```

### 4. [Any Of Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/AnyOfFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:any_of",
  "terms": []
}
```

### 5. [None Of Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/NoneOfFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:none_of",
  "terms": []
}
```

### 6. [Item Or Tag Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/ItemOrTagFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:item",
  "values": [
    "minecraft:apple",
    "#minecraft:planks"
  ]
}
```

### 7. [Mod Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/ModFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:mod",
  "mods": [
    "minecraft",
    "aquamirae"
  ]
}
```

### 8. [Enchantment Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/EnchantmentFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:enchantment",
  "any_enchantment": true,
  "any_curse": true,
  "enchantments": [
    "Minecraft:fire_aspect"
  ]
}
```

### 9. [Rarity Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/RarityFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:rarity",
  "rarity": "epic"
}
```

### 10. [NBT Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/NbtFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:nbt",
  "nbt": "{test_tag:{sub_tag:1}}"
}
```

### 11. [Property Filter](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/filter/PropertyFilter.java)

```json
"filter": {
  "type": "obscure_tooltips:property",
  "has_foil": true
}
```

-----

## Tooltip Labels

Label files define the additional line of text displayed beneath an item’s name. Using **providers**, labels can display the item’s rarity or custom text. If an item matches multiple label definitions, the one with the **highest priority** is applied.

> Resource Pack Directory: `assets/<modid>/tooltips/label/`
{: .prompt-tip }

For example, the following file will display the **rarity label** for **all items**:

```json
{
  "priority": 0,
  "provider": {
    "type": "obscure_tooltips:rarity"
  },
  "filter": {
    "type": "obscure_tooltips:always"
  }
}
```

<br>

### 1. [Rarity Label Provider](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/label/RarityLabelProvider.java)

```json
"provider": {
  "type": "obscure_tooltips:rarity"
}
```

### 2. [Literal Label Provider](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/label/LiteralLabelProvider.java)

```json
"provider": {
  "type": "obscure_tooltips:literal",
  "text": "Some Text"
}
```

### 3. [Translatable Label Provider](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/label/TranslatableLabelProvider.java)

```json
"provider": {
  "type": "obscure_tooltips:translatable",
  "key": "label.my_mod.some_text"
}
```

-----

## Miscellaneous

### Colors

Whenever you need to define a color, you can use one of the following formats:

- **Hexadecimal (ARGB)** – a string in the form #AARRGGBB
- **Decimal (ARGB)** — a 32-bit unsigned integer value
- **Normalized float array (ARGB)** — an array of four values in the range 0.0–1.0, representing [Alpha, Red, Green, Blue]

```json
{
  "color": "#ffffffff",
  "color": 4294967295,
  "color": [ 1.0, 1.0, 1.0, 1.0 ]
}
```

### Transform

The transform object is always optional. If omitted, default values are used. Each property inside transform is also optional and will fall back to its own default.

- **offset** — a 3D vector [x, y, z] that shifts the object’s position
- **scale** — a uniform scale factor (default: 1.0)
- **rotation** — a rotation angle in degrees (default: 0.0)

```json
"transform": {
  "offset": [ 0.0, 0.0, 0.0 ],
  "scale": 1.0,
  "rotation": 0.0
}
```

### Particles

Particles are used by certain effects. There are multiple particle types available:

#### 1. [Line Particle](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/particle/LineParticle.java)

A horizontal line one pixel thick, with a gradient fading toward the center.

```json
"particle": {
  "type": "obscure_tooltips:line",
  "center_color": "#ffffffff",
  "edge_color": "#00ffffff",
  "transform": {}
}
```

#### 2. [Texture Particle](https://github.com/ObscuriaLithium/obscure-tooltips/blob/master/common/src/main/java/dev/obscuria/tooltips/client/particle/TextureParticle.java)

A particle rendered from a square texture. Any 1:1 resolution texture can be used, but with the default scale it is treated as having a virtual size of 16x16 pixels.

```json
"particle": {
  "type": "obscure_tooltips:texture",
  "texture": "obscure_tooltips:textures/gui/particle/star.png",
  "transform": {}
}
```

## Example Usage

To see all features in action, check out the built-in Obscuria Tooltips [resource pack](https://github.com/ObscuriaLithium/obscure-tooltips/tree/master/common/src/main/resources).

## Overriding

If you want to completely disable the built-in tooltips from the mod, you can override the Obscure Tooltips definition files in your resource pack. Just follow the standard Minecraft resource override rules and apply the `obscure_tooltips:never` filter. This ensures that none of the default styles will ever be applied to any item.

## Hotswap

While developing a resource pack, you can quickly reload your changes in-game by pressing `F3 + T` inside a Minecraft world.

## Any Questions?

Join my [Discord Server](https://dsc.gg/obscuria) or ask your question in the comments at the bottom of this page.
