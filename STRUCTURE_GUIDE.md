# IELTS Test Interface Structure

## Visual Structure Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                      index.html                              │
│              (Main Landing Page)                             │
│                                                              │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐       │
│   │ 🎧 Listening │  │ 📖 Reading   │  │ ✍️ Writing   │       │
│   │ 10 Types    │  │ 12 Types    │  │ 2 Parts     │       │
│   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘       │
└──────────┼─────────────────┼─────────────────┼──────────────┘
           │                 │                 │
           ▼                 ▼                 ▼
    
┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│ listening.xhtml  │  │  reading.xhtml   │  │  writing.xhtml   │
├──────────────────┤  ├──────────────────┤  ├──────────────────┤
│ HEADER           │  │ HEADER           │  │ HEADER           │
│ • IELTS Logo     │  │ • IELTS Logo     │  │ • IELTS Logo     │
│ • Partners       │  │ • Partners       │  │ • Partners       │
│                  │  │                  │  │                  │
│ TEST BANNER      │  │ TEST BANNER      │  │ TEST BANNER      │
│ • Candidate Info │  │ • Candidate Info │  │ • Candidate Info │
│ • Timer          │  │ • Timer          │  │ • Timer          │
│ • 🔊 VOLUME BAR  │  │ (no audio)       │  │ (no audio)       │
│ • Settings       │  │ • Settings       │  │ • Settings       │
│ • Help           │  │ • Help           │  │ • Help           │
│ • Hide           │  │ • Hide           │  │ • Hide           │
│                  │  │                  │  │                  │
│ NAVIGATION       │  │ NAVIGATION       │  │ NAVIGATION       │
│ ├─ Fill in gaps  │  │ ├─ Flow-chart    │  │ ├─ Part 1        │
│ ├─ Short answers │  │ ├─ True/False    │  │ └─ Part 2        │
│ ├─ Flow-chart    │  │ ├─ Matching      │  │                  │
│ ├─ Form          │  │ ├─ Headings      │  │                  │
│ ├─ Map labelling │  │ ├─ Endings       │  │                  │
│ ├─ Matching      │  │ ├─ MCQ Multiple  │  │                  │
│ ├─ MCQ Multiple  │  │ ├─ MCQ Single    │  │                  │
│ ├─ MCQ Single    │  │ ├─ Note          │  │                  │
│ ├─ Sentence      │  │ ├─ Sentence      │  │                  │
│ └─ Table         │  │ ├─ Summary List  │  │                  │
│                  │  │ ├─ Summary Text  │  │                  │
│                  │  │ └─ Table         │  │                  │
│                  │  │                  │  │                  │
│ MAIN CONTENT     │  │ MAIN CONTENT     │  │ MAIN CONTENT     │
│ (Dynamic Load)   │  │ (Dynamic Load)   │  │ (Dynamic Load)   │
│                  │  │                  │  │                  │
│ FOOTER           │  │ FOOTER           │  │ FOOTER           │
│ • Review ☑       │  │ • Review ☑       │  │ • Review ☑       │
│ • ← Previous     │  │ • ← Previous     │  │ • ← Previous     │
│ • Next →         │  │ • Next →         │  │ • Next →         │
└──────────────────┘  └──────────────────┘  └──────────────────┘
```

## Component Breakdown

### 1. HEADER SECTION
```
┌────────────────────────────────────────┐
│  [IELTS Logo]      [Partner Logos]     │
└────────────────────────────────────────┘
```

### 2. TEST BANNER SECTION
```
┌─────────────────────────────────────────────────────────┐
│ Candidate: XXXX XXXXXXX | Number: 123456    Time: 30min│
│                                                          │
│ [LISTENING ONLY: 🔊━━━━━━━━━━ Volume Control]          │
│                                                          │
│ [Settings] [Help] [Hide]                                │
└─────────────────────────────────────────────────────────┘
```

### 3. NAVIGATION SECTION
```
┌───────────────────────────────────────┐
│ Question Types                        │
├───────────────────────────────────────┤
│ 1. [Question Type 1]                  │
│ 2. [Question Type 2]                  │
│ 3. [Question Type 3]                  │
│ ...                                   │
│                                       │
│ [Summary View] [Details View]        │
└───────────────────────────────────────┘
```

### 4. MAIN CONTENT AREA
```
┌───────────────────────────────────────┐
│                                       │
│   Question content loads here         │
│   dynamically based on selection      │
│                                       │
└───────────────────────────────────────┘
```

### 5. FOOTER CONTROLS
```
┌───────────────────────────────────────┐
│ ☑ Review   [← Previous]  [Next →]    │
└───────────────────────────────────────┘
```

## Interface Comparison Matrix

| Feature                | Listening | Reading | Writing |
|------------------------|-----------|---------|---------|
| IELTS Logo Header      | ✅        | ✅      | ✅      |
| Candidate Info         | ✅        | ✅      | ✅      |
| Timer                  | ✅        | ✅      | ✅      |
| Volume Control Bar     | ✅        | ❌      | ❌      |
| Settings Button        | ✅        | ✅      | ✅      |
| Help Button            | ✅        | ✅      | ✅      |
| Hide Button            | ✅        | ✅      | ✅      |
| Navigation Bar         | ✅        | ✅      | ✅      |
| Question Type Links    | ✅ (10)   | ✅ (12) | ✅ (2)  |
| Review Checkbox        | ✅        | ✅      | ✅      |
| Previous/Next Buttons  | ✅        | ✅      | ✅      |
| Dynamic Content Area   | ✅        | ✅      | ✅      |

## File Relationships

```
/app/
├── index.html                          ← Main entry point
│
├── listening.xhtml                     ← Listening interface
│   └── Links to ↓
├── Listening/
│   ├── Fill in the gaps/
│   │   └── index.xhtml
│   ├── Fill in the gaps short answers/
│   │   └── index.xhtml
│   ├── Flow-chart Completion/
│   │   └── index.xhtml
│   └── ... (10 types total)
│
├── reading.xhtml                       ← Reading interface
│   └── Links to ↓
├── Reading/
│   ├── Flow-chart Completion (selecting words from the text)/
│   │   └── index.xhtml
│   ├── Identifying Information (TrueFalseNot Given)/
│   │   └── index.xhtml
│   ├── Matching Headings/
│   │   └── index.xhtml
│   └── ... (12 types total)
│
├── writing.xhtml                       ← Writing interface
│   └── Links to ↓
└── Writing/
    ├── writing-part-1/
    │   └── index.xhtml
    └── writing-part-2/
        └── index.xhtml
