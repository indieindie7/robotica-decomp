# Robotica / Daedalus (Sega Saturn, Genki 1995) reverse-engineering notes and symbols

Hand-named function map, review inputs and tools for the Saturn first-person shooter **Robotica** (Europe, MK-81008
V1.000; Japanese title *Daedalus*, developed by Genki for Micronet, published by Acclaim / Sega). Round 1 = one
naming pass over every function of the main program:

| Program | Functions | Hand-named | Still `provisional` |
|---|---|---|---|
| AABIOS.BIN (main program at 0x06018000) | 1,119 | 1,119 | 0 (5 review passes, done) |

0 placeholder (`FUN_`) names left.

Subsystems named: Sega GFS / CDC file system and CD access (`gfs_`, `cdc_`, `cd_`, `cdfile_`, `cdfs_`), CPK movie
playback (`movie_`), VDP1 / VDP2 (`vdp1_`, `vdp2_`, `gfx_`, `sprite_`), sound (`snd_`), maths and fixed point
(`math_`, `fp_`, `fpdec_`), memory (`mem_`), player, enemies, map and HUD (`player_`, `enemy_`, `obj_`, `map_`, `hud_`),
game / mode flow (`game_`, `sys_`).

Same method as [deadoralive-decomp](https://github.com/indieindie7/deadoralive-decomp) and
[astal-decomp](https://github.com/indieindie7/astal-decomp): functions by SH-2 prologue scan, a decompile dump cut
into slices, each slice named from its code and strings (prompt in `ghidra/naming/`), names applied as USER_DEFINED
labels; next, every provisional name is re-read with its callers by a local model (prompt in `ghidra/review/`,
verdicts applied with `tools/srprovapply.py`).
Non-commercial, done for study and preservation (early console FPS design reference).

**No game data is included**: no disc image, no executables, no decompiled C, no game text, no Ghidra database.
You need your own copy of the game to use any of this.

## What is here

| Path | Content |
|---|---|
| `NOTES.md` | disc layout, Ghidra setup, rounds, what comes next |
| `ghidra/hand_AABIOS.txt` | hand names: `0x<addr> func <name> hand <comment>` (apply with ApplyNames.java from the Scorcher / AMOK repos, hand mode) |
| `ghidra/funcinfo_AABIOS.tsv` | per-function export: `F` address name source size, `C` callees (string rows removed) |
| `ghidra/naming/prompt_ROB.txt` | the round-1 naming prompt |
| `ghidra/review/prompt_r1_rob.txt` | the provisional-review prompt |
| `ghidra/scripts/` | `FindSh2FunctionsMem.java` (SH-2 prologue scan in a raw image), `CreateAt.java`, `CsDumpAll.java` (decompile dump with headers) |
| `tools/` | `ckprovctx.py` (review contexts with callers), `srprovapply.py` (apply verdicts), `pubfuncinfo.py` (strip strings from the export) |

## Licence

Notes, names and tools: MIT (see `LICENSE`). Robotica / Daedalus belong to their rights holders; nothing from the game is distributed here.
