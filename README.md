

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
