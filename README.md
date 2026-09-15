# Operation Phantom Swipe
### Investigating a Cross-Border ATM & Credit-Card Fraud Ring
**Assignment 1 â€” Unit 1: Foundations of Digital Forensics**

> âš ï¸ **Academic simulation.** Every artefact in this repository is fabricated for a
> teaching exercise. All card numbers are the **publicly published network *test*
> PANs**; all names, e-mails, phone numbers, wallets, IPs and GPS points are
> fictitious. Nothing here is real data, and the tooling is provided strictly for
> lawful, educational forensic practice.

---

## 1. Author

| | |
|---|---|
| **Name** |Kartik Kumar|
| **Roll No.** | 2301730205 |
| **Course / Subject** |B.Tech CSE AIML (Section - 3) |
| **Institution** |K.R Mangalam University |
| **Submission date** |21-08-2026 |

---

## 2. Scenario

An organised ring installs **ATM skimmers** with PIN-pad overlays in New Delhi and
Dubai, **clones** the harvested cards, commits **online / card-not-present fraud**,
and **sells the stolen "dumps"** to an overseas buyer with proceeds moved in
cryptocurrency. Two exhibits were seized â€” a **skimmer** (`EXH-01`) and an
**operator's phone** (`EXH-02`) â€” and examined in this early-phase investigation.

## 3. Repository structure

```
operation-phantom-swipe/
â”œâ”€â”€ README.md                      â† you are here (overview + execution guide)
â”œâ”€â”€ AUTHORSHIP.md                  â† authorship declaration
â”œâ”€â”€ requirements.txt               â† Python deps (only for PDFs/screenshots)
â”œâ”€â”€ .github/workflows/
â”‚   â””â”€â”€ validate-structure.yml     â† CI: structure check + reproducibility
â”œâ”€â”€ docs/
â”‚   â”œâ”€â”€ 01_Cybercrime_Taxonomy_and_Legal_Mapping.md   â† Sub-problem 1
â”‚   â”œâ”€â”€ Legal_Technical_Report.pdf                     â† Sub-problem 5 (main report)
â”‚   â”œâ”€â”€ Chain_of_Custody_Form.pdf                      â† Sub-problem 2
â”‚   â””â”€â”€ Execution_Guide.md                             â† how to run everything
â”œâ”€â”€ evidence/
â”‚   â”œâ”€â”€ device01_skimmer/          â† EXH-01: tracks, config, BT pairing, firmware
â”‚   â”œâ”€â”€ device02_phone/            â† EXH-02: SMS, WhatsApp, apps, mail, media, notes
â”‚   â””â”€â”€ protected/vault.zip        â† password-protected dumps (Sub-problem 4)
â”œâ”€â”€ artefacts/
â”‚   â”œâ”€â”€ extracted_artefacts.md     â† catalogue of recovered artefacts (Sub-problem 3)
â”‚   â”œâ”€â”€ evidence_log.csv           â† machine-readable evidence log
â”‚   â””â”€â”€ recovered/                 â† files recovered AFTER cracking the vault
â”œâ”€â”€ hashes/SHA256SUMS.txt          â† SHA-256 of every acquired file
â”œâ”€â”€ logs/                          â† real run transcripts (hashing/search/cracking)
â”œâ”€â”€ screenshots/                   â† tool-usage screenshots (PNG)
â””â”€â”€ scripts/                       â† all Python/Bash tooling
    â”œâ”€â”€ generate_evidence.py  hash_files.py  search_media.py  crack_zip.py
    â”œâ”€â”€ seal_vault.sh  crack_with_john.sh  run_all.sh  validate_structure.py
    â”œâ”€â”€ make_report_pdf.py  make_coc_pdf.py  make_screenshots.py
    â””â”€â”€ wordlist.txt
```

## 4. Quick start

```bash
# Core forensic pipeline uses ONLY the Python standard library:
bash scripts/run_all.sh              # generate â†’ seal â†’ hash â†’ verify â†’ search â†’ crack

# To regenerate the PDFs and screenshots as well:
pip install -r requirements.txt
python3 scripts/make_report_pdf.py && python3 scripts/make_coc_pdf.py && python3 scripts/make_screenshots.py

# Validate the submission the same way CI does:
python3 scripts/validate_structure.py
```
See **`docs/Execution_Guide.md`** for step-by-step details and expected output.

## 5. How each sub-problem is addressed

| # | Sub-problem | Where to look |
|---|---|---|
| 1 | Cybercrime classification & legal mapping | `docs/01_Cybercrime_Taxonomy_and_Legal_Mapping.md` (IT Act 2000, IPC 1860, Budapest) + Appendix A of the report |
| 2 | Evidence collection simulation + chain of custody + SHA-256 | `scripts/generate_evidence.py`, `scripts/hash_files.py`, `hashes/SHA256SUMS.txt`, `docs/Chain_of_Custody_Form.pdf` |
| 3 | Media search & artefact extraction (5+) | `scripts/search_media.py`, `artefacts/extracted_artefacts.md`, `artefacts/evidence_log.csv`, `logs/search.log` |
| 4 | Cryptography â€” crack the protected folder | `evidence/protected/vault.zip`, `scripts/crack_zip.py`, `scripts/crack_with_john.sh`, `logs/cracking.log` |
| 5 | Legal-ethical report (4â€“6 pages) | `docs/Legal_Technical_Report.pdf` |

## 6. Mapping to the evaluation criteria (10 marks)

| Marks | Criterion | Evidence in this repo |
|---|---|---|
| 1.5 | Cybercrime taxonomy & legal mapping | `docs/01_Cybercrime_Taxonomy_and_Legal_Mapping.md` |
| 2.0 | Evidence acquisition + chain of custody | `hashes/SHA256SUMS.txt`, `logs/hashing.log`, `docs/Chain_of_Custody_Form.pdf` |
| 2.0 | File/media analysis & artefact extraction | `artefacts/`, `logs/search.log`, `screenshots/02_string_search.png` |
| 1.5 | Cryptography simulation & discussion | `logs/cracking.log`, report Â§3.2â€“3.4, `screenshots/03_password_crack.png` |
| 2.0 | Final legal-technical report quality | `docs/Legal_Technical_Report.pdf` |
| 1.0 | GitHub structure, documentation, CI | this README, `docs/Execution_Guide.md`, `.github/workflows/validate-structure.yml` |

## 7. Tools used

Python 3 standard library (`hashlib`, `zipfile`, `re`, `csv`, `struct`) Â· GNU
coreutils `sha256sum` Â· Info-ZIP `zip`/`unzip` Â· **John the Ripper / hashcat**
(reference cracking workflow in `scripts/crack_with_john.sh`) Â· **ReportLab** (PDF
typesetting) Â· **Pillow** (screenshots) Â· **GitHub Actions** (CI).

## 8. Ethics & safety

This project simulates criminal tooling only to teach lawful investigation. The
cracking utilities operate exclusively on the bundled dummy `vault.zip`. Do not use
them against data you are not authorised to access â€” unauthorised access is itself
an offence under Â§Â§43/66 of the IT Act, 2000. See report Â§3.3 for the discussion of
brute-force vs. lawful decryption requests.

## 9. Authorship declaration

See **`AUTHORSHIP.md`**. In short: this is my own original work for the course named
above; all case data is simulated; external tools are credited in Â§7.
