# Changelog — mh LTC Generator

All notable changes to mh LTC Generator are documented here.

---

## [2.0.3] — 2026-04-28

### Fixed
- **Taskbar clearance** — window was overlapping the taskbar on all Windows configurations. Root cause: `self.height()` returns the client-area height only; `self.move()` positions the top of the window *frame*, so the bottom of the window overshot by the title-bar height (~32 px). Fixed by using `self.frameGeometry().height()` in `_center_at_bottom()`.
- **Auto-hide taskbar** — when the taskbar is set to auto-hide, `availableGeometry()` returns the full screen height. Added detection (`avail.bottom() < full.bottom()`) and a 56 px safety margin for the auto-hide case vs 8 px for a docked taskbar.

---

## [2.0.2] — 2026-04-28

### Fixed
- **Compact mode resize** — toggling Compact collapsed the controls visually but the window did not shrink. Root cause: `setFixedSize(sizeHint())` was called before Qt had processed the visibility change, so `sizeHint()` still returned the pre-hide height. Fix: release size constraints → `QApplication.processEvents()` → `adjustSize()` → `setFixedSize(self.size())`.
- **Compact separator** — the horizontal divider line above the controls panel is now stored as `self._sep` and hidden alongside `_controls_widget`, eliminating the dead grey gap that remained in compact mode.
- **Initial size lock** — `setFixedSize` is now deferred to `showEvent` (after `adjustSize()`) instead of being called at the end of `_build_ui()` before the window is visible, preventing the full expanded size from being locked in before the first show.

---

## [2.0.1] — 2026-04-28

### Added
- **TC Colour toggle** — three checkable buttons (Amber / Red / Green) in the Controls Panel let the user change the TC display colour live. Default is Amber. Has no effect on the LTC audio signal.

### Fixed
- **Window positioning** — replaced top-of-screen `showEvent` centering with `_center_at_bottom()`, positioning the window just above the taskbar on first show and after every compact toggle.
- **About dialog links** — updated to `anti-matter-3d.com/tools/` and `anti-matter-3d.com/contact/`.

---

## [2.0.0] — 2026-04-28

Complete rewrite from PyQt6 / generic dark theme to PySide6 / Dark Amber theme with HMAC licensing, a new LTC engine, and expanded feature set.

### Added
- **Dark Amber PySide6 UI** — full mh_tools standard theme (header strip, amber accent, amber version badge, dark backgrounds).
- **Fractional-sample-accurate LTC engine** — for each frame N, `samples = round(N × sr/fps) − round((N−1) × sr/fps)`. Eliminates cumulative drift at pull-down rates (29.97, 59.94, 47.95 fps). The previous engine used a fixed integer blocksize, accumulating ~20 ms of error per 83 seconds at 29.97 fps.
- **Polarity correction bit** — bit 59 for the 25/50/100 fps family; bit 27 for all other rates. Ensures each frame begins with a rising bi-phase transition. Was absent from v1.x.
- **Output level slider** — −18 to 0 dBFS, default −12 dBFS. Prevents clipping at the recorder input (full-scale ±1 was the only option in v1.x).
- **Output channel routing** — Left (Ch 1) / Right (Ch 2) / Both. Mono output with no channel selection was the only option in v1.x.
- **Sample rate selection** — 48 000 Hz (default), 44 100 Hz, 96 000 Hz.
- **HFR frame rate extension** — Show HFR Rates toggle adds 47.95, 48, 50, 59.94, 59.94DF, 60, 96, 100, 120 fps (SMPTE ST 12-3).
- **HMAC-SHA256 licensing** — INDIVIDUAL license, MAC-address bound. Seed unique to this tool (`ltcg3n_mh_vfxt00ls_2026_s3curity`, 32 bytes XOR-obfuscated). License file: `ltc_license.dat`.
- **Free mode daily cap** — 75 minutes of LTC generation per calendar day. Resets at midnight. Tracked in `%APPDATA%\mh_tools\ltcg_s.bin` (base64-encoded, no obvious extension). Countdown shown in status strip.
- **Registration mailto** — Help → Register / License… opens a pre-filled email with the machine's MAC address.
- **Compact mode** — hides the Controls Panel, repositions window just above the taskbar.
- **Status strip** — shows free-mode countdown (amber) or licensee name (green) depending on license state.
- **Three-step icon pattern** — `_set_windows_app_id()` before `QApplication`, `app.setWindowIcon()` before `MainWindow()`, `win.setWindowIcon()` after `MainWindow()`.
- **NTP sub-second alignment** — at Play with Sync to Time of Day enabled, fractional seconds are converted to the correct frame number within the current second.

### Changed
- PyQt6 → PySide6.
- Default frame rate: 30 fps → **25 fps** (EBU / PAL — appropriate for SA production).
- Audio blocksize: variable (1 block per frame) → **fixed 2048 samples** (engine generates multiple frames per callback as needed).
- Window centering: bottom-left → **bottom-centre of primary screen**.

### Removed
- Generic dark grey stylesheet (replaced by Dark Amber).
- Compact mode checkbox visibility bug from v1.x (controls were visually hidden but space was retained — now properly resizes).

---

## [1.9.4] — pre-session baseline

PyQt6 prototype. Generic dark stylesheet. Fixed-blocksize LTC engine (one frame per audio callback, integer samples, cumulative drift at pull-down rates). No polarity correction bit. No output level control. No channel routing. No licensing. No compact-mode resize.

---

*mh LTC Generator — © 2026 Martin P. Heigan — anti-matter-3d.com/tools/*
