# Black Tie Customer Feedback System

A complete customer feedback loop for Black Tie Cannabis dispensaries, featuring real-time data collection and AI-powered insights.

## Overview

This project demonstrates end-to-end product thinking: identifying a business need (understanding customer preferences), designing a solution (mobile-first survey + analytics dashboard), and implementing the full data pipeline.

## Components

### Customer Survey (`index.html`)
- Mobile-first design optimized for QR code scanning
- Location tracking (Greene vs Lewiston)
- Free-text responses for authentic customer voice
- Automatic discount code delivery on completion
- Submits to Google Sheets via Apps Script

### Insights Dashboard (`insights-dashboard.html`)
- Pulls live data from Google Sheets
- AI-powered theme extraction using Claude API
- Top 10 "more of" and "less of" insights per location
- Executive summary generation
- Filter by location

## Tech Stack

- **Frontend**: Vanilla HTML/CSS/JS (zero dependencies, instant load)
- **Backend**: Google Apps Script (serverless, free)
- **Database**: Google Sheets (accessible, shareable)
- **AI**: Claude API for qualitative analysis

## Architecture

```
[QR Code] → [Survey] → [Google Sheets] → [Dashboard] → [Claude API]
                              ↓
                    [Actionable Insights]
```

## Setup

1. Create a Google Sheet with columns: `timestamp`, `location`, `moreOf`, `lessOf`
2. Add the Apps Script (see below) and deploy as web app
3. Update the script URL in `index.html`
4. Publish the Sheet as CSV and update URL in `insights-dashboard.html`
5. Host files via GitHub Pages or Netlify

### Google Apps Script

```javascript
function doGet(e) {
  const sheet = SpreadsheetApp.openById('YOUR_SHEET_ID').getActiveSheet();
  
  sheet.appendRow([
    e.parameter.timestamp || new Date().toISOString(),
    e.parameter.location || '',
    e.parameter.moreOf || '',
    e.parameter.lessOf || ''
  ]);
  
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'success' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

## Skills Demonstrated

- **Product Management**: End-to-end solution design, user journey mapping
- **Data Pipeline**: Collection → Storage → Analysis → Visualization
- **AI Integration**: Practical LLM application for business insights
- **Technical Implementation**: Full-stack development, API integration
- **Business Impact**: Direct line from customer feedback to operational improvements

## License

MIT
