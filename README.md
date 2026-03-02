# FOR-_TUTORS
📚 Automated Tutoring Session Organizer & Reporter
This guide explains how to set up an automated system for organizing Google Meet recordings and generating monthly tutoring reports.

This system uses two Google Apps Scripts working together:

The Sorter: Automatically moves Google Meet recordings and AI transcripts from the default folder into organized, student-specific folders.

The Reporter: Scans those transcripts at the end of the month, calculates billable/tutoring time, extracts a verbal summary you give at the end of the session, and generates professional summary documents.

Legal Disclaimer: This system involves storing and processing student data, video recordings, and transcripts. Ensure you have the appropriate GDPR, FERPA, or local privacy agreements signed by parents/guardians before implementing this workflow.

⚙️ Phase 1: Google Calendar & Meet Setup
For the scripts to recognize your files, your Google Meet sessions must be named precisely.

Create Recurring Events: Create Google Calendar events for your tutoring sessions.

Name the Event After the Student: The title of the event must start with the student's name exactly as you will type it into the script later (e.g., "JaneDoe" or "Jane").

Enable Meet Add-ons: Ensure your Google Workspace account has recording and "Gemini Notes/Transcriptions" enabled. Configure your recurring meetings to automatically record and transcribe if your tier allows it, or remember to turn them on at the start of every session.

📂 Phase 2: Google Drive Setup
Open your Google Drive.

Create a master folder to hold all your student sessions. Name it "Tutoring Sessions".

Open this new folder and look at the URL in your browser. It will look something like this:
https://drive.google.com/drive/folders/1A2b3C4d5E6f7G8h9I0jK_LMNOPQR?usp=drive_link

Copy the string of letters and numbers (e.g., 1A2b3C...). This is your Folder ID. Save it; you will need it for the script.

💻 Phase 3: Installing & Configuring the Scripts
Go to script.google.com and create a New Project.

Delete any code in the editor and paste the provided code block containing both scripts.

Save the project as "Tutoring Automation".

Variables You MUST Change:
You need to customize the code to match your specific students and folders. Use Ctrl+F (or Cmd+F) to find these specific lines in the code and update them:

For the Monthly Reporter Script:

const parentFolderId = "YOUR_FOLDER_ID_HERE";

Replace this with the Folder ID you copied in Phase 2.

const INSTRUCTOR_NAME = "Instructor";

Change "Instructor" to your name exactly as Google Meet transcribes it (e.g., "Mr. Smith" or "John").

const STUDENT_NAMES = ["Student"];

Change this to an array of your students' names as Google Meet transcribes them (e.g., ["Jane", "Tommy", "Sarah"]).

(Optional) Break Settings: If you have students who take standard mid-session breaks, you can configure BREAK_STUDENT, BREAK_MINUTES, and BREAK_THRESHOLD to automatically deduct that time from their total monthly hours.

For the Auto-Mover Script (At the bottom of the code):

const STUDENTS = ['Student1', 'Student2', 'Student3'...];

Change these to match the exact names you use in your Google Calendar event titles.

🚀 Phase 4: Activating the Automation
Once your variables are set, you need to authorize and start the scripts.

1. Turn on the Auto-Mover (Hourly):

At the top of the Apps Script editor, look for the function dropdown menu (it usually says createMonthlySummaries by default).

Change it to createTimeTrigger.

Click the Run button.

Google will ask for permissions. Click "Review permissions", choose your account, click "Advanced", and click "Go to [Project Name] (unsafe)". Allow all permissions.

Result: The script will now run silently every hour, moving any new recordings from "Meet Recordings" into Tutoring Sessions -> [Student Name] Sessions.

2. Running the Monthly Reports:

At the beginning of a new month, open your Apps Script project.

Select createMonthlySummaries from the dropdown menu and click Run.

Result: The script will scan the previous month's folders, calculate durations, find your verbal summaries, and output a "Monthly Summaries" folder containing individual student reports and a Master Report for your billing.

🎤 Pro-Tip: The "Verbal Summary" Cheat Code
The Reporter script is programmed to look for a very specific phrase in the transcript: "report report report".

When you are finishing a session with a student, say that phrase out loud to trigger the AI note-taker, followed by your summary. For example:

"Alright Jane, great job today. Report, report, report: Jane did excellent work on her quadratic equations today. We struggled a bit with factoring, so we will focus on that next week for homework."

The script will locate that exact paragraph in the transcript, extract it, and automatically place it into the student's monthly summary document for the parents to read. Keep this summary under 400 words.
