# AI Resume Matcher

A production-ready n8n automation workflow designed to parse resumes and match candidates against open job roles using AI-driven analysis.

## Project Overview

This project automates the manual process of resume screening. It accepts a PDF resume, extracts the text, and utilizes the Google Gemini API to compare the candidate's skills against a pre-defined set of open job positions.

## Folder Structure

As seen in image_98f3ed.png, the project is organized as follows:

```text
athul-pp-ai-resume-matcher/
├── configuration-spec.txt    # Integration and mechanics documentation
├── Dummy.pdf                 # Sample resume used for testing
├── output.txt                # Resulting match output from the final node
├── README.md                 # Project documentation
├── Screenshot-workflow.jpg   # Visual map of the n8n canvas
└── workflow.json             # Exported automation blueprint

```

## Features

* **Automated Parsing:** Extracts raw text from binary PDF files using built-in n8n utilities.
* **AI-Powered Matching:** Leverages Google Gemini 1.5-flash for intelligent skill-to-job comparison.
* **Multi-Source Integration:** Combines local file input with AI-based reasoning and structured data.
* **Security-First:** Credentials are managed securely via n8n’s encrypted credential manager.

## Workflow Structure

1. **Manual Trigger:** Initiates the workflow execution.
2. **Read Binary File:** Fetches the resume from the designated secure folder.
3. **Extract from File:** Parses PDF data into processable text.
4. **Edit Fields (Set):** Defines the list of open job roles.
5. **Google Gemini:** Processes the resume against job requirements to generate matches.

## Requirements

* **n8n:** Latest version.
* **Google Gemini API Key:** Configured in n8n Credentials.
* **PDF File:** Placed in the designated `.n8n-files` directory.

## Installation & Usage

1. Import the `workflow.json` into your n8n instance.
2. Ensure your Gemini API credentials are added to the n8n Credential Manager.
3. Place your resume file in the secure `C:\Users\HP\.n8n-files\` directory.
4. Execute the workflow manually to generate the match result, which is captured in `output.txt`.

## Submission Details

* **Author:** Athul P P
* **Project Name:** AI Resume Matcher