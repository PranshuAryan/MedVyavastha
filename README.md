📌 The Problem When an ambulance rushes a critical patient to a hospital, the emergency room often has zero information until the patient physically walks through the door. Beds aren't prepared. Equipment isn't ready. Specialists aren't alerted. MedVyavastha eliminates that gap.

💡 What is MedVyavastha? MedVyavastha is a real-time healthcare coordination platform that bridges the critical information gap between ambulances and hospitals during emergency transit. By transmitting patient data to the receiving hospital while the patient is still en route, we give medical teams the time they need to prepare life-saving interventions in advance — turning reactive emergency care into proactive emergency care.

🚀 Key Features FeatureDescription🤖 Med AI — Emergency AssistantDescribe your symptoms in plain language; AI instantly identifies the emergency type, recommends the right hospital category, provides step-by-step first aid, and shows matching hospitals below📡 Real-time Transit MonitoringTracks emergency vehicles and pushes live ETA updates directly to hospital staff🩺 Pre-Arrival Patient DataSecurely transmits vital signs and medical history to the ER before the ambulance arrives🛏️ Dynamic Resource AllocationHospitals can manage bed availability and specialized equipment based on incoming emergency data📊 Unified DashboardHigh-contrast, minimalist interface for monitoring multiple incoming emergencies simultaneously🔍 Hospital FinderGPS-powered search to locate the nearest available hospitals with live bed & ICU counts🏥 Hospital PortalDedicated interface for hospitals to update real-time resource availability

🛠️ Tech Stack Frontend → HTML5, CSS3, Vanilla JavaScript Backend → Firebase Firestore (Real-time Database) Auth → Firebase Authentication AI → Claude API (Anthropic) — Med AI Emergency Assistant Hosting → Netlify (Auto-deploy on git push, global CDN) Reports → PptxGenJS (Automated medical report generation) Maps → Google Maps Embed API, Nominatim (OpenStreetMap)

🤖 Med AI — Emergency Assistant

"Describe symptoms — AI will find the right hospital type for you instantly."

Med AI is MedVyavastha's built-in emergency intelligence layer, accessible directly from the home page. It removes the panic-driven guesswork of figuring out which hospital to go to during a crisis. How it works:

Describe the emergency — User types symptoms in plain language (e.g. "chest pain and shortness of breath") AI analyses the emergency — Instantly classifies the emergency type and identifies the right hospital speciality needed First Aid guidance — Provides a clear checklist of what to do right now and what NOT to do, with an important safety note Matching hospitals surface — The FindHospital section automatically filters to show hospitals equipped for that specific emergency

Why it matters: In a real emergency, people freeze. Med AI gives them a clear, immediate action plan in seconds — before they even leave the house.

⚙️ Architecture Overview Ambulance / Field Unit │ │ (vitals, location, patient data) ▼ Firebase Firestore ◄──────────────────────────────────┐ │ │ │ (real-time snapshots) Hospital Portal ▼ (updates bed/ICU counts, Hospital Dashboard resource availability) (ER team sees patient data before arrival)

🐛 The Debugging Journey Building MedVyavastha was a race against time. Here's an honest account of the technical challenges we battled — and beat.

🔄 Real-time Data Sync Lag Problem: Significant lag when syncing patient vitals between the ambulance and the hospital dashboard, causing the ER to see outdated information. Fix: Optimized Firebase Firestore listeners and implemented local state management so the UI updates instantly — without waiting for full database round-trips.

📄 PptxGenJS Memory Leaks Problem: Generating automated medical reports in PPT format caused browser memory leaks during conversion of complex data tables. Fix: Refactored the data-parsing logic to process information in smaller chunks, ensuring smooth document generation even on low-end devices.

📶 IoT Connectivity in Low-Network Areas Problem: Emergency transit often passes through low-network zones. Unstable connections caused the application to crash mid-transit. Fix: Implemented a "Sync-when-Online" architecture using Firebase's offline persistence — the app stores data locally and uploads it the moment connectivity is restored. No data loss, no crashes.

👻 The "Ghost UI" (Unclickable Elements) Problem: Every element on the FindHospital page was visible but completely unresponsive — buttons, search bars, all of it. Fix: Discovered a Z-index conflict where an invisible CSS overlay was silently capturing all click events. Fixing the CSS layering instantly restored full interactivity.

🔍 Search-to-Box Breakdown Problem: Search results appeared but the hospital detail boxes refused to open or expand on click. Fix: Refactored the state logic — the search query wasn't correctly triggering the toggle state for hospital detail components.

🌫️ The "Blur & Drift" Visual Crisis Problem: After fixing search, two visual bugs appeared simultaneously: a permanent blur filter stuck on screen, and hospital cards shifting into overlapping positions. Fix: A CSS class wasn't being removed after a modal closed. Manually cleaned up conditional rendering and reset Flexbox positioning across components.

⚡ Static Data → Live Firebase Integration Problem: Even with the UI fully functional, hospital availability data was static — it didn't reflect real-world changes. Fix: After extensive troubleshooting, successfully linked the frontend to Firebase Firestore with real-time snapshots, so availability data updates live across all connected clients without a page refresh.

👥 The Team Pranshu Aryan Lead Backend Engineer & Systems Architect End-to-end backend architecture, full Firebase integration, and real-time database management. Primary debugger — resolved deep-rooted UI/UX bottlenecks and ensured seamless data flow between hospital and transit systems.

Mahima Kumari Lead Frontend Developer & Feature Specialist Headed development of core platform features and frontend coordination. Translated complex healthcare workflows into functional, accessible user interfaces and ensured cross-component compatibility throughout the sprint.

🌐 Live Demo medvyavastha.netlify.app The platform is live and fully functional. Hospital staff can log in via the hospital portal to update real-time availability. Emergency coordinators and ambulance teams can access the transit dashboard.

📁 Repository Structure / ├── index.html # Landing page ├── findhospital.html # GPS-powered hospital finder ├── register.html # Hospital registration portal ├── hospital-home.html # Hospital management dashboard ├── assets/ │ ├── css/ # Stylesheets │ └── js/ # Scripts └── README.md

⚖️ License & Intellectual Property This project is proprietary. The source code is made public for review and evaluation purposes only. No permission is granted to copy, modify, redistribute, or use this codebase — in whole or in part — for any purpose without explicit written consent from the authors. © 2026 MedVyavastha. All rights reserved.

Built under pressure. Debugged with patience. Deployed with purpose. MedVyavastha — Because the ER should never be caught off guard.
