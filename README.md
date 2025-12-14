# REAPS – Roundcube Email Addresses Processing Suite v1.3

A privacy-focused web application designed to recover, clean, and organize email contacts from received and sent email messages.

## ⚠️ Important Note: Use Case

**This tool is specifically designed for disaster recovery.**
It is intended for users who have lost their address books during a migration or upgrade of their **Roundcube** email server and did not have a backup of their contacts.

This suite allows you to reconstruct your contact list by extracting email addresses directly from your **Sent** and **Received** email history (MBOX/ZIP backups).

## 🚀 Features

- **100% Client-Side:** Data never leaves your computer.
- **Archive Converter:** Extracts text from `.zip` and `.mbox` files, removing attachments.
- **Intelligent Parsing:** Extracts "human" emails while ignoring system notifications.
- **Sequential Workflow:** Clean, Parse, Merge, and Deduplicate in steps.

## 📋 Prerequisites: Backing up Roundcube

Before using this tool, you need to export your email history from Roundcube to your local disk.

1.  Log in to your **Roundcube** webmail.
2.  Go to your **Inbox**.
3.  Select all messages (or select specific pages of messages).
    - _Tip:_ You may need to scroll down or increase the "Messages per page" in Settings > Preferences > Mailbox View to select more at once.
4.  Click the **More** button (often represented by `...` or a generic icon) in the toolbar.
5.  Select **Download** or **Export**.
    - If available, choose **MBOX** format.
    - If MBOX is not an option, it may download as a **.zip** file containing `.eml` files. Both work with this tool.
6.  **Repeat this process** for your **Sent** folder (crucial for capturing people you have emailed).
7.  Save these files to a known folder on your computer.

## 📖 Step-by-Step Recovery Guide

Follow these tabs in order to reconstruct your contact list.

### Step 1: Extract Data (Tab 1)

**Goal:** Convert your Roundcube backups into readable text.

1.  Go to the **MBOX/ZIP** tab.
2.  Drag and drop your Roundcube backup file (e.g., `Inbox.zip` or `Sent.mbox`).
3.  Wait for processing.
4.  Click **Download Text**.
5.  _Repeat this for every backup file you have (Inbox, Sent, etc.)._

### Step 2: Parse Contacts (Tab 2)

**Goal:** Extract names and emails from the text files created in Step 1.

1.  Go to the **Header Parser** tab.
2.  Upload one of the text files you just downloaded in Step 1.
3.  The tool will extract valid contacts and remove "mailer-daemon" or technical junk.
4.  Click **Download CSV**.
5.  _Repeat this for every text file from Step 1._

### Step 3: Merge Lists (Tab 3)

**Goal:** Combine the separate CSV lists (Inbox contacts, Sent contacts) into one master file.

1.  Go to the **Merger** tab.
2.  Select **ALL** the CSV files you created in Step 2.
3.  The tool will stack them into one massive list (keeping all duplicates for safety).
4.  Click **Download Merged CSV**.

### Step 4: Finalize & Dedupe (Tab 4)

**Goal:** Create the final, clean contact list.

1.  Go to the **CSV Deduper** tab.
2.  Upload the **Merged CSV** from Step 3.
3.  The tool will remove duplicate email addresses.
    - _Note:_ It automatically prioritizes entries that have a Full Name over entries that only have an email address.
4.  Click **Download Clean CSV**.

**Result:** You now have a restored contact list ready for import into your new email system.

## 🛠 Technologies

- **HTML5 / CSS3**
- **JavaScript (Vanilla ES6+)**
- **Carbon Design System**
- **JSZip**

## 📄 License

This project is licensed under the **MIT License**.

Copyright (c) 2023 [Your Name / Organization]

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
