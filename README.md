# Data-Validation
Standard Operating Procedures (SOPs) for System Implementations

Standard Operating Procedure (SOP)
SOP Title: Validating and Cleaning System User Data for Onboarding

Version: 1.0
Created by: Robin Rozum
Date: 2026-01-05
Status: Draft

🎯 Objective

To ensure all system users are valid, active, and properly attributed by cleaning and verifying exported user data from core systems. This SOP supports onboarding, security audits, and operational compliance.

📍 Scope

Applies to any spreadsheet-based export from SaaS, CMMS, HRIS, or internal system logs where active personnel must be verified.

📂 Inputs
Source	Format	Key Fields
User Export	.csv	User ID, Name, Email, Status
HR Active List	.xlsx	Employee ID, Active Flag, Department
Manual Exception Log	.docx	Notes from stakeholder input
🛠 Tools Required

Microsoft Excel or Google Sheets

Power Query (optional)

SQL interface (for advanced filtering or joins)

Notion or Markdown for documentation

🔄 Procedure
Step 1: Import Data

Load the User Export into Excel

Validate that all required columns exist

Save a working copy


Step 2: Normalize Fields

Trim whitespace, fix inconsistent casing

Convert email addresses to lowercase

Ensure all user IDs are numeric or in standard UUID format


Step 3: Identify Duplicates

Use conditional formatting or COUNTIF() to detect duplicate User IDs

Tag duplicates with a "DUPLICATE" note in a new column

Step 4: Cross-Reference with HR Active List

Use VLOOKUP() or Power Query to match User ID with HR list

Add column Active in HR? with Yes/No status

Step 5: Apply Logic Rules
IF Status = 'Active' AND [Active in HR?] = 'Yes' THEN '✅ VALID'
IF Status = 'Active' AND [Active in HR?] = 'No' THEN '⚠️ REVIEW'
IF Status = 'Inactive' THEN '🗃 ARCHIVE'

Create a "Review Flag" column to summarize results

Step 6: Finalize Export

Filter out archived or invalid rows

Save final cleaned list as Validated_Users_YYYYMMDD.xlsx

Document any manual changes in Exception Log

✅ QA Checklist




📬 Outputs

Cleaned & validated user list

Exception log notes for non-matches or duplicates

🔐 Storage Path

/project_name/data_validation/validated_exports/Validated_Users_YYYYMMDD.xlsx

📜 Change Log
Version	Date	Changes	Author
1.0	2026-01-05	Initial SOP draft	Robin Rozum
🌀 Notes

This SOP is designed to support modular use in implementation consulting roles, particularly where system data is exported, cleaned, and returned to business stakeholders in a reliable format.
