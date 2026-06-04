# ShadeSense AI

An Agentic AI Beauty Analysis System built using **n8n**, **Gemini Vision**, **Groq LLMs**, **Google Sheets**, **Gmail**, and **PDF generation**.

ShadeSense analyzes a user's face image and generates personalized beauty recommendations including skin tone analysis, seasonal color palettes, makeup guidance, product recommendations, and a final beauty report.

---

## Features

### Face Analysis using Vision AI

* Upload facial image through a webhook.
* Gemini Vision extracts:

  * Skin tone
  * Undertone
  * Face shape
  * Skin type
  * Visible facial features

### Multi-Agent Architecture

The workflow uses specialized AI agents:

#### Color Palette Agent

Generates:

* Seasonal color palette
* Recommended colors
* Colors to avoid

#### Product Match Agent

Generates:

* Foundation recommendations
* Concealer recommendations
* Blush recommendations
* Lipstick recommendations
* Suggested beauty products

#### Makeup Placement Agent

Generates:

* Blush placement guidance
* Bronzer placement guidance
* Contour placement guidance
* Highlighter placement guidance
* Personalized makeup tips

#### Final Beauty Report Agent

Combines outputs from all agents and creates:

* Beauty summary
* Best colors
* Makeup recommendations
* Product recommendations
* Beauty tips
* Confidence score
* Confidence explanation

---

## Architecture

```text
Image Upload
      │
      ▼
Webhook
      │
      ▼
Image → Base64 Conversion
      │
      ▼
Gemini Vision Feature Extraction
      │
      ├──────────────┬──────────────┬
      ▼              ▼              ▼
Color Agent    Product Agent   Makeup Agent
      │              │              │
      └───────Merge Outputs─────────┘
                     │
                     ▼
          Final Report Generator
                     │
                     ▼
           Confidence Evaluation
                     │
      ┌──────────────┴──────────────┐
      ▼                             ▼
Confidence ≥ 70            Confidence < 70
      │                             │
Auto Approval              Human Review
      │                             │
Google Sheets              Review Email
PDF Generation             Pending Status
Email Delivery             Webhook Response
```

---

## Agentic AI Design

ShadeSense follows an agentic architecture by decomposing a complex beauty consultation task into specialized AI roles.

| Agent                    | Responsibility                       |
| ------------------------ | ------------------------------------ |
| Feature Extraction Agent | Extract facial attributes from image |
| Color Palette Agent      | Determine seasonal palette           |
| Product Match Agent      | Recommend products and shades        |
| Makeup Placement Agent   | Suggest makeup application strategy  |
| Final Report Agent       | Review and generate final report     |

---

## Human-in-the-Loop

The workflow includes a confidence-based approval mechanism.

### Case 1: Confidence ≥ 70

The report is automatically approved.

Actions:

* Status updated to **Approved**
* Stored in Google Sheets
* PDF report generated
* Report emailed to user

### Case 2: Confidence < 70

The report requires human review.

Actions:

* Status marked as **Pending Review**
* Review email sent
* User receives review-required response
* Human reviewer validates recommendations before delivery

---

## Technologies Used

### Workflow Orchestration

* n8n

### AI Models

* Gemini 2.5 Flash Vision
* Groq Llama 3.3 70B Versatile

### Integrations

* Google Sheets
* Gmail
* PDFBolt

### Programming

* JavaScript
* JSON

---

## Data Storage

Analysis results are logged into Google Sheets, including:

* Timestamp
* Skin Tone
* Undertone
* Face Shape
* Skin Type
* Season
* Foundation Family
* Summary
* Approval Status

---

## PDF Report Generation

Approved reports are automatically converted into professional PDF reports containing:

* Personalized beauty summary
* Color palette recommendations
* Makeup recommendations
* Product suggestions
* Beauty tips
* Confidence analysis

---

## API Usage

### Test Webhook

```bash
curl -X POST \
-F "image=@face.jpg" \
http://localhost:5678/webhook-test/beauty-analysis
```

### Successful Response

```json
{
  "success": true,
  "status": "Approved"
}
```

### Human Review Required

```json
{
  "success": true,
  "status": "PENDING_REVIEW",
  "confidence": 64,
  "message": "Human review required"
}
```

---

## Key Highlights

* Multi-Agent AI System
* Vision-based Face Analysis
* Confidence-based Decision Making
* Human-in-the-Loop Validation
* Automated PDF Report Generation
* Google Sheets Logging
* Email Notifications
* End-to-End Workflow Automation

---

## Contributors

* Ishita Khot
* Sheza Mishal

---

## Future Enhancements

* Interactive review dashboard
* Beauty product price comparison
* Skin concern detection
* Hairstyle recommendations
* Multi-image analysis
* Real-time beauty assistant chatbot
