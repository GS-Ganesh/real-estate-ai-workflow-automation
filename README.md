# ALTRIO Mini Agentic Workflow

## Overview
Automated PDF document processing workflow that classifies, extracts, and populates structured data into Google Sheets.

## Setup Instructions

### Prerequisites
- n8n (cloud or self-hosted)
- Google Drive API credentials
- Google Sheets API credentials
- OpenAI API key

### Installation
1. Import `Altrio_Mini_Agentic_Workflow.json` into n8n
2. Configure credentials:
   - Google Drive (OAuth2)
   - Google Sheets (OAuth2)
   - OpenAI API key
3. Update Google Drive File ID in the workflow
4. Create Google Sheet with tabs: Unit Mix, Sales Comps, Lease, Logs

### Running the Workflow
1. Place PDF in Google Drive
2. Trigger workflow manually
3. Check Google Sheets for populated data

## Workflow Architecture

**Nodes:**
1. Manual Trigger
2. Google Drive → Download PDF
3. Extract from File (PDF to text)
4. Sample Pages (first 5 + last 2)
5. OpenAI Classifier
6. Parse Classification
7. OpenAI Page Selector
8. Parse Page Selection
9. Split Into Tasks
10. Filter Unit Mix / Filter Sales Comps (parallel)
11. OpenAI Extract (per task)
12. Map to Sheets format
13. Append to Google Sheets

## Results
- Unit Mix: 2 records extracted
- Sales Comps: 6 records extracted
- Processing time: ~30-60 seconds per PDF

## Trade-offs & Assumptions
- Used sampled pages (first 5 + last 2) for classification instead of full document analysis for efficiency
- Page selection is logical (page numbers) rather than physical PDF splitting
- Hardcoded file metadata for initial testing (can be dynamic with Google Drive trigger)
- Error handling logs to console (can be extended to Logs sheet)
- Used gpt-4o-mini for cost optimization on classification, gpt-4o for extraction accuracy