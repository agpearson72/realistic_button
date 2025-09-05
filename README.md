## Realistic Button Templates for Home Assistant

A set of polished button-card templates for lights, media, climate, fireplaces, and fans—designed to look realistic with soft depth, a glossy top, and dynamic “glow” that reflects device state (including true light colors and Twinkly effects).

> Templates included

> * realistic_button (base)

> * realistic_button_climate

> * realistic_button_fireplace

> * realistic_button_fan
>
> * <img width="1048" height="730" alt="image" src="https://github.com/user-attachments/assets/4238f465-ee4a-4bc5-ba02-54af1135b642" />



## Installation

1. Ensure you’ve installed button-card (HACS or manual) and added its resource to Lovelace.

1. Copy the template YAML into your dashboard’s button_card_templates: section.

1. Use the examples below for each template.

> Tip: Keep the default aspect_ratio: 1/1 unless you explicitly want a rectangle. Avoid wrapping aspect_ratio in [[[ ... ]]]—it can break layout/stacking.


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


<html xmlns:v="urn:schemas-microsoft-com:vml"
xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:x="urn:schemas-microsoft-com:office:excel"
xmlns="http://www.w3.org/TR/REC-html40">

<head>

<meta name=ProgId content=Excel.Sheet>
<meta name=Generator content="Microsoft Excel 15">
<link id=Main-File rel=Main-File
href="file:///C:/Users/AGPEAR~1/AppData/Local/Temp/msohtmlclip1/01/clip.htm">
<link rel=File-List
href="file:///C:/Users/AGPEAR~1/AppData/Local/Temp/msohtmlclip1/01/clip_filelist.xml">
<!--table
	{mso-displayed-decimal-separator:"\.";
	mso-displayed-thousand-separator:"\,";}
@page
	{margin:.75in .7in .75in .7in;
	mso-header-margin:.3in;
	mso-footer-margin:.3in;}
.font0
	{color:black;
	font-size:11.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Aptos Narrow", sans-serif;
	mso-font-charset:0;}
.font5
	{color:black;
	font-size:10.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Arial Unicode MS";
	mso-generic-font-family:auto;
	mso-font-charset:0;}
tr
	{mso-height-source:auto;}
col
	{mso-width-source:auto;}
br
	{mso-data-placement:same-cell;}
td
	{padding-top:1px;
	padding-right:1px;
	padding-left:1px;
	mso-ignore:padding;
	color:black;
	font-size:11.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Aptos Narrow", sans-serif;
	mso-font-charset:0;
	mso-number-format:General;
	text-align:general;
	vertical-align:bottom;
	border:none;
	mso-background-source:auto;
	mso-pattern:auto;
	mso-protection:locked visible;
	white-space:nowrap;
	mso-rotate:0;}
