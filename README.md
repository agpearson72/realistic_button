## Realistic Button Templates for Home Assistant

A set of polished button-card templates for lights, media, climate, fireplaces, and fans—designed to look realistic with soft depth, a glossy top, and dynamic “glow” that reflects device state (including true light colors and Twinkly effects).

> Templates included

> * realistic_button (base)

> * realistic_button_climate

> * realistic_button_fireplace

> * realistic_button_fan
>
<img width="1048" height="730" alt="image" src="https://github.com/user-attachments/assets/9acfa082-57ff-4e35-ab70-85c674429b35" />




## Installation

1. Ensure you’ve installed button-card (HACS or manual) and added its resource to Lovelace.

1. Copy the template YAML into your dashboard’s button_card_templates: section.

1. Use the examples below for each template.

> Tip: Keep the default aspect_ratio: 1/1 unless you explicitly want a rectangle. Avoid wrapping aspect_ratio in [[[ ... ]]]—it can break layout/stacking.<BR>
> If you use a Grid, set "square: false" if you want to use aspect_ratio to change the button's shape.


## Common Design & Anatomy

### Grid layout (default):
* i: icon, badge: tiny status pill

* n: name, s: state, l: label

### Special layers (absolute, full-card):

* custom_fields.gloss – subtle glass highlight

* custom_fields.glow – dynamic glow (radial or full)

* custom_fields.under_glow – faint color wash beneath content

* custom_fields.indicator – small red/green dot (optional)


## Base Template — realistic_button

Use this for lights, switches, sensors, media, etc. It automatically:

* Shows a bottom-anchored glow that matches the light’s color (rgb_color, hs_color, or temperature → hue).

* Can color-match light groups (via entity_id members).

* Supports Twinkly Light effects (multi-color radial blend) with a palette map.

* Optional state dot, badge, gloss, and full-card glow.

### Minimal Example
<img width="753" height="170" alt="image" src="https://github.com/user-attachments/assets/f562a9d8-547f-435c-9174-82878a3fdcc8" />


## Useful variables (base)


Variable | Type | Default | Notes
-- | -- | -- | --
accent | color | var(--accent-color) | Fallback   accent
show_state_dot | bool | FALSE | Red/green   dot bottom-right
show_gloss | bool | FALSE | Enable   top gloss layer
gloss_top_opacity | 0–1 | 0.18 | Gloss   strength at top
gloss_mid_opacity | 0–1 | 0.06 | Mid-stop   opacity
gloss_mid_stop | % | 25 | Transition   stop (%)
gloss_break_stop | % | 46 | Fade-out   stop (%)
glow_full | bool | FALSE | Full-card   glow overlay
glow_full_alpha | 0–1 | 0.35 | Full-glow   strength
glow_blend_mode | string | screen | normal/screen
glow_origin_x/y | % | 50 / 88 | Radial   center
glow_radius_x/y | % | 120 / 90 | Radial   size
glow_falloff | % | 65 | Fade   distance
glow_for_non_lights | bool | TRUE | Glow   for switches/media
glow_non_light_color | color | accent | Non-light   glow color
glow_non_light_opacity | 0–1 | 0.35 | Non-light   glow opacity
icon_color_matches_light | bool | TRUE | Icon   adopts light color
twinkly_members | list | [] | Entities   to inspect for effect/color
twinkly_multi_mode | enum | blend | blend or single
twinkly_effect_map | dict | (provided) | Map   effect→single color
twinkly_effect_palettes | dict | (provided) | Effect→palette   (multi)

### Twinkly: multi-color glow
<img width="758" height="131" alt="image" src="https://github.com/user-attachments/assets/70fbdef8-2027-4f39-b5b7-2476d811f9c8" /><BR>
The glow will render a multi-stop radial gradient when an effect name matches.


### Per-card icon overrides
<img width="753" height="101" alt="image" src="https://github.com/user-attachments/assets/96d69cfb-08f5-46bb-9aa5-47db3fd6d224" />


