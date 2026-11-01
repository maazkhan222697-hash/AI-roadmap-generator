AI LEARNING ROADMAP GENERATOR
==============================

ABOUT
-----
A Python + Streamlit application that uses the Groq API to create personalized
learning roadmaps. Users enter a domain, skill level, available duration, and
daily study hours. They may optionally upload a PDF or TXT file for context.

FEATURES
--------
- Beginner, Intermediate, and Advanced levels
- Learning durations from 2 weeks to 1 year
- Daily study-hour selection
- Optional PDF and TXT uploads
- AI-generated phases, topics, practice tasks, projects, milestones, and resources
- Download the roadmap as a Markdown file

FILES
-----
app.py             Main Streamlit application
requirements.txt   Required Python packages
README.txt         Setup and deployment instructions

REQUIREMENTS
------------
- Python 3.9 or newer
- Groq account and API key
- Internet connection

GET A GROQ API KEY
------------------
1. Visit https://console.groq.com/
2. Sign in and create an API key.
3. Keep it private. Never put it directly in app.py or commit it to GitHub.

RUN LOCALLY (WINDOWS)
---------------------
1. Open Command Prompt in this project folder.
2. Create a virtual environment:
   python -m venv .venv
3. Activate it:
   .venv\Scripts\activate
4. Install packages:
   pip install -r requirements.txt
5. Set your API key for this Command Prompt session:
   set GROQ_API_KEY=your_actual_groq_api_key
6. Run:
   streamlit run app.py
7. Open the local URL shown by Streamlit, usually http://localhost:8501

MODEL
-----
The default model is llama-3.3-70b-versatile. If it is unavailable to your
Groq account, choose a currently supported model in the app's sidebar.
Check https://console.groq.com/docs/models for current model availability.

DEPLOY ON STREAMLIT COMMUNITY CLOUD
-----------------------------------
1. Create a GitHub repository.
2. Upload app.py and requirements.txt (README.txt is optional).
3. Visit https://share.streamlit.io/ and sign in with GitHub.
4. Create an app and select your repository, branch, and app.py.
5. Add this secret in the app's Secrets settings:

   GROQ_API_KEY = "your_actual_groq_api_key"

6. Deploy. Never upload your API key to a public GitHub repository.

GOOGLE COLAB + CLOUDFLARE (TEMPORARY DEVELOPMENT)
-------------------------------------------------
1. Upload app.py and requirements.txt to Colab.
2. Install dependencies:
   !pip install -q -r requirements.txt
3. Enter the key securely:
   import os
   from getpass import getpass
   os.environ["GROQ_API_KEY"] = getpass("Groq API key: ")
4. Install cloudflared:
   !wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -O cloudflared
   !chmod +x cloudflared
5. Start Streamlit:
   !streamlit run app.py --server.port 8501 --server.address 0.0.0.0 &
6. In another cell, start the tunnel:
   !./cloudflared tunnel --url http://localhost:8501
7. Open the https://...trycloudflare.com URL printed in the output.

IMPORTANT: Cloudflare Quick Tunnels are temporary and intended for testing.
The Colab runtime and tunnel must remain active. The URL stops working when
the runtime or tunnel stops. Use Streamlit Community Cloud or another host
for a more dependable public deployment.

TROUBLESHOOTING
---------------
Missing API key:
- Set GROQ_API_KEY in the environment or Streamlit secrets.
- Restart the app after changing secrets.

Model error:
- Check https://console.groq.com/docs/models and select an available model
  in the app's sidebar.

PDF has no extracted text:
- Scanned/image-only PDFs may require OCR before their text can be extracted.

Rate limit or quota error:
- Check usage and limits in your Groq Console.

PRIVACY
-------
Uploaded files are used to extract text for the AI prompt. Avoid uploading
confidential or sensitive documents. Verify AI-generated resources and advice.

LICENSE
-------
Add a license file if you plan to distribute this project publicly.
