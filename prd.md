# Product Requirements Document (PRD)

**Product:** Email Processing Suite
**Version:** 1.3
**Platform:** Web (Client-Side)

## 1. Product Overview

The Email Processing Suite is a client-side utility designed to solve a specific data loss scenario: **Recovering email contacts after a Roundcube server migration/upgrade failure.**

When standard address book backups are unavailable, this tool allows users to reconstruct their contact database by parsing historical email logs (MBOX/ZIP exports) from their "Sent" and "Received" folders. It converts raw email headers into structured CSV data (First Name, Last Name, Email).

## 2. User User Workflow (The "Happy Path")

The user is expected to perform the following sequential actions:

1.  **Backup:** User exports `Inbox.zip` and `Sent.zip` from Roundcube webmail interface.
2.  **Extraction (Tab 1):** User uploads `Inbox.zip`. System extracts text content, stripping heavy Base64 attachments to prevent browser crashes. User downloads `inbox_clean.txt`. User repeats for `Sent.zip`.
3.  **Parsing (Tab 2):** User uploads `inbox_clean.txt`. System applies regex heuristics to find "Human <email>" patterns while blocking "noreply/bot" traffic. User downloads `inbox_contacts.csv`. User repeats for `sent_clean.txt`.
4.  **Merging (Tab 3):** User uploads `inbox_contacts.csv` AND `sent_contacts.csv`. System merges them into `master_list.csv` without removing data.
5.  **Deduping (Tab 4):** User uploads `master_list.csv`. System identifies duplicate emails and retains the entry with the highest quality metadata (Name presence). User downloads `final_recovered_contacts.csv`.

## 3. Functional Requirements

### 3.1 Tab 1: Archive Converter

- **Input:** `.zip` (containing text/eml), `.mbox`, `.txt`.
- **Processing:**
  - Utilize `JSZip` for decompression.
  - **Crucial:** Detect and remove Base64 strings (long contiguous alphanumeric blocks) to reduce file size and processing load.
- **Output:** Downloadable sanitized `.txt` file.

### 3.2 Tab 2: Intelligent Header Parser

- **Input:** Text files (from Tab 1) or raw CSV dumps.
- **Extraction Logic:**
  - Identify standard email headers (`From:`, `To:`, `Cc:`).
  - Regex extraction of `Name <email>` pairs.
- **Filtration Logic:**
  - **Technical Blocklist:** Filter domains like `amazonses.com`, `bounces.google.com`.
  - **Keyword Filter:** Filter users like `postmaster`, `mailer-daemon`, `noreply`.
  - **Artifact Cleaning:** Remove `3D`, `2E`, `mailto:` encoding artifacts common in raw dumps.
- **Output:** structured `.csv` (First Name, Family Name, Email).

### 3.3 Tab 3: Merger (Accumulator)

- **Input:** Multiple `.csv` files.
- **Logic:** Concatenate datasets.
- **Constraint:** Zero data loss. Do not deduplicate at this stage.
- **UI:** Sortable columns (A-Z).

### 3.4 Tab 4: Deduper (Finalizer)

- **Input:** Single `.csv` file.
- **Logic:**
  - Unique Key: `Email` (Case-insensitive).
  - **Conflict Resolution:** If Email X appears twice (Row A and Row B):
    - If Row A has "First Name" and Row B is empty -> Keep A.
    - If both are equal -> Keep first occurrence.
- **Output:** Final unique `.csv`.

## 4. Non-Functional Requirements

- **Privacy:** STRICT REQUIREMENT. No data transmission to external servers. All processing in-browser.
- **Capacity:** Must support input files up to ~50MB.
- **UX:** Clear status messages ("Processing...", "Found X emails").

## 5. Constraints

- Dependent on the user correctly exporting data from Roundcube.
- Cannot recover contacts that were never emailed (i.e., phone numbers stored in contacts but never used in an email thread).
