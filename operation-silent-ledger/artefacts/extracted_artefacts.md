# Extracted Artefacts - Operation Silent Ledger

_Generated 2026-08-21T19:05:44Z by `search_media.py`. Examiner: Md Umar Farooq._

Total artefacts catalogued: **24** (requirement: >= 5).

| ID | Type | Value | Source | Location | Investigative significance |
|----|------|-------|--------|----------|----------------------------|
| ART-001 | Leak / paste URL | `https://mega.io` | `evidence/device01_laptop/browser_history.txt` | line 4 | Proof-sample publication or offshore exfil destination |
| ART-002 | Leak / paste URL | `https://pastewall.example/x9f2` | `evidence/device01_laptop/browser_history.txt` | line 5 | Proof-sample publication or offshore exfil destination |
| ART-003 | Darknet leak mirror (.onion) | `leakwall7z2xj4qd.onion` | `evidence/device01_laptop/browser_history.txt` | line 6 | Threatened publication endpoint for the stolen dataset |
| ART-004 | Crypto wallet (BTC) | `1SiLentLedgerTestOnlyDummyAddr000` | `evidence/device02_phone/apps/wallet_config.json` | line 4 | Extortion ransom address - money-trail anchor |
| ART-005 | Crypto wallet (Monero) | `48SiLentLedgerTestOnlyDummyMoneroDoNotUseSi...` | `evidence/device02_phone/apps/wallet_config.json` | line 5 | Privacy-coin fallback for extortion proceeds - hard to trace |
| ART-006 | Email address | `shadowmkt@proton.example` | `evidence/device02_phone/contacts.vcf` | line 4 | Anonymous persona / victim CISO / external broker correspondence |
| ART-007 | Email address | `n1ghtjar@proton.example` | `evidence/device02_phone/contacts.vcf` | line 9 | Anonymous persona / victim CISO / external broker correspondence |
| ART-008 | Email address | `ciso@vantagecrm.example` | `evidence/device02_phone/mail/extortion_demand.eml` | line 2 | Anonymous persona / victim CISO / external broker correspondence |
| ART-009 | Originating / exit IP | `185.220.100.252` | `evidence/device02_phone/mail/extortion_demand.eml` | line 6 | Tor exit used to send the extortion e-mail - attribution lead |
| ART-010 | GPS coordinate | `12.9698,77.7500` | `evidence/device02_phone/media/photo_metadata.csv` | line 2 | Places suspect device at office (dump) / cafe (demand sent) |
| ART-011 | GPS coordinate | `12.9784,77.6408` | `evidence/device02_phone/media/photo_metadata.csv` | line 3 | Places suspect device at office (dump) / cafe (demand sent) |
| ART-012 | Anti-forensic command | `history -c` | `evidence/device01_laptop/shell_history.log` | line 2 | Deliberate destruction of evidence - relevant to mens rea |
| ART-013 | Exfiltration command | `mysqldump` | `evidence/device01_laptop/shell_history.log` | line 5 | Direct evidence of database dump / archiving / offsite upload |
| ART-014 | Exfiltration command | `tar czf` | `evidence/device01_laptop/shell_history.log` | line 7 | Direct evidence of database dump / archiving / offsite upload |
| ART-015 | Exfiltration command | `zip -e` | `evidence/device01_laptop/shell_history.log` | line 8 | Direct evidence of database dump / archiving / offsite upload |
| ART-016 | Archive password (shell) | `n1ghtjar2025` | `evidence/device01_laptop/shell_history.log` | line 8 | Password typed on the command line - opens exfil_archive.zip |
| ART-017 | Exfiltration command | `rclone` | `evidence/device01_laptop/shell_history.log` | line 9 | Direct evidence of database dump / archiving / offsite upload |
| ART-018 | Exfiltration command | `curl` | `evidence/device01_laptop/shell_history.log` | line 10 | Direct evidence of database dump / archiving / offsite upload |
| ART-019 | Anti-forensic command | `shred` | `evidence/device01_laptop/shell_history.log` | line 11 | Deliberate destruction of evidence - relevant to mens rea |
| ART-020 | Reused password (binary) | `n1ghtjar2025` | `evidence/device01_laptop/sync_agent.bin` | carved string | Same secret guards exfil_archive.zip - weak reuse enables crack |
| ART-021 | Suspect persona | `n1ghtjar` | `evidence/device01_laptop/sync_agent.bin` | carved string | Links laptop tooling to the extortion e-mail alias |
| ART-022 | Photo EXIF GPS+time | `12.9698,77.7500 @ 2025:06:18 02:31:10` | `evidence/device02_phone/media/photo_metadata.csv` | IMG_5521.jpg | Geotags suspect device at the office and cafe at the material times |
| ART-023 | Photo EXIF GPS+time | `12.9784,77.6408 @ 2025:06:20 20:03:47` | `evidence/device02_phone/media/photo_metadata.csv` | IMG_5533.jpg | Geotags suspect device at the office and cafe at the material times |
| ART-024 | Photo EXIF GPS+time | `12.9784,77.6408 @ 2025:06:20 20:12:05` | `evidence/device02_phone/media/photo_metadata.csv` | IMG_5540.jpg | Geotags suspect device at the office and cafe at the material times |

## Notes
- The archive password recovered from `sync_agent.bin` (`ARCHIVE_KEY`) is **reused** as the `exfil_archive.zip` password and typed in the shell history - see the cryptography component.
- Exfiltration commands (`mysqldump` -> `tar` -> `zip -e` -> `rclone`) reconstruct the theft end-to-end; the trailing `shred`/`history -c` show deliberate anti-forensics.
- GPS points and photo geotags corroborate the Signal/SMS timeline, placing the device at the office during the dump and at a cafe when the extortion e-mail was sent.
- Proton (Switzerland) e-mail, MEGA (offshore) storage and the crypto wallets establish the cross-border dimension even though the suspect operated domestically.
