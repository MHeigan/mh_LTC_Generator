# mh LTC Generator

**Professional SMPTE LTC Timecode Generator for Windows**

Converts timecode data into a bi-phase mark encoded audio signal, routable to
any audio output â€” field recorder, camera audio track, or audio interface â€” for
shot synchronisation in film, television, commercial, and gaming production.

> **Latest release: v2.0.3** - see the [Releases](https://github.com/MHeigan/mh_LTC_Generator/releases/tag/mh_LTC_Generator_v2_0_3) page to
> download.

- - -
## Features

- **Fractional-sample-accurate LTC** â€” no drift at pull-down rates (29.97, 59.94,
  47.95)
- **SMPTE ST 12-1** standard frame rates: 23.976, 24, 25, 29.97, 29.97DF, 30
- **SMPTE ST 12-3** high frame rate extension: 47.95, 48, 50, 59.94, 59.94DF, 60,
  96, 100, 120 fps _(toggle HFR rates on/off â€” keeps the UI clean for standard
  production)_
- **Configurable output level** â€” âˆ’18 to 0 dBFS slider, default âˆ’12 dBFS
- **Output channel routing** â€” Left (Ch 1), Right (Ch 2), or Both
- **NTP time-of-day sync** â€” sub-second frame alignment from pool.ntp.org
- **TC display colour** â€” Amber, Red, or Green
- **Compact mode** â€” collapses to TC display + controls, docks above the taskbar
- **Free mode** â€” 75 minutes of generation per calendar day, all features included

- - -
## Frame Rates

### Standard (visible by default)


|Label  |Rate          |Standard     |Typical Use                           |
|-------|--------------|-------------|--------------------------------------|
|23.976 |24000/1001 fps|SMPTE ST 12-1|Cinema pull-down, HD streaming        |
|24     |24.000 fps    |SMPTE ST 12-1|Digital cinema, DCP                   |
|25     |25.000 fps    |EBU / PAL    |European broadcast â€” **default**      |
|29.97  |30000/1001 fps|SMPTE ST 12-1|NTSC, non-drop frame                  |
|29.97DF|30000/1001 fps|SMPTE ST 12-1|NTSC, drop frame â€” wall-clock accurate|
|30     |30.000 fps    |SMPTE ST 12-1|Music, some North American broadcast  |

### HFR Extension (enable via "Show HFR Rates")


|Label          |Rate          |Notes                     |
|---------------|--------------|--------------------------|
|47.95          |48000/1001 fps|2Ã— pull-down              |
|48             |48.000 fps    |HFR cinema                |
|50             |50.000 fps    |PAL HFR                   |
|59.94 / 59.94DF|60000/1001 fps|NTSC HFR                  |
|60             |60.000 fps    |NTSC HFR                  |
|96             |96.000 fps    |High-speed cinema, ST 12-3|
|100            |100.000 fps   |PAL HFR, ST 12-3          |
|120            |120.000 fps   |NTSC HFR, ST 12-3         |

> **Note on HFR frame number encoding:** At frame rates of 60 fps and above, mh
> LTC Generator v2.0.3 uses standard BCD encoding. The frame counter rolls over
> at 99 rather than at the true frame count per second. The audio signal timing
> is sample-accurate at all rates. For sync reference use (e.g. Xsens mocap,
> witness cameras), the signal is fully functional. Frame-number-dependent
> workflows at 60+ fps should await a future update. See the user manual, Section
> 12.5.

- - -
## Output Level Guide


|Level   |Use                                          |
|--------|---------------------------------------------|
|âˆ’18 dBFS|EBU nominal â€” calibrated professional systems|
|âˆ’12 dBFS|Default â€” most audio interfaces and cameras  |
|0 dBFS  |**Avoid** â€” clipping corrupts LTC transitions|

- - -
## System Requirements


|Component|Requirement                        |
|---------|-----------------------------------|
|OS       |Windows 10 or Windows 11 (64-bit)  |
|Audio    |Any WASAPI-compatible output device|
|CPU      |Dual-core 2 GHz or faster          |
|RAM      |4 GB                               |
|Disk     |100 MB                             |
|Internet |Optional â€” NTP sync only           |

- - -
## Licensing


|Mode      |Limit     |Notes                                        |
|----------|----------|---------------------------------------------|
|Free      |75 min/day|All features â€” daily limit resets at midnight|
|Individual|None      |Single machine, MAC-address bound, no expiry |

To register: go to **Help â†’ Register / Licenseâ€¦** in the application. A
pre-filled email opens with your system information. Send it, and your license
file will be issued within 24 hours.

- - -
## Security

The release executable is signed with an OV code-signing certificate (Certum)
and RFC 3161 timestamped. Submitted to Microsoft WDSI prior to public release.
VirusTotal - clean scan.

- - -
## More mh_tools

[anti-matter-3d.com/tools/](https://anti-matter-3d.com/tools/)

[anti-matter-3d.com/timecode/](https://anti-matter-3d.com/timecode/)

© 2026 Martin P. Heigan. All Rights Reserved.

