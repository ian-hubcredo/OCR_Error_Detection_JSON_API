# OCR Detection without Error Image

## Overview

A webhook-based packaging OCR error detection workflow that returns error results as JSON without generating an annotated image. It receives a packaging image via POST webhook, uses Gemini 2.5 Pro to extract all text and detect errors, maps errors to coordinates with color-coded types, and returns the combined error data and original image as a JSON response. The image editing step is available but disabled, making this a faster, data-only version of the OCR detection pipeline.

## How It Works

```
Webhook (POST with image) -> Gemini 2.5 Pro (extract text + detect errors) -> Parse OCR output -> Extract errors with coordinates + colors -> Merge errors with original image base64 -> Combine into final JSON -> Respond to webhook
```

### Workflow Diagram

```mermaid
flowchart TD
    A["Webhook\nPOST with Image"] --> B["Gemini 2.5 Pro\nExtract Text +\nDetect Errors"]
    A --> E
    B --> C["Parse + Clean\nOCR Output"]
    C --> D["Extract Errors\nwith Coordinates"]
    D --> E["Merge\nErrors + Image"]
    E --> F["Combine\nFinal Output"]
    F --> G["Respond\nJSON"]

    style A fill:#1B3A4B,color:#fff
    style B fill:#2C5F7C,color:#fff
    style D fill:#3D5A80,color:#fff
    style G fill:#274C36,color:#fff
```

## Integrations

- **Google Gemini (2.5 Pro)** - Text extraction and error detection

## Setup

1. Import `OCR_detection_without_error_image.json` into your n8n instance.
2. Configure Google Gemini credentials.
3. Activate the workflow. Send POST requests with packaging images to the webhook URL.
