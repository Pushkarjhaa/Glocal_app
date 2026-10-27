# Glocal_app
# GLOCAL – Skill Assessment Mobile App

A Flutter app that runs the full skill-assessment workflow, from creating a batch to approving results, for five user roles in one codebase.


> **Note:** The source code belongs to the client and is not public. This repository showcases the app's features, architecture and my contribution. I'm happy to walk through the code in an interview.


## 📱 Screenshots

| Login | Agency Dashboard | Batch Details |
|:---:|:---:|:---:|
<img width="720" height="1600" alt="agency_login" src="https://github.com/user-attachments/assets/22356185-1beb-4c83-8f9e-aa0f4b6303e4" />

<img width="720" height="1600" alt="agency_batch_details" src="https://github.com/user-attachments/assets/411c3726-7d78-4ea2-9c06-0ccd3405269f" />
<img width="720" height="1600" alt="agency_dashboard" src="https://github.com/user-attachments/assets/b5d4a5ab-a9c3-4950-a792-f12589523b56" />



| Assessor Dashboard | Live Assessment | Result CSV Upload |
|:---:|:---:|:---:|
<img width="720" height="1600" alt="assessor_login" src="https://github.com/user-attachments/assets/d0ddbbaf-5c4a-42f3-b61a-ab02660e981f" />
<img width="720" height="1600" alt="upload_csv_result" src="https://github.com/user-attachments/assets/d01b209d-ddc4-43fc-ba59-0851f909b622" />
<img width="720" height="1600" alt="assessor_dashboard" src="https://github.com/user-attachments/assets/1c7e28f6-3a13-4d13-8a16-28ca556d6a65" />



| Candidate Exam | Proctor View | Operator |
|:---:|:---:|:---:|


---

## 🧩 The Problem

Skill assessments for training programmes are run by several parties: training agencies, assessors, proctors and the candidates themselves. Before this app, much of that work happened on a web portal from a desktop, even though assessors and proctors work in the field at the assessment centres.


---

## 👥 User Roles & Features

### 🏢 Agency
- Dashboard with batch, candidate and assessment statistics
- Create and update batches, import candidates in bulk (CSV), and upload candidate photos in bulk
- Assign assessors, proctors and question papers, and schedule the assessment date and time
- Manage staff: create and edit proctors and operators, and assign sectors
- Track live assessments and view batch results

### 📝 Assessor
- Today's assessments, split into **Online** and **Offline**
- Mark attendance with a live photo, ID proof and GPS location
- Assigned batches: accept or **return a batch to the agency** (re-assign)
- **Offline result upload:** download a sample CSV, fill it in, upload it and see row-level error reports
- Send results for approval, then view and update them until they are approved

### 🎓 Candidate
- Login, profile, and ID-card / photo verification
- Take the online exam (theory / viva / practical)
- View exam status and results

### 👁️ Proctor
- Assigned batches and attendance with photo and location
- Monitor candidates during the assessment

### ⚙️ Operator
- Sector-based access to batches and candidates
- Day-to-day data entry and support tasks

---

## 🛠️ Tech Stack

| Area | Technology |
|---|---|
| Framework | Flutter 3.38, Dart 3.10 |
| State management | `flutter_bloc` (Cubit + Equatable) |
| Navigation | `go_router` (StatefulShellRoute, nested navigation, auth redirect) |
| Networking | `dio` with a central API client, interceptors and per-role tokens |
| Device features | Camera, geolocation, file picker, image compression |
| Files | CSV import/export, multipart upload, share sheet |
| Storage | Secure session storage per role |
| Release | Signed Android App Bundle, adaptive launcher icons |

---

## 🏗️ Architecture

The code is organised **feature-first**, with a shared core layer:

```
lib/
├── core/
│   ├── network/        # API client (Dio), exceptions, interceptors
│   ├── theme/          # Colors, text styles, design tokens
│   ├── widgets/        # Reusable UI components (buttons, fields, toasts…)
│   └── routing/        # App router + session redirect
└── features/
    ├── agency/
    │   ├── data/
    │   └── presentation/
    │       ├── bloc/       # Cubits + States
    │       ├── pages/      # Screens
    │       ├── widgets/    # Feature-specific widgets
    │       └── routing/    # Role routes
    ├── assessor/
    ├── candidate/
    ├── proctor/
    └── operator/
```

**Flow:** `UI (Page)` → `Cubit` → `ApiClient (Dio)` → `REST API` → `State` → `UI rebuild`

- Each role is a self-contained feature module, so a change in one role does not affect another.
- Cubits keep the business logic out of widgets, and Equatable states avoid unnecessary rebuilds.
- A single API client handles the base URL, tokens, error parsing and multipart uploads in one place.

<img src="docs/architecture.png" width="700"/>

---

## 📊 Project in Numbers

| | |
|---|---|
| Screens | **131** |
| Cubits (state classes) | **109** |
| REST APIs integrated | **150+** |
| Routes | **159** |
| Lines of Dart code | **~73,000** |
| User roles | **5** |

---

## 💡 Key Challenges I Solved

- **Five roles, one app.** I built per-role authentication and token handling so each role has its own session, routes and dashboard.
- **Field verification.** I built the live photo, ID proof and GPS capture flow, and fixed a camera bug caused by permission requests firing at the same time.
- **Offline results.** I built a CSV download/upload flow that reads the server's validation response and shows the user exactly which rows failed and why.
- **Complex navigation.** I used nested tab navigation with `StatefulShellRoute` and fixed back-stack issues after create/edit flows.
- **Parity with the web portal.** I matched the existing web portal screen by screen and worked with the backend team to define and verify the API contracts.
- **Release.** I set up release signing, adaptive launcher icons and app bundle builds for the Play Store.

---

## 👨‍💻 My Role

**Flutter Developer.** I was responsible for the mobile app end to end:
- UI/UX implementation across 131 screens
- State management and app architecture
- REST API integration and coordination with the backend team
- Testing with the QA team, bug fixing and release builds

---

## 📄 More Details

- [Technical Overview (PDF)](docs/Technical_Overview.pdf)

---

## 📬 Contact

**Pushkar Jha**
- LinkedIn: [linkedin.com/in/your-profile](https://linkedin.com/in/your-profile)
- Email: your.email@example.com
- GitHub: [github.com/your-username](https://github.com/your-username)
