### **Project Sprint Plan: AMC Premiere Finder (MVP)**

This document outlines the sprint-by-sprint plan to develop, test, and deploy the Minimum Viable Product (MVP) of the AMC Premiere Finder application.

* **Team Composition (Assumed):** 1 Product Manager, 1-2 Backend Engineers, 1-2 Mobile Engineers (cross-platform), 1 QA Engineer.
* **Sprint Duration:** 2 Weeks
* **Project Start Date:** Monday, August 11, 2025

---

### **Sprint 1: The Foundation (Backend & API)**

* **Dates:** Monday, August 11, 2025 – Friday, August 22, 2025
* **Sprint Goal:** **Establish the core backend infrastructure and a functional API.** By the end of this sprint, the mobile team will have a live, albeit basic, endpoint they can use to start building the app.

| Priority | User Story / Task | Story Points | Team Member(s) | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | **TECH-301:** Set up database and data ingestion pipeline. | 8 | Backend | Focus on creating the `Movie`, `Theater`, and `Showing` data models. The initial ingestion can be from a static mock file to start. |
| **P0** | **TECH-302:** Implement premiere-flagging logic. | 3 | Backend | Develop and test the business logic to correctly set the `is_premiere` flag on showtimes based on the release date. |
| **P0** | **TECH-303:** Build and deploy V1 of the `/premieres` API endpoint. | 5 | Backend | Create the `GET /api/v1/premieres` endpoint. It should accept location parameters and return a structured JSON response of premiere data. |
| **P0** | **Project Setup:** Initialize mobile app repository (React Native/Flutter). | 2 | Mobile | Set up the basic project structure, navigation, and theme files for the mobile application. |

**Sprint 1 Review & Retrospective:**
* **Review:** Demonstrate the API endpoint being called (e.g., via Postman) and successfully returning structured, mocked premiere data.
* **Retrospective:** Discuss the reliability of the data source and the clarity of the API contract.

---

### **Sprint 2: The "See" Sprint (Mobile UI - Home Screen)**

* **Dates:** Monday, August 25, 2025 – Friday, September 5, 2025
* **Sprint Goal:** **Build a functional home screen that displays real data.** The user should be able to open the app, grant location permissions, and see a list of premieres fetched from the backend API.

| Priority | User Story / Task | Story Points | Team Member(s) | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | **CORE-101:** Implement location permission request flow. | 3 | Mobile | Integrate native location services to get the user's coordinates. |
| **P0** | **CORE-102:** Implement manual ZIP code entry UI. | 2 | Mobile | Create the UI for manual input as a fallback. |
| **P0** | **API Integration:** Connect the mobile app to the `/premieres` endpoint. | 3 | Mobile | Implement the network layer in the app to fetch data from the live API developed in Sprint 1. |
| **P0** | **CORE-103:** Build the home screen premiere list UI. | 5 | Mobile | Develop the scrollable list component, with each item showing the movie poster, title, and premiere date. |
| **P0** | **QA:** Test location services and data display. | 3 | QA | Verify that location is detected correctly and that data from the API is rendered properly on the home screen. |

**Sprint 2 Review & Retrospective:**
* **Review:** Demonstrate the live application on a device/simulator. Show the app requesting permissions, fetching data from the API, and displaying the list of local premieres.
* **Retrospective:** Discuss challenges with native location APIs and the performance of the data fetch.

---

### **Sprint 3: The "Decide & Act" Sprint (Details & Handoff)**

* **Dates:** Monday, September 8, 2025 – Friday, September 19, 2025
* **Sprint Goal:** **Allow users to make a decision and act on it.** Complete the core user journey by building the movie detail screen and implementing the deep link to the AMC ticketing platform.

| Priority | User Story / Task | Story Points | Team Member(s) | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | **CORE-104:** Build the movie detail screen UI. | 3 | Mobile | Create the static parts of the detail screen: synopsis, rating, trailer player, etc. |
| **P0** | **CORE-105:** Display local theaters and showtimes on the detail screen. | 5 | Mobile | Fetch and display the dynamic list of nearby theaters and their specific premiere showtimes for the selected movie. |
| **P0** | **CORE-106:** Implement deep-linking to the AMC app/website. | 3 | Mobile | Configure the app to correctly format and launch the deep links for ticketing. This requires research into AMC's specific URL schemes. |
| **P0** | **Backend:** Refine data source. | 5 | Backend | Move from mocked data to a more robust solution (e.g., a test API or a scraper for the live AMC site). |
| **P0** | **QA:** End-to-end testing of the user flow. | 5 | QA | Test the full journey: Open app -> Select movie -> Select showtime -> Verify correct handoff to AMC platform. |

**Sprint 3 Review & Retrospective:**
* **Review:** Demonstrate the complete, end-to-end MVP user flow on a device.
* **Retrospective:** Discuss the complexities of deep-linking and the stability of the data source.

---

### **Sprint 4: Polish, Test, & Deploy**

* **Dates:** Monday, September 22, 2025 – Friday, October 3, 2025
* **Sprint Goal:** **Prepare the MVP for a public release.** Focus on bug fixing, performance optimization, and completing all necessary steps for submission to the app stores.

| Priority | User Story / Task | Story Points | Team Member(s) | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | **Bug Fixing:** Address all P0 and P1 bugs identified by QA. | 8 | All Engineers | Focused effort to stabilize the application. |
| **P1** | **Performance Tuning:** Optimize app startup time and list scrolling. | 5 | Mobile | Profile the app and address any performance bottlenecks. |
| **P1** | **UI/UX Polish:** Final design review and adjustments. | 3 | Mobile | Address minor UI inconsistencies, improve loading states, and refine animations. |
| **P0** | **Deployment Prep:** Prepare app store listings. | 3 | Product, Mobile | Create screenshots, write app descriptions, configure privacy policies, and prepare for submission. |
| **P0** | **Final Regression Testing:** Full regression test of the final release candidate. | 5 | QA | Final sign-off on the application before submission. |

**Sprint 4 Review & Retrospective:**
* **Review:** Present the final, polished application. Confirm that it is ready for release.
* **Retrospective:** Conduct a project-level retrospective to discuss what went well and what could be improved for future projects.

**Official MVP Launch Target: Week of October 6, 2025.**