### Triggers for live updates
<img width="760" height="115" alt="image" src="https://github.com/user-attachments/assets/bfd4a838-d6c9-4a0a-b68e-bf46bf7d505e" />


## Climate Template — realistic_button_climate
Adds a big temperature and an HVAC-tinted background. Works with hvac_action or hvac_mode. Optionally read ambient from a separate sensor.<BR>
<img width="752" height="200" alt="image" src="https://github.com/user-attachments/assets/d4cada10-c44b-4f71-b223-13a0703b2aa3" />

### Variables (climate)

Variable | Type | Default | Notes
-- | -- | -- | --
ambient_sensor | entity_id | null | Use this sensor for big temp
show_setpoint | bool | TRUE | Show target temp/range
show_humidity | bool | FALSE | Add % RH
show_mode | bool | TRUE | Add hvac action/mode
bg_tint_alpha | 0–1 | 0.18 | Background tint strength
heat_color/cool_color/... | color | (provided) | Colors by state
hvac_glow_full | bool | TRUE | Full-card glow tinted by state
hvac_glow_alpha | 0–1 | 0.22 | Glow strength
icon_size_css | CSS | clamp(18px,5.5vw,26px) | Responsive icon
temp_font_css | CSS | clamp(20px,7vw,38px) | Responsive temp
name_font_css | CSS | clamp(12px,3.2vw,16px) | Responsive name
set_font_css | CSS | clamp(10px,2.8vw,14px) | Responsive footer


The temp row uses 1fr to fill vertical space so the footer sits near the bottom.

## Fireplace Template — realistic_button_fireplace
Shows orange/red glow for low/high, with an optional animated flame (moving/flicker) glow.
### Example
<img width="749" height="267" alt="image" src="https://github.com/user-attachments/assets/027cb41f-58a6-4094-acb3-02465f58b961" /><BR>

## Variables (fireplace)


Variable | Type | Default | Notes
-- | -- | -- | --
fireplace_attr | string | null | Where to read level (e.g., preset_mode, flame, level)
fireplace_high_states | list | ['high','hi','max','on_high','on   hi','2'] | Matches treated as “high”
fireplace_low_states | list | ['low','lo','min','on_low','on   low','1'] | Matches treated as “low”
fireplace_high_color | color | #ff3b3b | High glow/icon
fireplace_low_color | color | #ff9900 | Low glow/icon
fireplace_full_glow | bool | TRUE | Full-card tint when on
fireplace_glow_alpha | 0–1 | 0.26 | Glow strength
flame_enabled | bool | TRUE | Turn animation on/off
flame_speed | time | 2.8s | Up/down cycle
flame_flicker_speed | time | 1.3s | Flicker cycle
flame_move_y_min/max | % | 0%/-4% | Vertical motion range
flame_scale_min/max | number | 1 / 0.95 | Squeeze effect
flame_flicker_min/max | number | 0.92/1.08 | Brightness flicker


## Fan Template — realistic_button_fan
A button-card template (inherits realistic_button) for fans.
It:
> * Colors the icon by state (on / off / unavailable)

> * Shows a speed label: Low / Medium / High (or raw %)

> * Spins the icon at variable rates based on speed/percentage

> * Adds a configurable glow (color, alpha, bottom-radial or full-card)

> * Can control a different fan on tap (handy for linked controls)

Requires: custom:button-card and your base realistic_button template to be loaded.