.xl63
	{font-weight:700;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl64
	{text-align:left;}
.xl65
	{font-size:10.0pt;
	font-family:"Arial Unicode MS";
	mso-generic-font-family:auto;
	mso-font-charset:0;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl66
	{text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl67
	{font-style:italic;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
-->

</head>

<body link="#467886" vlink="#96607D">


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

</body>
</html>

### Twinkly: multi-color glow
<img width="758" height="131" alt="image" src="https://github.com/user-attachments/assets/70fbdef8-2027-4f39-b5b7-2476d811f9c8" /><BR>
The glow will render a multi-stop radial gradient when an effect name matches.


### Per-card icon overrides
<img width="753" height="101" alt="image" src="https://github.com/user-attachments/assets/96d69cfb-08f5-46bb-9aa5-47db3fd6d224" />


### Triggers for live updates
<img width="760" height="115" alt="image" src="https://github.com/user-attachments/assets/bfd4a838-d6c9-4a0a-b68e-bf46bf7d505e" />


## Climate Template — realistic_button_climate
Adds a big temperature and an HVAC-tinted background. Works with hvac_action or hvac_mode. Optionally read ambient from a separate sensor.
<img width="752" height="200" alt="image" src="https://github.com/user-attachments/assets/d4cada10-c44b-4f71-b223-13a0703b2aa3" />

### Variables (climate)

<html xmlns:v="urn:schemas-microsoft-com:vml"
xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:x="urn:schemas-microsoft-com:office:excel"
xmlns="http://www.w3.org/TR/REC-html40">

<head>

<meta name=ProgId content=Excel.Sheet>
<meta name=Generator content="Microsoft Excel 15">
<link id=Main-File rel=Main-File
href="file:///C:/Users/AGPEAR~1/AppData/Local/Temp/msohtmlclip1/01/clip.htm">
<link rel=File-List
href="file:///C:/Users/AGPEAR~1/AppData/Local/Temp/msohtmlclip1/01/clip_filelist.xml">
<!--table
	{mso-displayed-decimal-separator:"\.";
	mso-displayed-thousand-separator:"\,";}
@page
	{margin:.75in .7in .75in .7in;
	mso-header-margin:.3in;
	mso-footer-margin:.3in;}
.font5
	{color:black;
	font-size:10.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Arial Unicode MS";
	mso-generic-font-family:auto;
	mso-font-charset:0;}
tr
	{mso-height-source:auto;}
col
	{mso-width-source:auto;}
br
	{mso-data-placement:same-cell;}
td
	{padding-top:1px;
	padding-right:1px;
	padding-left:1px;
	mso-ignore:padding;
	color:black;
	font-size:11.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Aptos Narrow", sans-serif;
	mso-font-charset:0;
	mso-number-format:General;
	text-align:general;
	vertical-align:bottom;
	border:none;
	mso-background-source:auto;
	mso-pattern:auto;
	mso-protection:locked visible;
	white-space:nowrap;
	mso-rotate:0;}
.xl65
	{font-weight:700;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl66
	{text-align:left;}
.xl67
	{font-size:10.0pt;
	font-family:"Arial Unicode MS";
	mso-generic-font-family:auto;
	mso-font-charset:0;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl68
	{text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl69
	{font-style:italic;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
-->

</head>

<body link="#467886" vlink="#96607D">


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

</body>
</html>
The temp row uses 1fr to fill vertical space so the footer sits near the bottom.

## Fireplace Template — realistic_button_fireplace
Shows orange/red glow for low/high, with an optional animated flame (moving/flicker) glow.
### Example
<img width="749" height="267" alt="image" src="https://github.com/user-attachments/assets/027cb41f-58a6-4094-acb3-02465f58b961" /><BR>

## Variables (fireplace)

<html xmlns:v="urn:schemas-microsoft-com:vml"
xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:x="urn:schemas-microsoft-com:office:excel"
xmlns="http://www.w3.org/TR/REC-html40">

<head>

<meta name=ProgId content=Excel.Sheet>
<meta name=Generator content="Microsoft Excel 15">
<link id=Main-File rel=Main-File
href="file:///C:/Users/AGPEAR~1/AppData/Local/Temp/msohtmlclip1/01/clip.htm">
<link rel=File-List
href="file:///C:/Users/AGPEAR~1/AppData/Local/Temp/msohtmlclip1/01/clip_filelist.xml">

<!--table
	{mso-displayed-decimal-separator:"\.";
	mso-displayed-thousand-separator:"\,";}
@page
	{margin:.75in .7in .75in .7in;
	mso-header-margin:.3in;
	mso-footer-margin:.3in;}
.font0
	{color:black;
	font-size:11.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Aptos Narrow", sans-serif;
	mso-font-charset:0;}
.font5
	{color:black;
	font-size:10.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Arial Unicode MS";
	mso-generic-font-family:auto;
	mso-font-charset:0;}
tr
	{mso-height-source:auto;}
col
	{mso-width-source:auto;}
br
	{mso-data-placement:same-cell;}
td
	{padding-top:1px;
	padding-right:1px;
	padding-left:1px;
	mso-ignore:padding;
	color:black;
	font-size:11.0pt;
	font-weight:400;
	font-style:normal;
	text-decoration:none;
	font-family:"Aptos Narrow", sans-serif;
	mso-font-charset:0;
	mso-number-format:General;
	text-align:general;
	vertical-align:bottom;
	border:none;
	mso-background-source:auto;
	mso-pattern:auto;
	mso-protection:locked visible;
	white-space:nowrap;
	mso-rotate:0;}
.xl65
	{font-weight:700;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl66
	{text-align:left;}
.xl67
	{font-size:10.0pt;
	font-family:"Arial Unicode MS";
	mso-generic-font-family:auto;
	mso-font-charset:0;
	text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
.xl68
	{text-align:left;
	vertical-align:middle;
	border:.5pt solid windowtext;
	white-space:normal;}
-->

</head>

<body link="#467886" vlink="#96607D">


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

</body>
</html>

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

