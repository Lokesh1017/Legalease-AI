# LegalEase AI

**AI-Assisted Legal Document Generator**

LegalEase AI is a local web application that helps users create editable
legal-document drafts from structured information such as document type,
parties, terms, effective date, jurisdiction, and language.

It uses a web-based frontend, a FastAPI backend, and Google Gemini for
AI-assisted document generation. Generated documents can be edited,
copied, saved locally in the browser, and downloaded as **TXT, DOCX, or
PDF**.

> **Important:** LegalEase AI produces AI-assisted document drafts. It
> is not a law firm, does not provide legal advice, and does not
> guarantee that a generated document is legally valid or appropriate
> for a particular jurisdiction. Always review generated documents
> carefully and obtain qualified legal advice when appropriate.

------------------------------------------------------------------------

## Table of Contents

-   [What LegalEase AI Does](#what-legalease-ai-does)
-   [Main Features](#main-features)
-   [How the Application Works](#how-the-application-works)
-   [Project Structure](#project-structure)
-   [Requirements](#requirements)
-   [Installation](#installation)
-   [Gemini API Configuration](#gemini-api-configuration)
-   [Running the Application](#running-the-application)
-   [Using LegalEase AI](#using-legalease-ai)
-   [Document Generation Fields](#document-generation-fields)
-   [Generated Document Functions](#generated-document-functions)
-   [My Documents](#my-documents)
-   [Settings](#settings)
-   [Download Formats](#download-formats)
-   [Backend API](#backend-api)
-   [AI Generation Behavior](#ai-generation-behavior)
-   [Data and Storage](#data-and-storage)
-   [Security](#security)
-   [Troubleshooting](#troubleshooting)
-   [Development Notes](#development-notes)
-   [Limitations](#limitations)
-   [Future Improvements](#future-improvements)
-   [License](#license)

------------------------------------------------------------------------

## What LegalEase AI Does

LegalEase AI provides a simple workflow for creating legal-document
drafts:

1.  Choose a document type.
2.  Enter the parties involved.
3.  Describe the terms and requirements.
4.  Select the effective date.
5.  Provide the jurisdiction.
6.  Select the language.
7.  Generate the document using Google Gemini.
8.  Review and edit the generated content.
9.  Copy or save the document.
10. Download it as TXT, DOCX, or PDF.

The application is designed to make the first drafting step faster while
keeping the generated result editable and reviewable.

------------------------------------------------------------------------

## Main Features

### AI Document Generation

Generate a legal-document draft from user-provided information using
Google Gemini.

### Supported Input

The generator accepts:

-   Document type
-   Parties
-   Terms
-   Effective date
-   Jurisdiction
-   Language

### Editable Output

The generated document can be edited before downloading.

### Copy Function

Copy the generated document content for use in another application.

### Multiple Download Formats

Download generated documents as:

-   `.txt`
-   `.docx`
-   `.pdf`

### My Documents

Generated documents can be stored in the browser's local storage and
accessed later from the **My Documents** section.

### Settings

The application provides settings for:

-   Default jurisdiction
-   Default language
-   Auto-save
-   Backend connection status
-   Clearing saved documents
-   About/disclaimer information

### AI Safety-Oriented Drafting Rules

The AI prompt is designed to:

-   Avoid inventing facts supplied by the user.
-   Use visible placeholders when information is missing.
-   Organize documents into numbered sections.
-   Include relevant signature blocks.
-   Include an Important Review Notice.
-   Avoid claiming guaranteed legal validity.
-   Avoid claiming attorney review.
-   Avoid claiming jurisdictional compliance without sufficient
    information.

------------------------------------------------------------------------

## How the Application Works

The application follows this flow:

``` text
User
  |
  v
LegalEase AI Frontend
  |
  | Enter document information
  v
POST /generate
  |
  v
FastAPI Backend
  |
  v
GeminiDocumentGenerator
  |
  v
Google Gemini
  |
  v
Generated Legal Document Draft
  |
  v
Frontend Document Preview
  |
  +--> Edit
  +--> Copy
  +--> Save
  +--> Download TXT
  +--> Download DOCX
  +--> Download PDF
```

The frontend communicates with the backend at:

``` text
http://127.0.0.1:8000
```

The frontend itself runs at:

``` text
http://127.0.0.1:5500
```

------------------------------------------------------------------------

## Project Structure

The main project structure is:

``` text
LegalEaseAI/
│
├── .env
├── .gitignore
├── .venv/
├── .pytest_cache/
│
├── ai_core/
│   └── gemini_generator.py
│
├── backend/
│   ├── main.py
│   ├── routes.py
│   └── models.py
│
├── document_utils/
│
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── app.js
│
├── tests/
│
├── app.py
├── requirements.txt
└── style.css
```

### Important folders

  Folder/File                     Purpose
  ------------------------------- ------------------------------------------------
  `frontend/`                     User interface
  `frontend/index.html`           Main application page
  `frontend/style.css`            Frontend styling
  `frontend/app.js`               Frontend behavior and API interaction
  `backend/`                      FastAPI backend
  `backend/main.py`               Creates and configures the FastAPI application
  `backend/routes.py`             API endpoints and document downloads
  `backend/models.py`             Request and response data models
  `ai_core/`                      AI integration
  `ai_core/gemini_generator.py`   Gemini document-generation logic
  `document_utils/`               Document-related utilities
  `tests/`                        Project test files
  `requirements.txt`              Python dependencies
  `.env`                          Local secrets and Gemini configuration
  `.gitignore`                    Files that Git must ignore

------------------------------------------------------------------------

## Requirements

Before running LegalEase AI, install:

-   Python 3
-   Google Gemini API key
-   Git/GitHub Desktop if you want version control
-   A modern web browser

The Python packages used by the project are:

``` text
fastapi
uvicorn
python-dotenv
google-genai
python-docx
fpdf2
pydantic
```

------------------------------------------------------------------------

## Installation

### 1. Open the project folder

The project is expected at:

``` text
C:\Users\muki1\OneDrive\Documents\LegalEaseAI
```

Open PowerShell or Command Prompt and run:

``` powershell
cd "C:\Users\muki1\OneDrive\Documents\LegalEaseAI"
```

### 2. Create/activate the virtual environment

If the project already contains `.venv`, activate it.

PowerShell:

``` powershell
.\.venv\Scripts\Activate.ps1
```

If a virtual environment has not been created yet:

``` powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

``` powershell
python -m pip install -r requirements.txt
```

If needed, individual packages can be installed with:

``` powershell
python -m pip install fastapi uvicorn python-dotenv google-genai python-docx fpdf2 pydantic
```

------------------------------------------------------------------------

## Gemini API Configuration

LegalEase AI requires a Gemini API key for AI document generation.

Create or obtain your Gemini API key through Google AI Studio.

Create a local file named:

``` text
.env
```

in the project root:

``` text
LegalEaseAI/
└── .env
```

Add:

``` env
GEMINI_API_KEY=YOUR_NEW_API_KEY
GEMINI_MODEL=gemini-3.8-flash
```

Replace `YOUR_NEW_API_KEY` with your actual key.

### Never publish `.env`

The `.env` file contains a secret and must remain local.

The project's `.gitignore` contains:

``` text
.env
```

Do not:

-   Upload `.env` to GitHub.
-   Put the API key in `app.js`.
-   Put the API key in `index.html`.
-   Put the API key in a README.
-   Share the API key in screenshots.
-   Paste the API key into public source code.
-   Paste the API key into ChatGPT.

If an API key has already been exposed publicly, revoke it and create a
new key before continuing to use the project.

------------------------------------------------------------------------

## Running the Application

LegalEase AI uses two local servers:

-   Frontend: port `5500`
-   Backend: port `8000`

Both should be running while using the application.

------------------------------------------------------------------------

### Start the Backend

Open a terminal and run:

``` powershell
cd "C:\Users\muki1\OneDrive\Documents\LegalEaseAI"
python -m uvicorn backend.main:app --reload --port 8000
```

A successful startup should show something similar to:

``` text
Uvicorn running on http://127.0.0.1:8000
Application startup complete.
```

### Verify the Backend

Open:

``` text
http://127.0.0.1:8000
```

Health check:

``` text
http://127.0.0.1:8000/health
```

API documentation:

``` text
http://127.0.0.1:8000/docs
```

The health endpoint should return:

``` json
{
  "status": "ok"
}
```

------------------------------------------------------------------------

### Start the Frontend

Open a second terminal.

Run:

``` powershell
cd "C:\Users\muki1\OneDrive\Documents\LegalEaseAI\frontend"
python -m http.server 5500
```

Then open:

``` text
http://127.0.0.1:5500
```

### Important

Do not start the frontend HTTP server from the project root.

Incorrect:

``` powershell
cd "C:\Users\muki1\OneDrive\Documents\LegalEaseAI"
python -m http.server 5500
```

That displays a directory listing.

Correct:

``` powershell
cd "C:\Users\muki1\OneDrive\Documents\LegalEaseAI\frontend"
python -m http.server 5500
```

------------------------------------------------------------------------

## Using LegalEase AI

Once both servers are running:

1.  Open `http://127.0.0.1:5500`.
2.  Select **Generate Document**.
3.  Complete the form.
4.  Click the generate button.
5.  Wait for Gemini to generate the draft.
6.  Review the generated document.
7.  Edit anything that needs correction.
8.  Copy, save, or download the document.

------------------------------------------------------------------------

## Document Generation Fields

### Document Type

Specify the type of legal document you want to draft.

Example:

``` text
Non-Disclosure Agreement
```

### Parties

Enter the people or organizations involved.

Example:

``` text
Rahul Sharma and ABC Technologies Pvt. Ltd.
```

### Terms

Describe the requirements you want included.

Example:

``` text
Confidential information must not be disclosed to third parties.
The confidentiality period is 2 years.
The receiving party must use the confidential information only
for the agreed business purpose.
The receiving party must take reasonable measures to protect
the confidential information.
```

### Effective Date

Enter the date on which the document should become effective.

Example:

``` text
2026-10-06
```

### Jurisdiction

Specify the jurisdiction relevant to the document.

Example:

``` text
India
```

If the jurisdiction is not known, provide an appropriate value or leave
the application's default.

### Language

Select the desired document language.

Example:

``` text
English
```

------------------------------------------------------------------------

## Generated Document Functions

After generation, the result area provides document actions.

### Edit

The generated draft can be edited before use.

Always review:

-   Names
-   Addresses
-   Dates
-   Amounts
-   Obligations
-   Definitions
-   Governing law
-   Signatures
-   Missing placeholders

### Copy

Use the copy function to place the generated document content on the
clipboard.

### TXT

Downloads a plain-text version.

Example filename:

``` text
Non-Disclosure_Agreement.txt
```

### DOCX

Downloads an editable Microsoft Word document.

The backend formats the document using:

-   Times New Roman
-   12pt body text
-   Larger centered title
-   Paragraph spacing
-   1.5 line spacing
-   Footer

### PDF

Downloads a PDF version of the document.

The PDF includes:

-   Document title
-   Body content
-   Automatic page breaks
-   Footer

------------------------------------------------------------------------

## My Documents

The **My Documents** section provides access to previously generated
documents.

Depending on the current browser state, users can:

-   Open a document
-   Edit a document
-   Copy a document
-   Download a document
-   Delete a document

Documents are stored using browser `localStorage`.

### Important localStorage behavior

Documents are stored locally in the browser.

This means:

-   They are not automatically available on another computer.
-   They are not automatically synchronized to the cloud.
-   Clearing browser storage can remove them.
-   A different browser may not contain the same documents.

------------------------------------------------------------------------

## Settings

The **Settings** section provides application preferences and utility
functions.

### Default Jurisdiction

Set the jurisdiction that should be used as the default value.

### Default Language

Set the default generation language.

### Auto-Save

Controls the application's local document-saving behavior.

### Backend Connection Status

Helps determine whether the frontend can communicate with the backend.

The backend is expected at:

``` text
http://127.0.0.1:8000
```

### Clear All Documents

Removes saved documents from the application's browser storage.

Use this carefully because locally stored documents may not be
recoverable after clearing them.

### About / Disclaimer

Provides information about LegalEase AI and its AI-assisted nature.

------------------------------------------------------------------------

## Download Formats

LegalEase AI supports three download formats.

  Format   Use
  -------- ----------------------------------
  TXT      Simple plain-text document
  DOCX     Editable Microsoft Word document
  PDF      Printable/shareable document

The backend provides separate endpoints for these formats.

------------------------------------------------------------------------

## Backend API

The backend is built with FastAPI.

### Root

``` http
GET /
```

Provides basic backend information and links to the API documentation.

### Health

``` http
GET /health
```

Returns:

``` json
{
  "status": "ok"
}
```

### Generate Document

``` http
POST /generate
```

Request:

``` json
{
  "document_type": "Non-Disclosure Agreement",
  "parties": "Rahul Sharma and ABC Technologies Pvt. Ltd.",
  "terms": "Confidential information must not be disclosed to third parties.",
  "effective_date": "2026-10-06",
  "jurisdiction": "India",
  "language": "English"
}
```

Response contains:

``` json
{
  "content": "Generated document...",
  "document_type": "Non-Disclosure Agreement",
  "model": "..."
}
```

### Download TXT

``` http
POST /download/txt
```

### Download DOCX

``` http
POST /download/docx
```

### Download PDF

``` http
POST /download/pdf
```

------------------------------------------------------------------------

## AI Generation Behavior

The Gemini generator is implemented in:

``` text
ai_core/gemini_generator.py
```

The generator receives:

-   Document type
-   Parties
-   Terms
-   Effective date
-   Jurisdiction
-   Language

It constructs a legal-document generation prompt and sends it to Gemini.

### Information handling

The AI is instructed not to invent:

-   Names
-   Addresses
-   Amounts
-   Dates
-   Obligations
-   Facts

When information is missing, it should use visible placeholders such as:

``` text
[INSERT ADDRESS]
```

### Document organization

The generated document is instructed to include:

-   Clear title
-   Logical numbered sections
-   User-provided terms
-   Relevant signature blocks
-   Important Review Notice

### Legal disclaimer behavior

The AI is instructed not to state that:

-   The document is guaranteed to be legally valid.
-   An attorney reviewed the document.
-   The document is compliant with a jurisdiction unless the supplied
    information supports that statement.

------------------------------------------------------------------------

## Gemini Model Fallback

The configured primary model is:

``` text
gemini-3.8-flash
```

The generator also contains fallback model names:

``` text
gemini-3.7-flash
gemini-3.6-flash
gemini-3.5-flash
gemini-3.5-flash-lite
```

If a configured model fails, the generator attempts the next configured
model.

The exact availability of model names depends on the Gemini API/account
environment. If all configured models fail, the backend reports a
generation error.

------------------------------------------------------------------------

## Data and Storage

LegalEase AI currently has two separate data areas.

### AI generation

The document-generation request is sent from the frontend to the local
FastAPI backend, which calls Gemini.

### Browser documents

Saved documents are kept in browser localStorage.

There is currently no database or cloud document-storage layer described
by the current implementation.

Therefore, this project should currently be considered a **local
application**, not a multi-user cloud document-management system.

------------------------------------------------------------------------

## Security

Security is especially important because the application uses an API
key.

### `.env`

The `.env` file should contain secrets only on the local machine.

The repository's `.gitignore` includes:

``` text
.env
```

### If \`.env was accidentally published

Treat the exposed Gemini API key as compromised.

Do the following:

1.  Revoke/delete the exposed Gemini API key.
2.  Create a new Gemini API key.
3.  Remove `.env` from the project repository.
4.  Make sure `.env` is included in `.gitignore`.
5.  Clean the Git history so the old secret is no longer present in
    repository history.
6.  Publish the clean repository.
7.  Create a new local `.env`.
8.  Test the application using the new key.

Simply deleting `.env` from the latest version is not enough if the
secret exists in an earlier Git commit.

### Public repositories

Never commit secrets to a public repository.

Before publishing, check that the repository does not contain:

``` text
.env
API keys
Passwords
Tokens
Private credentials
Personal secrets
```

------------------------------------------------------------------------

## Troubleshooting

### `uvicorn` is not recognized

Use:

``` powershell
python -m pip install uvicorn
```

Then:

``` powershell
python -m uvicorn backend.main:app --reload --port 8000
```

Using `python -m uvicorn` avoids relying on a separately available
`uvicorn` command.

------------------------------------------------------------------------

### Browser shows `Directory listing for /`

You probably started the frontend server from the project root.

Stop the server:

``` text
Ctrl + C
```

Then:

``` powershell
cd "C:\Users\muki1\OneDrive\Documents\LegalEaseAI\frontend"
python -m http.server 5500
```

Open:

``` text
http://127.0.0.1:5500
```

------------------------------------------------------------------------

### Frontend cannot generate a document

Check that the backend is running:

``` text
http://127.0.0.1:8000/health
```

Expected:

``` json
{
  "status": "ok"
}
```

Then check:

``` text
http://127.0.0.1:8000/docs
```

If the backend is working but generation fails, check the Gemini
configuration and API key.

------------------------------------------------------------------------

### Gemini generation fails

Check:

1.  `.env` exists locally.
2.  `GEMINI_API_KEY` is present.
3.  The API key is valid.
4.  The configured Gemini model is available.
5.  The backend terminal for the exact error.
6.  The fallback models configured in `gemini_generator.py`.

Do not paste your API key into an issue, screenshot, or chat.

------------------------------------------------------------------------

### My Documents appears empty

Documents are stored in browser localStorage.

Possible causes:

-   Different browser.
-   Different browser profile.
-   Browser storage was cleared.
-   The document was deleted.
-   The application is being opened in a different local context.

------------------------------------------------------------------------

### Settings does not open

Make sure the current frontend JavaScript is loaded correctly and that
the frontend server is serving the latest files.

Refresh the page after restarting the frontend server.

If necessary, open the browser developer tools and check the Console for
JavaScript errors.

------------------------------------------------------------------------

### Downloads fail

Check that the backend is running.

The download endpoints are:

``` text
/download/txt
/download/docx
/download/pdf
```

Also verify that the backend dependencies are installed:

``` powershell
python -m pip install python-docx fpdf2
```

------------------------------------------------------------------------

## Development Notes

### Frontend API URL

The frontend currently communicates with:

``` javascript
const API_URL = "http://127.0.0.1:8000";
```

If the backend address or port changes, the frontend configuration must
be updated accordingly.

### Backend CORS

The current FastAPI application allows cross-origin requests for the
local frontend using permissive CORS settings.

This is convenient during development. A production deployment should
use an appropriate restricted origin configuration.

### Virtual Environment

The `.venv` directory is local development infrastructure and should not
be committed to Git.

------------------------------------------------------------------------

## Limitations

LegalEase AI currently has several important limitations.

### Not legal advice

The application generates AI-assisted drafts and does not replace a
qualified legal professional.

### No guaranteed legal validity

A generated document may require significant changes depending on:

-   Jurisdiction
-   Transaction
-   Parties
-   Industry
-   Applicable laws
-   Specific contractual requirements

### No attorney review

Generated documents are not automatically reviewed by an attorney.

### Local document storage

Documents are currently saved in browser localStorage rather than a
central database.

### No built-in user accounts

The current project does not describe a full authentication/user-account
system.

### No cloud synchronization

Documents are not automatically synchronized across devices.

### AI output can contain errors

Users must review generated documents for accuracy, completeness,
missing information, and suitability before using them.

------------------------------------------------------------------------

## Recommended User Workflow

For the best results:

1.  Choose the correct document type.
2.  Clearly identify all parties.
3.  Provide complete terms.
4.  Enter the correct effective date.
5.  Specify the appropriate jurisdiction.
6.  Select the required language.
7.  Generate the draft.
8.  Read the entire document.
9.  Replace any placeholders.
10. Check names, dates, amounts, obligations, and signatures.
11. Make required edits.
12. Download the appropriate format.
13. Obtain professional legal review when necessary.

------------------------------------------------------------------------

## Example: Non-Disclosure Agreement

Example input:

``` text
Document Type:
Non-Disclosure Agreement

Parties:
Rahul Sharma and ABC Technologies Pvt. Ltd.

Effective Date:
2026-10-06

Jurisdiction:
India

Language:
English

Terms:
Confidential information must not be disclosed to third parties.
The confidentiality period is 2 years.
The receiving party must use the confidential information only
for the agreed business purpose.
The receiving party must take reasonable measures to protect
the confidential information.
```

The generated document should then be reviewed and edited before being
used for an actual legal purpose.

------------------------------------------------------------------------

## Future Improvements

The current project can be extended with features such as:

-   User authentication
-   Database-backed document storage
-   Cloud synchronization
-   More legal-document templates
-   Document version history
-   AI document refinement
-   Better document formatting
-   Additional export formats
-   User-specific document libraries
-   Production deployment
-   More comprehensive automated tests
-   Improved jurisdiction-specific workflows
-   Professional legal review workflows

These are potential future improvements and are not necessarily part of
the current implementation.

------------------------------------------------------------------------

## License

No specific license was established in the current project information.

If this project is intended to be publicly distributed, choose and add
an appropriate open-source license before presenting it as an
open-source project.

------------------------------------------------------------------------

## Final Notes

LegalEase AI is currently best understood as a **local AI-assisted
legal-document drafting application**.

The core workflow is:

``` text
Enter information
      ↓
Generate with Gemini
      ↓
Review
      ↓
Edit
      ↓
Save / Copy
      ↓
Download
```

The most important operational rule is to keep Gemini API credentials
private and never commit `.env` to GitHub.

**LegalEase AI is an AI-assisted drafting tool, not a substitute for
qualified legal advice.**
