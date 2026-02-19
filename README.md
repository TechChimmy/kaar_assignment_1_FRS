# 🎓 Student Portal — Project Summary

**Assignment:** Responsive Student Management Website
**Tech Stack:** HTML5 · CSS3 · Vanilla JavaScript
**Submitted to:** KaarTech

---

## Overview

Student Portal is a fully responsive, browser-based academic management application built using only HTML, CSS, and JavaScript — no frameworks, no libraries, no backend. All data is persisted locally using the browser's `localStorage` API, meaning records survive page reloads without any server involvement.

---

## File Structure

```
student-portal/
├── index.html      — HTML structure and semantic markup, All styling including responsive layout and dark mode, All application logic and DOM interaction
```

---

## Design

### Visual Language
The entire UI is built around a single **Deep Navy Blue** colour palette (`#2563B0` as the base), ranging from near-black `#071020` to near-white `#F8FBFF`. No secondary accent colours are used — contrast, hierarchy, and depth are all achieved through shades of the same hue.

### Typography
**Plus Jakarta Sans** (Google Fonts) is used throughout — a modern geometric sans-serif with clean weight variation from 300 to 800, giving the interface a professional and academic character.

### Layout
- Desktop uses a flex/grid layout with a max-width of 1240px
- Feature cards sit in a **3-column grid** on desktop, collapsing to 2 then 1 on smaller screens
- The registration form uses a **2-column grid** that stacks to 1 column on mobile
- The hero section splits into a left content area and a right live preview card

### Light and Dark Mode
The app ships with a **white background light theme** as default. A toggle in the nav switches to a deep navy dark mode. Both themes use the same blue palette — the dark mode simply inverts the shade scale so light colours become text and dark colours become backgrounds. Theme preference is saved to `localStorage` and restored on page load.

### Responsive Behaviour
- **Desktop (>900px):** Horizontal nav, 3-column cards, full-width table, hero split layout
- **Tablet (720–900px):** 2-column cards, form adjusts proportionally
- **Mobile (<720px):** Hamburger menu, single-column cards, stacked form, horizontally scrollable table, hero preview card hidden to save space

---

## Functional Requirements (All Met)

### Navigation Bar
- Logo with icon on the left
- Three nav links — Home, Students, Contact — with active state styling
- Collapses into an animated **hamburger menu** on mobile with smooth open/close transition

### Feature Cards
Three informational cards each with an icon banner, title, description, and a "Learn More" button that links to the relevant section. Cards animate in on load with a staggered fade-up effect.

### Registration Form
Collects four fields:

| Field | Type | Validation |
|---|---|---|
| Student Name | Text | Required, non-empty |
| Email Address | Email | Required, regex format check |
| Course Enrolled | Dropdown | Must select an option |
| Age | Number | Required, must be between 10 and 80 |

- Submission is prevented if any field fails validation
- Inline error messages appear below each invalid field
- The form resets automatically after a successful submission
- In edit mode, the submit button label changes to **Update Student**

### Student Table
Displays all enrolled students with columns: Serial No, Name, Email, Course (as a badge), Age, and Actions (Edit + Delete buttons).

- **Live search** filters rows across name, email, and course simultaneously
- **Sortable columns** — Name, Course, and Age can be sorted ascending or descending by clicking the column header; active sort direction is shown with ↑ / ↓
- **Empty state** shows a friendly message when no records exist or no search results are found
- A student count badge updates in real time

### Delete Functionality
Each row has a Delete button. Clicking it triggers a browser confirmation dialog before removing the record from both the table and `localStorage`.

### Edit Functionality
Each row has an Edit button. Clicking it pre-fills the registration form with that student's data, scrolls to the form, and changes the submit button to "Update Student". On update, the record is replaced in-place in the array and re-saved.

### localStorage Persistence
Students are stored as a JSON array under the key `studentPortalV3`:

```json
[
  {
    "name": "Arjun Sharma",
    "email": "arjun@example.com",
    "course": "Computer Science",
    "age": 21
  }
]
```

Data is loaded on page boot and saved on every add, edit, delete, or import operation.

### Footer
Includes copyright text, a version label, a tagline, and four dummy social media links (Twitter, LinkedIn, GitHub, Email) that lift on hover.

---

## Additional Features

### 1. Analytics Dashboard
A live statistics panel displays five metric cards that update automatically whenever the student list changes:

- **Total Students** — count of all records
- **Courses Offered** — number of distinct courses enrolled
- **Average Age** — mean age across all students
- **Youngest Student** — age and name of the youngest record
- **Oldest Student** — age and name of the oldest record

### 2. Course Distribution Chart
Below the analytics cards, a horizontal bar chart renders one row per course showing relative enrolment proportions. Bars animate to their correct width using a CSS transition. The chart updates live as students are added or removed.

### 3. CSV Export
A single-click **Export CSV** button generates a properly formatted `.csv` file of all student records and triggers a browser download named `students.csv` with a header row included.

### 4. CSV Import
An **Import CSV** button opens a file picker. The selected file is parsed row by row — each row is validated (email format, age range, required fields) before being added. Invalid rows are skipped and a toast reports how many were imported versus skipped.

Expected import format:
```
Name,Email,Course,Age
Arjun Sharma,arjun@example.com,Computer Science,21
Sneha Patel,sneha@example.com,Data Science,22
```

### 5. Recent Enrollments Card
The hero section displays a live mini-card showing the last 3 students added (most recent first), with their initials avatar, name, course, and age. When no students exist it shows an empty state prompt. Updates instantly on every add, edit, delete, or import.

### 6. Toast Notifications
A non-blocking toast notification appears at the bottom-right of the screen after every key action — add, update, delete, export, import — with a blue dot for success and a red dot for errors. Disappears automatically after 3.2 seconds.

### 7. Dark / Light Theme Toggle
A moon/sun button in the nav bar toggles between light and dark mode. The preference is saved to `localStorage` and restored on every page load so the user's choice persists across sessions.

---

## JavaScript Concepts Used

- `localStorage.getItem` / `setItem` for persistence
- `JSON.parse` / `JSON.stringify` for serialisation
- DOM manipulation via `getElementById`, `innerHTML`, `classList`
- Event listeners — `click`, `oninput`, `onchange`
- Array methods — `filter`, `map`, `sort`, `reduce`, `splice`, `slice`, `reverse`
- `FileReader` API for CSV import
- `Blob` and `URL.createObjectURL` for CSV export
- Template literals for dynamic HTML generation
- Regex for email validation

## CSS Concepts Used

- CSS custom properties (variables) for the entire colour system
- Flexbox for nav, hero, footer, and card layouts
- CSS Grid for feature cards, form fields, and analytics panel
- `@media` queries for mobile, tablet, and desktop breakpoints
- `backdrop-filter: blur()` for frosted glass nav and mobile menu
- CSS `@keyframes` animations — fade-up on load, pulse on hero badge dot
- `transition` for hover effects, bar chart widths, and theme switching
- `clamp()` for fluid responsive typography

---

## Browser Compatibility

Works in all modern browsers — Chrome, Firefox, Edge, Safari. Requires no build tools, bundlers, or installations. Open `index.html` directly in a browser or serve via GitHub Pages.

---

## Deployment

Hosted on **GitHub Pages** — upload all three files to a public GitHub repository, enable Pages under Settings → Pages → Source: main branch, and the site goes live at:

```
https://YOUR-USERNAME.github.io/student-portal/
```

---

*© 2026 Student Portal · Academic Management System v2.0*