Variable  |  Type  |  Default  |  What it does
-- | -- | -- | --
fan_control_entity | entity_id/false | FALSE | Target for tap action. If falsy, uses the card’s entity.
fan_on_color | color | rgb(34,197,94) | Icon color when on.
fan_off_color | colo | var(--secondary-text-color) | Icon color when off.
fan_unavailable_color | color | rgb(255,0,0) | Icon color when unavailable.
fan_speed_labels | map | {33: Low, 66: Medium, 100: High} | Map percentage → label text.
fan_spin_low | time	2.3s | Spin duration at low speed.
fan_spin_med | time	1.2s | Spin duration at medium speed.
fan_spin_high | time | .5s | Spin duration at high speed.
fan_low_threshold | number | 33 | Boundary for low tier.
fan_med_threshold | number | 66 | Boundary for medium tier.
fan_value_attr | enum | auto | Where to read speed: auto / percentage / speed / preset_mode.
fan_glow_color | color/CSS var | var(--rb-fan-glow-color, #22c55e) | Glow color. Accepts hex/rgb/hsl or var(...).
fan_glow_alpha | number (0–1) | 0.3	Glow opacity.
fan_glow_full | bool | FALSE | true = full-card tint; false = bottom radial glow.

### Basic Usage:
<img width="754" height="124" alt="image" src="https://github.com/user-attachments/assets/797ba56d-39ac-41a1-a9de-9d84f5ad3650" />

### Per-Card Glow Override:
<img width="748" height="212" alt="image" src="https://github.com/user-attachments/assets/77cfc308-4aed-4bdd-bd99-11207a6c4671" />

### If your integration doesn't expose percentage:
<img width="754" height="75" alt="image" src="https://github.com/user-attachments/assets/d3a74385-bfe7-4d0d-9fe1-25332dc84d3d" />


### Tap/Hold (defaults):
<img width="748" height="169" alt="image" src="https://github.com/user-attachments/assets/f574f27e-1974-4fa3-896f-1e1838a6737c" />

## Advanced Tips
### Scrolling (marquee) label for long titles
<img width="790" height="200" alt="image" src="https://github.com/user-attachments/assets/c89b54a8-4eff-49c0-a0c5-5b22c34ff27c" />
<img width="749" height="240" alt="image" src="https://github.com/user-attachments/assets/ae66903c-e9fc-4426-ab30-7dd55fc7eaed" /><BR>
Applied on the media_player button

### Entity pictures (cover/TV/app artwork)
<img width="754" height="439" alt="image" src="https://github.com/user-attachments/assets/9b4ce39b-02a2-4ad1-a987-858092b221a7" />

### Locking a dangerous control (e.g., garage door)
<img width="760" height="158" alt="image" src="https://github.com/user-attachments/assets/94efa070-232a-4f9e-8585-b94f99cfd092" />

### Updating quickly when other entities change
Use triggers_update to watch related entities—e.g., fans, Apple TV, Twinkly group members.

### Troubleshooting
* **Fan glow looks yellow / too bright**
> You might be stacking the base glow from realistic_button with the fan glow. Disable the base non-light glow for fan cards using:
> <img width="718" height="76" alt="image" src="https://github.com/user-attachments/assets/e1baf3ae-5ff1-41c8-838e-64b3a98a0dc2" />

* **Buttons stack unexpectedly**
> Keep aspect_ratio as a literal 1/1, not a JS template string.
* **No icon showing**
> Ensure your grid includes "i" and the icon style has grid-area: i (the provided templates do).
* **Glow visible with a gap**
> The glow layers use position: absolute; inset: 0; border-radius: inherit—there’s no padding. If you see a gap, another wrapper (stack/grid) may have padding—remove it there.
* **Fireplace animation doesn’t move**
> Confirm extra_styles contains the keyframes once, and flame_enabled: true. Also make sure the card treats the device as fireplace (set fireplace_attr or put “fireplace” in the friendly name).
* **Twinkly effect shows one color**
> Multi-color only appears when twinkly_multi_mode: blend and a palette matches the effect text (number prefixes like 14 Carnival are stripped). Tweak twinkly_effect_palettes keys to match.

### Example: putting three side-by-side
<img width="753" height="396" alt="image" src="https://github.com/user-attachments/assets/deff9238-a6b0-491e-97d7-b996a7c3151f" />

### Contributing
* Open issues/PRs on GitHub with:

> * your entity attributes (from Dev Tools → States),

> * the card YAML snippet,

> * a screenshot of the unexpected result.

