# Authorship & Academic Integrity Declaration

## Author

| Field | Detail |
|-------|--------|
| **Name** | Md Umar Farooq |
| **Roll No.** | 2301730202 |
| **Programme** | B.Tech CSE (AIML), Section 3 |
| **Course** | Cyber Forensics / Digital Forensics |
| **Institution** | K.R. Mangalam University |
| **Project** | Operation Silent Ledger — Insider Data Theft & Cryptocurrency Extortion |
| **Date** | 22 August 2026 |

## Declaration

I, **Md Umar Farooq**, declare that this project — the case design, the simulated
evidence, the forensic tool-chain (all scripts under `scripts/`), the written
analysis (`docs/`), and the generated report and chain-of-custody documents — is
my own original work, produced for academic assessment.

The scenario, the fictional company *Vantage CRM Solutions Pvt. Ltd.*, the suspect
persona *n1ghtjar*, and every identifier, communication, wallet address, IP address
and data record in this repository are **entirely fabricated for teaching purposes**.
No real person, organisation, system, or data set is represented.

## Safety & ethics notes

- **No real data.** All "customer records" use reserved example/test domains
  (`example.test`, `example.org`, `example.com` per RFC 2606), masked phone numbers,
  and placeholder password hashes. No personal or financial data of any real
  individual is present.
- **No functional malware or exploits.** `sync_agent.bin` is an inert data blob
  containing recoverable ASCII strings for a carving exercise; it contains no
  executable logic. The "attack" commands in the shell history are illustrative text,
  not runnable tooling.
- **Defensive/educational purpose.** The cryptography component cracks a *self-made*
  archive using a deliberately weak, reused password to teach why ZipCrypto and
  password reuse are unsafe. It is not a tool for attacking third-party data.
- **Legal analysis is educational.** The mapping to the IT Act, IPC/BNS, DPDP Act and
  CERT-In directions is for learning and is not legal advice.

## Reproducibility

Every generated artefact in this repository can be rebuilt from source with
`bash scripts/run_all.sh`, and the pipeline is re-verified on a clean machine by the
GitHub Actions workflow in `.github/workflows/`. This means the results (hashes,
extracted artefacts, cracked archive, PDFs) are demonstrably produced by the code in
this repository and not hand-assembled.

_Signed:_ Md Umar Farooq