```

## User Journey Flow

```
User Journey:
┌─────────┐
│  Start  │
└────┬────┘
     │
     ▼
┌─────────────────┐
│  index.html     │  Choose test type
│  Landing Page   │
└────┬────┬───┬───┘
     │    │   │
   Listening │ Writing
     │    Reading
     ▼       │   │
┌──────────┐ │   │
│Listening │ │   │
│Interface │ │   │
└──────────┘ │   │
     │       ▼   ▼
     │   ┌─────────┐ ┌─────────┐
     │   │ Reading │ │ Writing │
     │   │Interface│ │Interface│
     │   └─────────┘ └─────────┘
     │       │           │
     ▼       ▼           ▼
┌───────────────────────────────┐
│  Select Question Type         │
│  from Navigation              │
└───────┬───────────────────────┘
        │
        ▼
┌───────────────────────────────┐
│  Question Content Loads       │
│  in Main Area                 │
└───────┬───────────────────────┘
        │
        ▼
┌───────────────────────────────┐
│  Answer Questions             │
│  Use Previous/Next            │
│  Mark for Review              │
└───────────────────────────────┘
```

## Key Design Decisions

### 1. Volume Control Placement
- **Listening:** Volume control bar placed in test banner, easily accessible
- **Reading/Writing:** No volume control (not needed for these test types)

### 2. Navigation Structure
- All question types visible in navigation bar
- Easy switching between different question formats
- Clear labeling of each question type

### 3. Consistent Layout
- Same header/footer structure across all interfaces
- Predictable button placements
- Familiar user experience regardless of test type

### 4. Accessibility
- Proper ARIA labels for screen readers
- Keyboard navigation support
- Reader-only text for important elements

### 5. Responsive Design
- Utilizes existing responsive CSS from question folders
- Adapts to different screen sizes
- Mobile-friendly navigation

---

**Visual Guide Version:** 1.0
**Last Updated:** October 18, 2024
