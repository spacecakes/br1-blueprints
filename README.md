# BeoRemote One Home Assistant blueprints

Automation blueprints that let a **Bang & Olufsen Beoremote One** control Home
Assistant through the
[`bang_olufsen`](https://www.home-assistant.io/integrations/bang_olufsen/)
integration (Mozart platform). The remote keeps working normally in standard operation; these just
listen for its key presses in Control or Light mode and act on your entities.

They take inspiration from the classic B&O light-keypad feel (brightness
presets on the digits, colour keys for moods) but extend it with modern Home
Assistant features like scene cycling, colour-temperature stepping, climate
control and arbitrary menu actions for anything else.

The remote sends keys under three namespaces. Each blueprint owns one — install
whichever you need.

| Blueprint                                            | Remote surface                     | What it does                                                                                                       |
| ---------------------------------------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [`beoremote1-light.yaml`](beoremote1-light.yaml)     | **Light** keypad                   | Brightness presets, dimming, colour-temp arrows, scenes on the colour keys (with optional scene-name notification) |
| [`beoremote1-climate.yaml`](beoremote1-climate.yaml) | **Control** keypad                 | One AC / heat pump: power, temp step + presets, fan speed, HVAC modes, Powerful/Boost, optional phone notification |
| [`beoremote1-menu.yaml`](beoremote1-menu.yaml)       | **Light** & **Control** LIST menus | Assign any action to each menu item inside the LIST menu's Control and Light sub-menus                             |

## Install

In Home Assistant: **Settings → Automations & Scenes → Blueprints → Import
Blueprint**, paste a file URL, then build an automation from it. Or use the
one-click links:

- [Lights](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fspacecakes%2Fbr1-blueprints%2Fmain%2Fbeoremote1-light.yaml)
- [Climate / AC](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fspacecakes%2Fbr1-blueprints%2Fmain%2Fbeoremote1-climate.yaml)
- [Menu functions](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fspacecakes%2Fbr1-blueprints%2Fmain%2Fbeoremote1-menu.yaml)

**Updating:** Home Assistant keeps a local copy on import. After a new version
is pushed here, open the blueprint's **⋮ → Re-import blueprint** to pull it.

## Key reference

<details>
<summary><strong>Lights</strong> — Light keypad</summary>

| Key                         | Action                                 |
| --------------------------- | -------------------------------------- |
| Select                      | Toggle                                 |
| Play / Stop                 | On / Off (Digit 0 also off)            |
| Up / Down                   | Dim ±6 %                               |
| Digit 1–9                   | Brightness 11 % … 99 %                 |
| Left / Right                | Colour temp warmer / cooler            |
| Green / Red / Yellow / Blue | Scene(s) — repeat presses cycle a list |

</details>

<details>
<summary><strong>Climate / AC</strong> — Control keypad</summary>

| Key                  | Action                                |
| -------------------- | ------------------------------------- |
| Select               | Toggle power                          |
| Play / Stop          | On / Off (Digit 0 also off)           |
| Up / Down            | Target temp ± step                    |
| Digit 1–9            | Temp presets, low → high              |
| Left / Right         | Fan speed − / +                       |
| Blue / Red / Yellow  | HVAC mode (default Cool / Heat / Dry) |
| Green                | Powerful / Boost (preset toggle)      |

Unsupported features (missing HVAC mode, no fan speeds, no boost preset) do
nothing rather than erroring.

</details>

<details>
<summary><strong>Menu functions</strong> — LIST menu</summary>

Every factory item in the Light and Control sub-menus is exposed (Morning,
Leaving, …, Window 1, Curtain 1, Doorlock, …). Assign any action to the ones you
use; the rest are ignored. Enable **Debug mode** to see the `FuncN` code each
item sends.

</details>

## Requirements

- The `bang_olufsen` integration set up with your product, and a Beoremote One paired to it.
- Phone feedback (climate, lights) needs a notify entity, e.g. from the HA companion app.

## Credits

Inspired by [cklit](https://gist.github.com/cklit)'s Beoremote One gists.
