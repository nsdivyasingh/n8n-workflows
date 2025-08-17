# Slack+Reddit Workflow  

This project is an **n8n workflow** that automates the process of identifying user-reported problems with **Slack** from Reddit discussions and generating AI-powered solutions. The results are logged into a Google Sheet for tracking and analysis.  

---

## 🚀 Features  

- **Reddit Integration**:  
  Searches Reddit for posts in the `r/Slack` subreddit containing the keyword *“Why I stopped using”*.  

- **Filtering Logic**:  
  Only includes posts that:  
  - Have **≥ 2 upvotes**  
  - Contain **non-empty text content**  

- **Field Extraction**:  
  Captures the post’s:  
  - Title  
  - Body text (`selftext`)  
  - Upvotes  
  - Created date  
  - URL  

- **AI-Powered Analysis (Google Gemini)**:  
  - Uses an **AI Agent** to determine whether the post describes a *specific problem* or a *feature request*.  
  - Generates a concise **problem explanation**.  
  - If applicable, uses a **Basic LLM Chain** to suggest a **solution/plan to fix the issue in Slack**.  

- **Data Storage**:  
  - Appends the problem, metadata, and AI-generated solution into a **Google Sheet** for tracking.  

---

## ⚙️ Workflow Structure  

1. **Trigger** → Manual execution (`When clicking 'Execute workflow'`)  
2. **Reddit Node** → Searches `r/Slack` for posts with keyword filter  
3. **If Node** → Filters posts (upvotes ≥ 2 & selftext not empty)  
4. **Edit Fields** → Extracts relevant fields (title, text, upvotes, date, URL)  
5. **AI Agent (Google Gemini)** → Determines if the post is a valid problem & explains it  
6. **If1** → Checks AI output  
   - ✅ If valid problem → Generate solution with **Basic LLM Chain**  
   - ❌ Otherwise → Skip  
7. **Merge & Append to Google Sheets** → Saves Title, Problem, Date, Upvotes, URL, Solution  

---

## 📂 Files in Repo  

- `Slack+Reddit.json` → The full n8n workflow export  
- `README.md` → Documentation (this file)  
- `workflow-diagram.png` → Visual representation of the workflow (optional, from screenshot)  

---

## 🛠️ Setup Instructions  

1. **Clone Repository**  
   ```bash
   git clone https://github.com/your-username/slack-reddit-workflow.git
   cd slack-reddit-workflow
   ```

2. **Import Workflow into n8n**
- Open your n8n instance
- Go to Workflows → Import from File
- Upload Slack+Reddit.json
- Or Simply copy the code and paste it in your workflow canvas.

3. **Configure Credentials**
- Reddit API → Create OAuth2 app in Reddit Developer Console
- Google Gemini API (PaLM) → Get API key from Google AI Studio
- Google Sheets → Connect your Google account to n8n

4. **Run Workflow**
- Manually trigger or schedule executions
- Data will appear in your connected Google Sheet