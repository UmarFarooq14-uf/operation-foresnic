# Cybercrime Taxonomy and Legal Mapping
### Operation Silent Ledger — Insider Data Theft and Cryptocurrency Extortion

**Examiner:** Md Umar Farooq
**Exhibits:** EXH-01 (suspect laptop), EXH-02 (suspect smartphone)
**Nature of case:** Insider exfiltration of a production customer database and proprietary source code from a SaaS employer, followed by an anonymous cryptocurrency extortion demand against the company's CISO, with a threat to publish the data on the dark web.

> All names, identifiers, and data in this exercise are fictitious. Customer records use reserved example/test domains (RFC 2606) and masked values. This document maps a *simulated* fact pattern to real legal provisions for educational analysis only; it is not legal advice.

---

## 1. Factual summary

A senior engineer at the fictional firm *Vantage CRM Solutions Pvt. Ltd.* (Bengaluru), operating under the persona **n1ghtjar**, held legitimate credentials to internal systems. Shortly before his access was due to be revoked on separation, he used a service account to run a `mysqldump` of the production `customers`, `orders`, and `auth_users` tables (~240,000 records including names, e-mail addresses, phone numbers, and password hashes), together with a copy of the backend source code. He archived the data, protected it with a weak, reused password using legacy ZipCrypto, and uploaded it to personal offshore cloud storage over the Tor network. He then destroyed the local dump (`shred`) and cleared his shell history (`history -c`).

Two days later he e-mailed the company's CISO from an anonymous Proton account, routed through a Tor exit node, demanding **3.5 BTC within 72 hours** and threatening to publish the full dataset via a `.onion` leak mirror and sell it to an external broker if the deadline passed. A 100-row "proof sample" was posted to an anonymous paste site.

This single course of conduct engages several distinct offences. The taxonomy below separates them so each can be charged and proved independently.

---

## 2. Cybercrime taxonomy

Cybercrimes are conventionally classified along two axes: **(a)** whether the computer is the *target* of the crime or merely the *tool/instrument* used to commit it, and **(b)** the primary harm (confidentiality, integrity, availability, or a downstream property/person harm). Operation Silent Ledger is primarily a *computer-as-target* confidentiality breach that is then leveraged as a *computer-as-tool* property crime (extortion).

| # | Offence in this case | Taxonomic class | CIA harm | Computer as |
|---|----------------------|-----------------|----------|-------------|
| 1 | Insider data theft / exfiltration of the customer DB and source code | Data breach / IP theft by an insider | Confidentiality | Target |
| 2 | Abuse of authorised access (used valid service-account credentials for an unauthorised purpose) | Unauthorised access / access exceeding authorisation | Confidentiality, Integrity | Target |
| 3 | Criminal breach of trust (entrusted with data as an employee, dishonestly converted it) | Property crime by a fiduciary | — | Tool |
| 4 | Cyber extortion (demand for cryptocurrency under threat of publication) | Extortion / cyber-enabled coercion | — (person/property) | Tool |
| 5 | Criminal intimidation / threat to cause loss and reputational harm | Threat offence | — | Tool |
| 6 | Anti-forensic destruction of evidence (`shred`, `history -c`) | Obstruction / tampering | Integrity (of evidence) | Tool |
| 7 | Publication / threatened transfer of personal data to third parties | Data-protection breach | Confidentiality | Target |

The distinction matters for charging: the *acquisition* (rows 1–2) is complete the moment the data is copied without authority; the *extortion* (rows 4–5) is a separate, later offence that does not require the acquisition to succeed; and the *anti-forensics* (row 6) is an independent obstruction offence.

**Insider-threat characterisation.** Because the suspect began with legitimate access, this is an *insider* or *privileged-misuse* incident rather than an external intrusion. There is no firewall breach to find; the forensic signal is *behavioural* — off-hours activity, use of a service account beyond its purpose, staging and encryption of bulk data, and use of anonymity tooling (Tor, Proton, Signal, a non-custodial wallet). The evidence catalogue in `artefacts/extracted_artefacts.md` is organised around exactly these signals.

---

## 3. Legal mapping — India

