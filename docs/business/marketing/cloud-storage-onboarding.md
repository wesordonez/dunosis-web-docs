# 🌩️ Dunosis Wasabi Cloud Storage - Team Onboarding Guide

This guide will walk you through accessing and configuring our cloud storage system hosted on **Wasabi**, using a simple tool called **Cyberduck**.

> ✅ No need to create a Wasabi account — your access keys have already been created by the admin. Just follow the steps below.

---
## Overview

### 📂 What is Wasabi?

Wasabi is a secure and affordable cloud storage platform — think of it like a vault for our media files (photos, videos, designs, and more).

- 🔐 Safe and encrypted  
- 🏃‍♀️ Fast uploads/downloads  
- 📦 Used for archiving final edits and raw content

---

### 🦆 What is Cyberduck?

Cyberduck is a free app that lets you easily upload and download files to cloud storage (like Wasabi), using a clean and simple interface. It's like Google Drive, but directly connected to our long-term cloud archive.

🔗 [Download Cyberduck here](https://cyberduck.io/)

---

### 🧰 What You’ll Need

Your team admin will provide you with:

- ✅ Your **Access Key ID**
- ✅ Your **Secret Access Key** (Keep this private!)
- ✅ Your **Wasabi bucket name** (e.g., `dunosis-archive`)
- ✅ The correct **endpoint URL** (e.g., `s3.us-east-1.wasabisys.com`)

---

## 🧑‍💻 Step-by-Step: Set Up Cyberduck

1. Open **Cyberduck** and click `Open Connection` (top left).

    ![Cyberduck](./assets/du-docs-cyberduck-config.png)

2. From the dropdown, select **Amazon S3** (yes, even for Wasabi).
3. Fill in the fields:
    - **Server**: `s3.us-east-1.wasabisys.com` *(or the endpoint given to you)*
    - **Access Key ID**: *(provided by admin)*
    - **Secret Access Key**: *(provided by admin — keep private!)*
    - Leave other fields blank for now
4. Click **Connect**

    ![Cyberduck](./assets/du-docs-cyberduck-config-end.png)

5. You’ll now see our storage bucket(s). Double-click to open.

> ✅ Recommended: Click the `Add to Keychain` option to save the credentials (on Mac OS)

---

## 📁 Uploading & Downloading Files

### Uploading:
- Simply **drag & drop files** into the appropriate client folders.
- Create subfolders as needed by right-clicking.

### Downloading:
- Right-click any file → choose **Download**

⚠️ Be careful not to delete anything unless you’re 100% sure!

---

## Final Notes
- 🔐 Never share your secret access key

---
