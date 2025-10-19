# 🏫 AutoClassPulse  
### Automated Daily Enrollment & Teacher Reporting Workflow

AutoClassPulse is a smart automation system designed for schools to manage and monitor **daily class enrollment submissions** by teachers.  
It integrates **Google Forms**, **Google Sheets**, and **n8n workflows** to ensure accurate, timely reporting — while automatically handling **reminders**, **notifications**, and **exceptions** (like excused teachers).

---

## 🚀 Overview

AutoClassPulse eliminates manual tracking of daily class attendance/enrollment by automating every step of the workflow.

Teachers submit their daily enrollment data via a **Google Form**, which is automatically recorded in a connected **Google Sheet**.  
The system then:
- Tracks which teachers have or haven’t submitted their data for the day,
- Sends automated **reminder emails** and **WhatsApp messages** via **n8n**, and
- Issues **show-cause notifications** for teachers who remain unresponsive by the end of the day.

All logic runs in the background via **Google Apps Script** and **n8n**, ensuring reliability and zero manual effort.

---

## 🧩 Core Features

✅ **Automated Daily Blocks**  
Automatically adds a new row block every morning for all teachers, preparing the tracker for the day.

✅ **Smart Pending Detection**  
Checks the submission status of each teacher and lists pending teachers in real-time.

✅ **Excused List Integration**  
Supports a dedicated “Excused” sheet to skip teachers who are officially excused for the day.

✅ **Time-Based Automation**  
- **Morning (9:30 AM):** Sends gentle reminders to teachers who haven’t submitted.  
- **Night (10:00 PM):** Sends show-cause notices to remaining pending teachers.  
- **Night (10:30 PM):** Clears pending data for a fresh start next day.

✅ **n8n Workflow Integration**  
Uses n8n to send emails and WhatsApp notifications automatically based on pending data.

✅ 💬 **WhatsApp messages** via WhatsApp Cloud API (using phone numbers from the Google Sheet)

📞 Contact Integration:
Each teacher’s record includes name, email, and phone number for messaging and escalation workflows

✅ **Error & Lock Handling**  
Includes script locks to prevent overlapping executions and detailed logging for troubleshooting.

✅ **Customizable & Scalable**  
Easily configurable for any number of grades, teachers, or communication channels.

✅ 💬 Multi-Channel Notifications:
AutoClassPulse sends notifications:

📧 Email reminders via Gmail API

.

---

## ⚙️ System Architecture

```mermaid
flowchart TD
A[Teacher] -->|Submits Google Form| B[Google Form Responses]
B -->|Linked| C[Google Sheet - Form Responses 1]
C -->|Processed by Apps Script| D[Submission Tracker]
D -->|Non-submitted detected| E[Pending Submissions]
E -->|Webhook Trigger| F[n8n Workflow - Reminder Automation]
E -->|10 PM Daily Trigger| G[n8n Workflow - Show Cause Automation]
H[Excused List] -->|Filter Skipped Teachers| D