India has no single "cybercrime code." Conduct is charged under a combination of the **Information Technology Act, 2000** (as amended in 2008), the general penal law (the **Indian Penal Code, 1860**, now being replaced by the **Bharatiya Nyaya Sanhita, 2023**), and sector/data-protection instruments (the **Digital Personal Data Protection Act, 2023** and **CERT-In** directions). Because the offence straddles the transition from the IPC to the BNS, both are cited below.

### 3.1 Information Technology Act, 2000

| Provision | Offence | Application to Operation Silent Ledger |
|-----------|---------|----------------------------------------|
| **s.43(b)** | Downloading/copying data from a computer resource without permission (civil liability, damages) | The `mysqldump` copy of ~240k customer records from the production database. |
| **s.43(j)** | Stealing/concealing/destroying source code | Copying the proprietary backend source; also the destruction of the local dump. |
| **s.66** | Fraudulently/dishonestly doing any act referred to in s.43 (criminal offence, up to 3 yrs / ₹5 lakh) | Elevates the s.43 acts to a criminal offence given the dishonest intent evidenced in `notes.txt` and the Signal chat. |
| **s.66C** | Identity theft — fraudulent use of another's electronic signature/password/unique ID | Use of the `svc_report` **service-account credentials** to access data for an unauthorised purpose. |
| **s.66D** | Cheating by personation using a computer resource | Arguable for the anonymous persona used to pressure the victim; more squarely an extortion matter (see IPC/BNS). |
| **s.72A** | Disclosure of personal information in breach of a lawful contract | The threatened/actual disclosure of customers' personal data obtained under his employment contract. |
| **s.43A** | Failure of a body corporate to protect sensitive personal data (civil, on the *company*) | Relevant to *Vantage's* own exposure — a reminder that the victim entity may also face liability, which shapes disclosure/reporting decisions. |
| **s.65** | Tampering with computer source documents required to be kept | Supports the source-code and anti-forensic dimensions where records were altered/destroyed. |

### 3.2 General penal law — IPC 1860 → BNS 2023

| IPC (1860) | BNS (2023) equivalent | Offence | Application |
|------------|-----------------------|---------|-------------|
| **s.408** | **s.316(4)** | Criminal breach of trust by clerk/servant | Core charge: as an employee entrusted with access to the data, he dishonestly misappropriated it. |
| **s.378 / 379** | **s.303 / 305** | Theft (of data/property) | The taking of the database and source code; charged in the alternative/together with breach of trust. |
| **s.383–384** | **s.308** | Extortion | The 3.5 BTC demand under threat of publication — the definitional core of the case. |
| **s.503 / 506** | **s.351** | Criminal intimidation | The threat to cause loss, reputational damage, and publish customer data to coerce payment. |
| **s.201** | **s.238** | Causing disappearance of evidence | The `shred` of the dump and `history -c` clearing of the shell history. |

**Why both breach-of-trust *and* extortion?** They protect different interests and complete at different moments. Criminal breach of trust (s.408 IPC / s.316 BNS) addresses the *misappropriation* of entrusted property and is complete at exfiltration. Extortion (s.384 IPC / s.308 BNS) addresses the *coercive demand* and is complete when the threat is made with intent to obtain property, whether or not any BTC is ever paid. Charging both captures the full criminality; charging only one would leave a gap.

### 3.3 Data protection — DPDP Act, 2023

The customer records are "personal data" and the company is a "Data Fiduciary" under the **Digital Personal Data Protection Act, 2023**. The Act principally regulates the *fiduciary's* obligations rather than criminalising the thief, but it is directly relevant here in three ways: (i) the breach triggers the fiduciary's **notification** duties to the Data Protection Board and affected Data Principals; (ii) it sharpens the harm analysis, because the exposed data enables downstream fraud against 240,000 individuals; and (iii) it interacts with **s.43A / s.72A** of the IT Act on the company's own security-safeguards liability. For the *suspect*, the DPDP Act reinforces that the data was legally protected and that its disclosure was unlawful.

### 3.4 Mandatory incident reporting — CERT-In Directions, 2022

Under the **CERT-In directions of 28 April 2022** (issued under s.70B(6) of the IT Act), the victim organisation must report specified cyber incidents — including **data breaches and unauthorised access** — to CERT-In **within 6 hours** of becoming aware of them, and must retain logs for 180 days. This is why acquisition timing and log preservation matter to the investigation: the organisation's own compliance clock starts at detection, and the ICT logs it is obliged to keep (VPN, database access, mail gateway) are precisely the corroborating evidence an examiner will request.

