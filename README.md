Event Management System 
1. Problem Statement 
Currently, event management within GMIT and GMU is fragmented and 
ineAicient. Students often miss out on workshops, seminars, or cultural 
fests due to a lack of a centralized notification system. The existing process 
involves manual registrations, physical ticket handling, and scattered 
information across multiple WhatsApp groups. 
Core Pain Points: 
 Information Silos: No single source of truth for all campus events. 
 Manual Overhead: Admins struggle to track participants and verify 
entries manually. 
 Verification Issues: Lack of secure, unique identification for registered 
attendees. 
 Communication Gap: DiAiculty in reaching the specific target audience 
(GMIT vs. GMU) eAectively. 
2. Objectives 
The primary goal is to build a unified Inter-Campus Event Hub that 
streamlines the lifecycle of an event. 
 Centralization: Provide a single platform for students of both 
universities to discover events. 
 Automation: Automate ticket generation using QR codes and email 
confirmations. 
 Administrative Control: Empower organizers with a dashboard to 
manage event logistics and monitor real-time participation. 
 Engagement: Increase event turnout through automated group 
notifications and easy search/filter capabilities. 
Technical Design & Implementation 
3. Proposed Solution & Architecture 
The system is built on a Client-Server Architecture using a "Model-View
Controller" (MVC) inspired approach to ensure separation of concerns. 
 User Side: A responsive interface where students can browse events 
using dynamic filters, register via a one-click process, and access a 
personal "Digital Wallet" for their QR-coded tickets. 
 Admin Side: A robust command center for creating, updating, or 
deleting events. It features a participant visualization tool to export 
attendee lists. 
 System Workflow: 1. Admin creates event → 2. Notification triggered 
to groups → 3. Student registers → 4. Python backend generates a 
unique hash → 5. QR Code & Email dispatched → 6. Admin verifies QR 
at the venue. 
4. Tech Stack & Tools 
 Frontend (HTML5, CSS3, JavaScript): Used for a lightweight, mobile-first UI. 
JavaScript handles asynchronous filtering for a smooth user 
experience. 
 Backend (Python - Flask/Django): Python was chosen for its rapid 
development capabilities and extensive libraries for QR generation 
and mail handling. 
 Database (MySQL): A relational database is used to maintain data 
integrity, especially for linking users to specific event registrations 
(Foreign Key relationships). 
 Libraries: qrcode for ticket generation, smtplib for automated 
emails, and MySQL-Connector for database operations. 
5. How It Addresses the Problem 
 Eliminates Confusion: The Search & Filter feature allows students 
to find events relevant to their specific college (GMIT or GMU) 
instantly. 
 Reduces Paperwork: The QR Code system replaces physical tickets, making 
entry verification 10x faster. 
 Increases Awareness: The Dashboard serves as a visual calendar, ensuring no 
student overlooks a deadline. 
 Ensures Accountability: Email confirmations provide students with a digital 
receipt, reducing "no-show" rates. 
Future Outlook & Context 
6. Future Scope & Roadmap 
 Phase 1 (Post-MVP): Integration of a payment gateway for paid 
workshops/fests. 
 Phase 2: An AI-based recommendation engine that suggests events 
based on a student’s previous interests or department. 
 Phase 3: In-app feedback and certificate generation logic—
automatically sending e-certificates to attendees once the admin 
marks them as "Present." 
 Scalability: Migrating the MySQL database to a cloud-hosted 
instance (like AWS RDS) to handle high-traAic spikes during major 
college fests. 
7. References & Resources 
Existing Tools & Software: 
 Eventbrite / Meetup: These professional platforms inspired the 
"Public Discovery" and "QR Check-in" workflow of this project. 
 Google Forms: While currently used by many clubs, our project 
improves on this by adding user accounts and persistent ticket 
storage, which Google Forms lacks. 
Research & Documentation: 
 OAicial Python Documentation: Referenced for implementing 
smtplib and secure password hashing (Werkzeug). 
 Database Normalization Standards: Applied 3rd Normal Form 
(3NF) to the MySQL schema to prevent data redundancy, grounded in 
standard Database Management System (DBMS) academic 
principles.

Backend :
🧑‍💻 1. Admin Creates Event (React Admin Dashboard)
The admin logs into the system (future scope: authentication).
Using the dashboard UI (built in React), they fill:
Event Name
Date & Time
Location
College (GMIT / GMU)
Description

👉 When they click “Create Event”:

A POST request is sent to backend:
POST /api/events/create

👉 Backend stores this in MongoDB

📌 Why this matters:

No more WhatsApp messages scattered everywhere
Everything is stored in one place → centralization begins here
🗄️ 2. Backend Stores Event in MongoDB
The backend (Node.js + Express) receives the request
It uses a Mongoose model (Event.js)

Example:

{
  "title": "Hackathon",
  "date": "2026-04-20",
  "college": "GMIT"
}

👉 Stored in MongoDB collection: events

📌 Why MongoDB?

Flexible (easy to add new fields later)
Fast for real-time apps
Scalable for large student data
🎓 3. Students Browse Events (React UI)
Students open the app
React fetches data:
GET /api/events
Events are displayed with:
Filters (GMIT / GMU)
Search
Categories

📌 Impact:

No confusion
No missed events
Everything visible in one dashboard
🖱️ 4. Student Clicks “Register”

When a student clicks register:

👉 Frontend sends:

POST /api/tickets/register

With:

{
  "userId": "123",
  "eventId": "456"
}
⚙️ 5. Backend Processing (MAIN LOGIC)

This is the most important part 💥

🔹 Step 1: Generate Unique ID
const uniqueId = `${userId}-${eventId}-${Date.now()}`;

👉 This ensures:

No duplicate tickets
Each student gets a unique identity
🔹 Step 2: Create QR Code
const qr = await QRCode.toDataURL(uniqueId);

👉 QR contains:

Unique ID
Acts as digital ticket
🔹 Step 3: Save Ticket in Database
{
  "userId": "123",
  "eventId": "456",
  "qrCode": "base64-image",
  "status": "Registered"
}

👉 Stored in tickets collection

📧 6. Email Sent with QR Code

Using nodemailer:

Student receives:
Event details
QR code (ticket)

📌 Why important:

Acts as digital proof
Reduces no-shows
No need for paper tickets
🎟️ 7. Admin Scans QR at Event

At event venue:

Admin uses scanner (future: mobile camera)
QR is scanned
Backend verifies:
GET /api/tickets/verify/:id

👉 If valid:

Entry allowed
Status updated → "Present"

📌 Benefit:

Fast entry (seconds)
No manual checking
No fake entries
