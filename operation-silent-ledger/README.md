# Operation Silent Ledger
### A Digital-Forensics Case Study: Insider Data Theft & Cryptocurrency Extortion

> **Academic exercise — everything here is fictitious.** The company, suspect,
> communications, wallets, IPs and "customer data" are fabricated for teaching.
> Customer records use reserved example/test domains (RFC 2606); no real personal or
> financial data is used, and no functional malware is included. See
> [`AUTHORSHIP.md`](AUTHORSHIP.md).

**Author:** Md Umar Farooq · Roll 2301730202 · B.Tech CSE (AIML), Section 3 · K.R. Mangalam University

---

## 1. The case

A senior engineer (persona **`n1ghtjar`**) at the fictional SaaS firm **Vantage CRM
Solutions Pvt. Ltd.**, Bengaluru, is suspected of copying the production customer
database (~240,000 records) and backend source code shortly before leaving the
company, sealing it in a password-protected archive, uploading it to offshore cloud
storage over Tor, and then **extorting the company's CISO for 3.5 BTC** under threat
of publishing the data on a dark-web leak site.

Two devices were seized and examined:

| Exhibit | Device | Key contents |
|---------|--------|--------------|
| **EXH-01** | Company laptop | shell history, disguised sync-job config, inert `sync_agent.bin`, browser history, staging manifest |
| **EXH-02** | Personal phone | SMS, Signal chat, contacts, installed apps, wallet config, the extortion `.eml`, photo EXIF, location history |
| **Protected** | — | `exfil_archive.zip` (ZipCrypto) holding the stolen data |

The investigation reconstructs the whole offence from these media and ties every
finding to a legal provision under Indian cyber-law.

---

## 2. Quick start

```bash
# core pipeline needs only Python 3.9+, zip/unzip and sha256sum
python3 -m pip install -r requirements.txt   # optional: only for the PDFs/screenshots
bash scripts/run_all.sh                       # rebuild & verify the entire case
```

`run_all.sh` runs all nine stages and ends with a structure/integrity check; a green
`[ALL DONE]` means the case rebuilt and verified from scratch. See
[`docs/Execution_Guide.md`](docs/Execution_Guide.md) for a stage-by-stage explanation.

---

## 3. How it maps to the grading rubric

| Rubric component | Where it is satisfied |
|------------------|-----------------------|
| **Cybercrime taxonomy + legal mapping** | [`docs/01_Cybercrime_Taxonomy_and_Legal_Mapping.md`](docs/01_Cybercrime_Taxonomy_and_Legal_Mapping.md) — taxonomy, IT Act / IPC→BNS / DPDP / CERT-In, cross-border MLAT, element-to-evidence matrix |
| **Evidence acquisition + chain of custody** | `scripts/generate_evidence.py`, `scripts/hash_files.py` → `hashes/SHA256SUMS.txt`, `logs/hashing.log`, and `docs/Chain_of_Custody_Form.pdf` |
| **File / media analysis (≥5 artefacts)** | `scripts/search_media.py` → **24 artefacts** in `artefacts/extracted_artefacts.md` + `artefacts/evidence_log.csv` |
| **Cryptography (protected evidence)** | `scripts/seal_archive.sh` (ZipCrypto) + `scripts/crack_zip.py` (dictionary attack) → `logs/cracking.log`; optional `scripts/crack_with_john.sh` |
| **Report quality** | `docs/Legal_Technical_Report.pdf` (generated, examiner metadata) |
| **GitHub structure + CI** | this `README.md`, `.github/workflows/validate-structure.yml`, `scripts/validate_structure.py` |

---

## 4. The forensic pipeline

```
generate → seal → hash → verify → search → crack → report → screenshots → validate
```

| Stage | Script | Output |
|-------|--------|--------|
| 1 | `generate_evidence.py` | simulated media in `evidence/` |
| 2 | `seal_archive.sh` | `evidence/protected/exfil_archive.zip` (plaintext deleted) |
| 3 | `hash_files.py` | `hashes/SHA256SUMS.txt`, `logs/hashing.log` |
| 4 | `sha256sum -c` | integrity verification (all `OK`) |
| 5 | `search_media.py` | `artefacts/extracted_artefacts.md`, `evidence_log.csv`, `logs/search.log` |
| 6 | `crack_zip.py` | recovered files in `artefacts/recovered/`, `logs/cracking.log` |
| 7 | `make_report_pdf.py` | `docs/Legal_Technical_Report.pdf` |
| 8 | `make_coc_pdf.py`, `make_screenshots.py` | CoC PDF + `screenshots/` |
| 9 | `validate_structure.py` | deliverable & integrity check |

### Analysis techniques demonstrated
- **Hashing & integrity** — chunked SHA-256 acquisition manifest, re-verified in CI.
- **Regex artefact search** — e-mails, BTC/XMR wallets, `.onion` mirrors, paste URLs, public IPs, GPS.
- **Command-history forensics** — exfiltration chain (`mysqldump`→`tar`→`zip -e`→`rclone`→`curl`-over-Tor) and anti-forensics (`shred`, `history -c`).
- **Binary string carving** — recovering the embedded key/persona/wallet from `sync_agent.bin`.
- **Metadata forensics** — EXIF GPS + location history corroborating the timeline.
- **Cryptanalysis** — dictionary attack exploiting a weak, **reused** ZipCrypto password.

---

## 5. Tool output (screenshots)

Acquisition hashing and integrity verification:

![Hashing](screenshots/01_hashing.png)
![Verify](screenshots/02_verify.png)

Artefact extraction and the archive crack:

![Search](screenshots/03_search.png)
![Crack](screenshots/04_crack.png)

---

## 6. Repository layout

```
operation-silent-ledger/
├── README.md · AUTHORSHIP.md · requirements.txt · .gitignore
├── .github/workflows/validate-structure.yml
├── docs/      taxonomy+legal mapping, execution guide, report PDF, CoC PDF
├── evidence/  device01_laptop/ · device02_phone/{apps,mail,media}/ · protected/
├── artefacts/ extracted_artefacts.md · evidence_log.csv · recovered/
├── hashes/    SHA256SUMS.txt
├── logs/      hashing · search · cracking
├── screenshots/
└── scripts/   generate · seal · hash · search · crack · john · run_all · validate · PDFs · screenshots · wordlist
```

---

## 7. Key finding

The suspect's operational security failed on one point that unravelled the case: the
ZipCrypto password (`n1ghtjar2025`) was **weak and reused** — it appears in the shell
history, is carved from `sync_agent.bin`, and is written in a plaintext note on the
phone. That let the examiner recover the protected archive in ~25 guesses and link the
anonymous persona to the seized hardware. The remediation is straightforward: strong,
unique passphrases and AES-256 archives, never ZipCrypto.

---

## 8. Legal summary

Indicative charges on these facts: **IT Act 2000** s.66 r/w s.43, s.66C, s.72A;
**criminal breach of trust** (s.408 IPC / s.316 BNS); **extortion** (s.384 IPC /
s.308 BNS); **criminal intimidation** (s.506 IPC / s.351 BNS); **causing
disappearance of evidence** (s.201 IPC / s.238 BNS); with **DPDP Act 2023** and
**CERT-In** obligations on the victim organisation and **MLAT / Letters Rogatory** for
the offshore artefacts. Full analysis in
[`docs/01_Cybercrime_Taxonomy_and_Legal_Mapping.md`](docs/01_Cybercrime_Taxonomy_and_Legal_Mapping.md).

---

_Prepared by **Md Umar Farooq** for academic assessment. All data fictitious._
