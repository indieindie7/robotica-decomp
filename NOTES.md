# Robotica (Saturn) decomp notes

## Disc
- Europe release MK-81008 V1.000 (1995-08-09), 2 tracks; data track 39 files.
- Main program `AABIOS.BIN` (946,176 bytes) loads at 0x06018000 (IP first read address). No other SH-2 code on the disc.
- Data: `STAGEnn.BIN` / `STAGEnnT.BIN` per floor (pointers into low work RAM 0x00200000-0x002fffff), sound banks and a sound map, title picture, the 68000 sound driver, CPK movies.

## Ghidra
- Import AABIOS.BIN as SH-2 big-endian (SuperH:BE:32:SH-2) at 0x06018000, no auto-analysis of data.
- `FindSh2FunctionsMem.java` prologue scan + `CreateAt.java`: 1,119 functions. `CsDumpAll.java` writes the decompile dump.

## Rounds
- Round 1 (2026-10-28): dump cut into 8 slices of 140 functions, each named by a Sonnet agent from `ghidra/naming/prompt_ROB.txt`; 1,119 names, 685 marked provisional, 6 duplicate names suffixed `_2`. Applied: 0 `FUN_` left.
- Review (pending): `ckprovctx.py` builds review contexts (function + up to 3 callers) for the 685 provisional names; a local model rules CONFIRM / RENAME / UNSURE per entry with `ghidra/review/prompt_r1_rob.txt`.

## Next
- Apply review verdicts, round 2 on the UNSURE rest, then structs / globals for the stage loader and player / enemy objects.