---

## 4. Cross-border dimension

Although the suspect operated physically within India, the *instrumentalities* are deliberately international, which is typical of modern cyber-extortion:

- **Anonymous e-mail** via Proton (servers in Switzerland).
- **Offshore cloud storage** (MEGA) holding the exfiltrated archive.
- **Tor** routing, so the originating IP resolves to an exit node abroad (`185.220.100.252` in the evidence).
- **Cryptocurrency** (BTC, with Monero as a trace-resistant fallback) as the payment rail.
- A **`.onion` leak mirror** as the publication threat.

Obtaining subscriber records, server contents, or wallet-exchange KYC from these providers requires **international cooperation**. India pursues this primarily through **Mutual Legal Assistance Treaties (MLATs)** and **Letters Rogatory** issued by a competent court. The **Budapest Convention on Cybercrime (2001)** is the leading multilateral framework for such cooperation and for harmonising offences — its Articles on illegal access (Art. 2), data interference (Art. 4), system interference (Art. 5), misuse of devices (Art. 6), and computer-related fraud (Art. 8) map closely onto the acts here. **India is not a party** to the Budapest Convention, so cooperation typically proceeds bilaterally (MLAT/Letters Rogatory) and through provider-specific lawful-disclosure channels, which is slower and shapes realistic investigative expectations.

The practical lesson for the examiner: preserve everything domestically and immediately (the two seized exhibits, the company's server-side logs), because the offshore artefacts may take months to obtain, if at all — and Monero may not be traceable at all.

---

## 5. Elements-to-evidence matrix

The value of the taxonomy is that each legal element can be tied to a concrete artefact recovered in this exercise (see `artefacts/extracted_artefacts.md` for the full catalogue with IDs).

| Legal element to prove | Evidence in this case | Where |
|------------------------|-----------------------|-------|
| Unauthorised copying of data (s.43/66 IT Act) | `mysqldump` of customer tables to a hidden path | `shell_history.log` |
| Dishonest intent / mens rea (breach of trust, extortion) | "PLAN (delete this)" note; Signal negotiation with a broker | `notes.txt`, `signal_chat.txt` |
| Identity/credential misuse (s.66C) | Use of `svc_report` service account off-hours | `shell_history.log` |
| Encryption to conceal (relevant to concealment) | `zip -e -P` with a reused weak key; ZipCrypto archive | `shell_history.log`, `exfil_archive.zip` |
| The extortion demand (s.384 IPC / s.308 BNS) | E-mail demanding 3.5 BTC in 72h under threat | `extortion_demand.eml` |
| Criminal intimidation (s.506 IPC / s.351 BNS) | Threat to publish + "do not involve the police" | `extortion_demand.eml` |
| Attribution linking persona to suspect | `PERSONA=n1ghtjar` and wallet carved from the agent binary; wallet config | `sync_agent.bin`, `wallet_config.json` |
| Anti-forensics (s.201 IPC / s.238 BNS) | `shred` of the dump; `history -c` | `shell_history.log` |
| Corroborating location/time | Geotagged photos + location history at office (dump) and café (demand) | `photo_metadata.csv`, `location_history.json` |
| Money trail | BTC/XMR addresses; broker split | `wallet_config.json`, `signal_chat.txt` |

---

## 6. Summary of charges (indicative)

On these simulated facts, a charge sheet would plausibly allege, cumulatively: **s.66 r/w s.43** and **s.66C** and **s.72A** of the IT Act, 2000; **criminal breach of trust** (s.408 IPC / s.316 BNS), **extortion** (s.384 IPC / s.308 BNS), **criminal intimidation** (s.506 IPC / s.351 BNS), and **causing disappearance of evidence** (s.201 IPC / s.238 BNS); with **DPDP Act, 2023** and **CERT-In** obligations engaging the victim organisation. The cross-border artefacts would be pursued via **MLAT / Letters Rogatory**.

The remainder of the project demonstrates, with a reproducible tool-chain, how each evidentiary item above was acquired, hash-sealed, searched, and (for the protected archive) recovered — so that the legal conclusions rest on a defensible chain of custody.
