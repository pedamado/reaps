# Changelog

## [v1.3] - 2023-12-14

### Documentation

- Updated README and PRD to explicitly define the **Roundcube Migration Recovery** use case.
- Added step-by-step instructions for exporting MBOX/ZIP files from Roundcube.
- Defined the strict sequential workflow (Tab 1 -> 2 -> 3 -> 4) for reconstructing lost address books.

### Added

- **Column Sorting:** Added functionality to click table headers (First Name, Family Name, Email) to sort data A-Z or Z-A.
- **Dedicated Dedupe Tab:** Created a specific tab (Tab 4) for deduplication to separate concerns from the merging process.

### Changed

- **Merger Logic:** Tab 3 now acts as a strict "Stacker". It no longer removes duplicates, ensuring all source data is preserved before cleaning.
- **Deduplication Logic:** The deduplication process now runs exclusively on the "Email" column but intelligently retains the row with the most complete name information.

## [v1.2] - 2023-12-13

### Added

- **Advanced Cleaning:** Integrated robust cleaning logic to strip server artifacts (`3D`, `2E`, `mailto:`).
- **Server Filtering:** Added blocklists for internal signatures (`EX05.up.pt`) and technical domains (`amazonses`, `outlook.com`).

## [v1.1] - 2023-12-12

### Added

- **UI Framework:** Integrated Carbon Design System.
- **JSZip Integration:** Added support for processing ZIP archives directly.
