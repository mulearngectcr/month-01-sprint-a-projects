# AI Resume Matcher Bot

An automated, multi-source AI recruitment automation workflow built using **n8n**, **Google Gemini**, **Google Sheets**, and **Telegram**. This system dynamically matches an uploaded resume against an active job board spreadsheet and returns the single best-matching job title with a concise reasoning summary directly back to the user via Telegram.

---

## Repository File Structure

* **`workflow.json`**: The exported n8n workflow canvas configuration (contains node logic; does not contain sensitive API credentials).
* **`Dummy.pdf`**: Sample resume file used for system testing.
* **`screenshot-workflow.jpg`**: A visual screenshot of the completed n8n canvas layout.
* **`output.jpg`**: Visual proof demonstrating a successful execution and matching result from the bot interface.
* **`configuration-spec.txt`**: Technical configuration environment setup details.
* **`README.md`**: Project documentation and architecture details.

---

## Key Features

* **Telegram Interface**: Replaces manual file triggers with a remote conversational bot, enabling mobile resume submission.
* **Secure Webhook Tunneling**: Integrates `ngrok` to bypass local networking restrictions, creating a secure HTTPS bridge for real-time Telegram event triggers.
* **Input Validation**: Includes logic routing to ensure only valid `.pdf` documents are processed by the pipeline, preventing workflow crashes from invalid message types.
* **Dynamic Job Board Retrieval**: Automatically pulls all active job openings, titles, and descriptions from a live Google Sheet using secure Google OAuth2 authorization.
* **Advanced AI Orchestration**: Utilizes n8n's Advanced AI framework (**Basic LLM Chain** paired with a **Google Gemini Chat Model**) to evaluate unstructured PDF text against global spreadsheet data in a single prompt execution.

---

## Technical Workflow Architecture

1. **Intake**: The user uploads a resume (`.pdf`) to the Telegram Bot. The **Telegram Trigger** fetches the file stream into local binary storage (`attachment_0`).
2. **Validation**: An **If** node intercepts the payload and verifies the file's MIME type is `application/pdf`. Invalid payloads are dropped.
3. **Extraction**: The **Extract from File** node parses the raw binary data into a string variable (`text`).
4. **Database Pull**: The **Google Sheets** node executes a `Get row(s)` operation with data pooling turned on (`Return All`), loading the global list of target roles into memory.
5. **AI Evaluation**: The **Basic LLM Chain** receives the resume text directly and utilizes an expression (`.all()`) to pull the full job board array from the Google Sheets node. This combined context is injected into a structured prompt evaluated by `gemini-1.5-flash`.
6. **Delivery**: A final **Telegram Action** node targets the sender's dynamic Chat ID, replying with the matching role and evaluation notes.

---

## Setup and Deployment

### 1. External Integrations

* **Telegram**: Generate an access token via `@BotFather` and initialize the chat conversation by sending `/start` to your bot.
* **Google Cloud Console**: Establish a project, enable the **Google Sheets API**, generate an OAuth Consent Screen configured for an External testing audience, and add your development profile as an authorized test account.

### 2. Local Environment Execution

Expose your local development port and inject the secure HTTPS address back into your n8n configuration framework:

```bash
# Terminal 1: Initialize the public tunnel
ngrok http 5678

# Terminal 2: Bind the environmental variable and launch n8n
set WEBHOOK_URL=https://<your-generated-id>.ngrok-free.app
npx n8n

```

Once running, import the `workflow.json` file into your n8n editor, update your credentials, turn the workflow status toggle to **Active**, and test by uploading a file.