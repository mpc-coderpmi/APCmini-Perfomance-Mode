# APC Mini MK1 — Performance Remote Script for Ableton Live 12

A community-made **MIDI Remote Script for the original Akai APC Mini (MK1)** that adds scoped scene launches, exclusive clip combinations, temporary fills, pattern memory, and timed A/B rotation while retaining the stock APC Mini controller and its clip LED handling.

> **MK1 only.** This script has **not been ported to the APC Mini MK2**. It relies on Ableton Live's bundled `APC_mini` Remote Script, and has been developed and iteratively tested with an original MK1 and Ableton Live 12 on Windows. This is an unofficial project, unaffiliated with Ableton or Akai.

## Features

| Controls | Result |
|---|---|
| Regular clip pads | Normal Ableton clip launch behavior |
| Right-side scene launch buttons | Launch only clips in the current 8-track Session rectangle instead of the entire Ableton scene |
| **Shift + pad(s)** | **Exclusive launch:** stop other tracks and launch the selected combination at the next quantized boundary. Also cancels rotation. |
| **Shift + scene button 7 (NOTE) + pad(s)** | **Temporary multi-clip fill:** play the selected clips, then restore the previous clips. During A/B rotation, fill starts after the current bar and rotation resumes with its next pattern afterward. |
| **Shift + scene button 6 (DRUM), hold ~1 s** | **Save** the currently playing clip combination to one in-memory slot. |
| **Shift + scene button 6 (DRUM), quick tap** | **Recall** the saved combination, queued for the next bar. |
| **Shift + scene button 6 (DRUM) + pad(s)** | **Start A/B rotation:** the currently playing clips become A; selected pads become B. Play B for 4 bars, A for 4 bars, repeat. |
| **Shift + scene button 6 (DRUM) + scene button 8 (STOP ALL)** | **Cancel rotation** without stopping the currently playing clips. |

**Scene button numbering:** Count the eight small scene buttons on the right **top to bottom**, 1–8. The bottom-right scene button is button 8. Shift is the separate bottom-right Shift key.

### Example: A/B rotation

1. Play three texture clips (pattern A).
2. Hold **Shift + 6**, tap the three pads you want in pattern B, then release button 6.
3. At the next bar, B enters for 4 bars. The script alternates A and B in 4-bar sections.
4. To leave the current sound playing and disable rotation, press **Shift + 6 + 8**. Alternatively, **Shift + pad(s)** cancels rotation and launches an exclusive new combination.
5. While rotating, **Shift + 7 + pad(s)** queues a temporary fill after the current bar; afterward the next A/B pattern resumes.

### Example: pattern memory

1. Start your main kick + bass + percussion groove.
2. Hold **Shift + 6 for approximately one second**, then release 6 to save.
3. Play another pattern.
4. Tap **Shift + 6** to recall the saved groove on the next bar.

There is **one memory slot**. Saving again overwrites it. It is **session-only**: the pattern is not retained after Ableton reloads the controller script.

## Installation (Windows)

1. Download the release ZIP and extract it.
2. Copy the **`APC_Mini_Rotation_Memory_v14_MK1`** folder (containing `__init__.py`) into the User Library's **`Remote Scripts`** folder. A typical location is:

   ```text
   C:\Users\<username>\Documents\Ableton\User Library\Remote Scripts\
   ```

   To find the configured User Library location in Live: **Settings → Library → Location of User Library**. If the `Remote Scripts` subfolder does not exist, create it. If your Live version does not detect scripts in the User Library, consult Live's Remote Script location documentation; the script must be in a directory Live scans.
3. Close and restart Ableton Live 12.
4. Open **Settings → Link, Tempo & MIDI**. Under **Control Surface**, select `APC_Mini_Rotation_Memory_v14_MK1`, then choose your APC Mini as both **Input** and **Output**.
5. Confirm the APC's pads and LEDs work before trying the custom shortcuts.

**Troubleshooting:** If the controller remains unlit, first return to a known-working script. Check the chosen control surface, input and output ports, script folder nesting, and Live's `Log.txt` (under `%APPDATA%\Ableton\Live 12...\Preferences`). Do not reset or reflash APC firmware as a first step.

## Requirements and limits

- Akai **APC Mini MK1** (not MK2).
- Ableton **Live 12** with bundled stock `APC_mini` Remote Script.
- No Max for Live devices or third-party Python packages required.
- For multi-pad gestures, **hold Shift and the corresponding scene modifier, tap one or more pads, then release the scene modifier**.
- One clip per Ableton track can play at a time. If multiple pads from one track are selected, the last selected clip wins.
- Four-bar rotation assumes a running transport. Launches are scheduled against musical song time; **Remote Script timing is not sample-accurate**, and Live/GUI load can cause late launches.
- Temporary fill return timing depends on clip lengths. For reliable fill restoration, use MIDI clips or warped audio clips with valid musical lengths; unwarped audio is unsupported for precise fills. Shorter selected fills may repeat while the longest fill completes.
- Pattern memory and rotation are **not persisted** in the Ableton set; re-establish them after reloading the script.
- Regular pad launches may cancel rotation; manual control takes priority.
- The script relies on internal API members of Ableton's bundled `APC_mini`; future Live updates could require changes.

## Contributing / MK2 roadmap

The MK2 uses different MIDI mapping and RGB feedback. **Do not install the MK1 script on an MK2.** MK2 support is a separate planned port and should be tested on real MK2 hardware before release.

If reporting a bug, include the exact Live version, operating system, steps to reproduce, selected track/clip layout, and any relevant exception from Live's `Log.txt`. Avoid sharing personal paths or sensitive project data in public reports.

## License

The **new code in this repository** is released under the MIT License (see [LICENSE](LICENSE)). Ableton Live, APC Mini and Akai are trademarks of their respective owners. No Ableton or Akai proprietary script files are redistributed here; the project imports the stock script installed with Live.
