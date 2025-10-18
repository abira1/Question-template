# 🎯 HANDOFF INSTRUCTIONS FOR NEXT AGENT

## Mission Overview
You are receiving an IELTS Mock Test website that needs a complete exam interface overhaul. Your task is to:
1. **REMOVE** all current exam interface, question types, and related features
2. **IMPLEMENT** the exact same interface, functionalities, and question types from this reference codebase
3. **INTEGRATE** all features including notes, highlighting, audio control, timer, and 24 question types

---

## 📋 PHASE 1: REMOVAL (Clean Slate)

### Step 1.1: Identify Current Exam Components
First, locate and document all existing exam-related code:

```bash
# Search for exam-related files
find . -type f -name "*exam*" -o -name "*test*" -o -name "*question*"

# Search for exam-related code
grep -r "exam\|test\|question" --include="*.js" --include="*.jsx" --include="*.ts" --include="*.tsx"
```

### Step 1.2: Remove Old Exam Interface
Delete or comment out:
- [ ] Old exam pages/components
- [ ] Old question type components
- [ ] Old exam routes
- [ ] Old exam API endpoints
- [ ] Old exam database models/schemas
- [ ] Old exam styles/CSS

**⚠️ IMPORTANT:** 
- Keep the admin panel intact
- Keep the "AI Import" feature (we'll modify it later)
- Keep user authentication system
- Keep database connection setup

### Step 1.3: Backup Before Removal
```bash
# Create backup branch
git checkout -b backup-old-exam-interface
git add .
git commit -m "Backup: Old exam interface before removal"
git checkout main
```

---

## 📦 PHASE 2: FILES YOU NEED FROM THIS CODEBASE

### Required Documentation Files (READ THESE FIRST!)
Copy these files from this codebase to your project:

```
📁 Documentation Files:
├── INTEGRATION_PLAN.md          ← Complete implementation guide
├── JSON_STRUCTURE_GUIDE.md      ← All 24 question types JSON format
├── STRUCTURE_GUIDE.md           ← Visual structure diagrams
├── QUICKSTART.md                ← Quick reference
└── INTERFACE_DOCUMENTATION.md   ← Technical interface details
```

### Required Asset Files
Copy these folders/files from this codebase:

```
📁 Assets & Resources:
├── Listening/
│   ├── Fill in the gaps/
│   │   ├── css/ (all CSS files)          ← Styling for interface
│   │   ├── js/
│   │   │   ├── notes.js                  ← Notes system code
│   │   │   ├── qti.js                    ← Core exam functionality
│   │   │   ├── theme.js                  ← Highlighting setup
│   │   │   └── (all other JS files)      ← jQuery, UI libraries
│   │   └── images/banner/                ← IELTS logos
│   └── (repeat for other question types)
│
├── Reading/
│   └── Matching Headings/
│       ├── css/ (all CSS files)
│       └── js/ (all JS files)
│
└── Writing/
    └── writing-part-1/
        ├── css/ (all CSS files)
        └── js/ (all JS files)
```

### Reference Interface Files
Use these as templates:

```
📁 Interface Templates:
├── listening.xhtml    ← Listening interface (WITH audio control)
├── reading.xhtml      ← Reading interface (NO audio control)
├── writing.xhtml      ← Writing interface (NO audio control)
└── index.html         ← Landing page template
```

---

## 🎯 PHASE 3: IMPLEMENTATION REQUIREMENTS

### 3.1: Interface Components to Build

#### **A. Header Section**
```jsx
Components needed:
- Logo (IELTS logo)
- Partner logos
- Candidate information display
- Test type indicator
```

#### **B. Test Banner**
```jsx
Components needed:
- Candidate name & number display
- Timer with countdown (format: MM:SS)
- Audio control bar (ONLY for Listening tests)
  * Volume slider (0-100%)
  * Play/Pause button
  * Time display
- Action buttons:
  * Settings button
  * Help button
  * Hide button
```

#### **C. Navigation Bar**
```jsx
Components needed:
- Question list navigation
- Current question highlight
- Question status indicators (answered/unanswered/marked)
- View toggle (Summary/Details)
```

#### **D. Main Content Area**
```jsx
Components needed:
- Question renderer (dynamic based on type)
- Instructions display
- Content area (text, tables, images, etc.)
- Answer input areas
```

#### **E. Footer Navigation**
```jsx
Components needed:
- Review checkbox (mark for review)
- Previous button
- Next button
- Question number display
```

#### **F. Feature Components**
```jsx
Critical features to implement:
1. Notes System:
   - Create sticky notes
   - Drag and move notes
   - Edit note content
   - Delete notes
   - Save note positions
   - Show highlighted text in note

2. Text Highlighting:
   - Select text functionality
   - Context menu with color options
   - Apply highlights (yellow, green, blue, pink)
   - Remove highlights
   - Save highlights

3. Help Modal:
   - Instructions display
   - Keyboard shortcuts
   - Feature guide

4. Timer:
   - Countdown timer
   - Warning at 10 minutes
   - Critical warning at 5 minutes
   - Auto-submit at time-up
```

### 3.2: Question Types to Implement (All 24)

#### **Listening (10 Types)**
```
Required Components:
1. FillInGaps.jsx
2. FillInGapsShortAnswers.jsx
3. FlowChartCompletion.jsx
4. FormCompletion.jsx
5. MapLabelling.jsx
6. Matching.jsx
7. MultipleChoiceMultiple.jsx
8. MultipleChoiceSingle.jsx
9. SentenceCompletion.jsx
10. TableCompletion.jsx
```

#### **Reading (12 Types)**
```
Required Components:
1. FlowChartCompletionText.jsx
2. TrueFalseNotGiven.jsx
3. MatchingFeatures.jsx
4. MatchingHeadings.jsx
5. MatchingSentenceEndings.jsx
6. MultipleChoiceMultiple.jsx
7. MultipleChoiceSingle.jsx
8. NoteCompletion.jsx
9. SentenceCompletion.jsx
10. SummaryCompletionList.jsx
11. SummaryCompletionText.jsx
12. TableCompletion.jsx
```

#### **Writing (2 Types)**
```
Required Components:
1. WritingTask1.jsx (Academic - graphs/charts/diagrams)
2. WritingTask2.jsx (Essay - 250 words)
```

**📖 Detailed specifications for each type:** See `JSON_STRUCTURE_GUIDE.md`

### 3.3: Backend API Endpoints to Create

```javascript
Required Endpoints:

// Exam Management
GET    /api/exams                    // List all exams
GET    /api/exams/:id                // Get specific exam with questions
POST   /api/admin/import-exam        // Import from JSON (AI Import feature)
PUT    /api/exams/:id                // Update exam
DELETE /api/exams/:id                // Delete exam

// Question Management
GET    /api/exams/:examId/questions  // Get all questions for exam
GET    /api/questions/:id            // Get specific question
POST   /api/questions                // Create question
PUT    /api/questions/:id            // Update question
DELETE /api/questions/:id            // Delete question

// Test Taking
POST   /api/exams/:id/start          // Start test session
POST   /api/exams/:id/submit         // Submit answers
GET    /api/exams/:id/results        // Get results
POST   /api/exams/:id/save-progress  // Save current progress

// User Features
POST   /api/user/notes               // Save notes
GET    /api/user/notes/:examId       // Get notes for exam
POST   /api/user/highlights          // Save highlights
GET    /api/user/highlights/:examId  // Get highlights for exam

// Audio Files (Listening)
GET    /api/audio/:filename          // Stream audio file
```

**📖 Detailed API specs:** See `INTEGRATION_PLAN.md` Phase 4

### 3.4: Database Models to Create

```javascript
Required Models:

1. Exam Model
   - id, title, type, duration, instructions
   - questions (reference)
   - createdAt, updatedAt

2. Question Model
   - id, examId, questionNumber, questionType
   - section, instructions, audioFile
   - content (JSON), answers (JSON)
   - marks

3. TestSession Model
   - id, userId, examId, startTime, endTime
   - answers (JSON), score, completed
   - notes (JSON), highlights (JSON)

4. UserProgress Model
   - id, userId, examId, currentQuestion
   - answers (JSON), timeSpent
   - notes (JSON), highlights (JSON)
```

**📖 Detailed schemas:** See `INTEGRATION_PLAN.md` Phase 4

---

## 🔧 PHASE 4: INTEGRATION WITH ADMIN PANEL

### 4.1: Modify "AI Import" Feature

The current admin panel has an "AI Import" section. Modify it to accept this JSON format:

**Input Format:**
```json
{
  "exam": {
    "id": "unique-id",
    "type": "listening|reading|writing",
    "title": "Exam Title",
    "duration": 1800,
    "instructions": { },
    "questions": [ ]
  }
}
```

**📖 Complete JSON structure:** See `JSON_STRUCTURE_GUIDE.md`

### 4.2: Admin Panel Features to Add/Update

```jsx
Required Admin Features:

1. Import Tab (existing - modify)
   - JSON input textarea
   - Validate JSON structure
   - Preview imported exam
   - Save to database

2. Exam List Tab
   - Show all imported exams
   - Edit/Delete exams
   - View exam details

3. Question Management Tab
   - View all questions in exam
   - Edit question content
   - Edit correct answers
   - Upload audio files (for listening)

4. Preview Tab
   - Preview exam as student would see
   - Test all features
```

---

## 📚 PHASE 5: IMPLEMENTATION GUIDE

### Step-by-Step Implementation Order

#### Week 1: Foundation Setup
```
Day 1-2: Remove old code, setup new structure
- Clean up old exam code
- Create new folder structure
- Copy necessary CSS/JS files
- Setup component hierarchy

Day 3-4: Build basic interface
- Header component
- Test banner component
- Navigation bar
- Footer navigation

Day 5: Core features setup
- Timer component
- Audio control component (listening)
- Basic routing
```

#### Week 2: Question Types (Priority)
```
Day 1-2: Implement top 5 question types
- Fill in the Gaps
- Multiple Choice Single
- True/False/Not Given
- Matching
- Sentence Completion

Day 3-4: Implement next 10 question types
- Refer to JSON_STRUCTURE_GUIDE.md for each type

Day 5: Implement remaining 9 question types
```

#### Week 3: Advanced Features
```
Day 1-2: Notes System
- Follow code in INTEGRATION_PLAN.md
- Draggable notes
- Save/load functionality

Day 3-4: Text Highlighting
- Follow code in INTEGRATION_PLAN.md
- Color selection
- Save/load functionality

Day 5: Help & Settings
- Help modal
- Settings panel
```

#### Week 4: Backend & Integration
```
Day 1-2: API endpoints
- Create all required endpoints
- Test with Postman/Insomnia

Day 3-4: Admin panel integration
- Modify AI Import
- Add exam management

Day 5: Testing
- Full flow testing
- Bug fixes
```

#### Week 5: Polish & Deploy
```
Day 1-2: Testing
- Test all question types
- Test all features
- Cross-browser testing

Day 3-4: Optimization
- Performance tuning
- Mobile responsiveness

Day 5: Deploy
- Production deployment
- Final testing
```

---

## ✅ VERIFICATION CHECKLIST

Before marking complete, verify:

### Interface Components
- [ ] Header displays correctly
- [ ] Candidate info shows
- [ ] Timer counts down properly
- [ ] Audio control works (listening only)
- [ ] Settings/Help/Hide buttons function
- [ ] Navigation bar shows all questions
- [ ] Footer buttons work (Previous/Next)
- [ ] Review checkbox saves state

### Features
- [ ] Can create sticky notes
- [ ] Notes are draggable
- [ ] Notes save content
- [ ] Can delete notes
- [ ] Can highlight text
- [ ] Can choose highlight colors
- [ ] Highlights persist
- [ ] Can remove highlights
- [ ] Timer warns at 10 and 5 minutes
- [ ] Auto-submit at time-up

### Question Types (Test Each)
- [ ] Fill in the Gaps renders correctly
- [ ] MCQ Single Answer works
- [ ] MCQ Multiple Answers works
- [ ] True/False/Not Given works
- [ ] Matching works
- [ ] Sentence Completion works
- [ ] Summary Completion works
- [ ] Table Completion works
- [ ] Form Completion works
- [ ] Note Completion works
- [ ] Flow-chart works
- [ ] Map Labelling works
- [ ] Matching Headings works
- [ ] Matching Features works
- [ ] Matching Endings works
- [ ] Writing Task 1 works
- [ ] Writing Task 2 works

### Admin Panel
- [ ] Can paste JSON in AI Import
- [ ] JSON validates correctly
- [ ] Exam imports successfully
- [ ] Can view imported exams
- [ ] Can edit exams
- [ ] Can delete exams
- [ ] Can upload audio files
- [ ] Preview works

### Backend
- [ ] All API endpoints work
- [ ] Data saves correctly
- [ ] Answers validate correctly
- [ ] Scoring works
- [ ] Progress saves
- [ ] Audio streams properly

### Performance
- [ ] Page loads in < 3 seconds
- [ ] No memory leaks
- [ ] Smooth animations
- [ ] Responsive on mobile
- [ ] Works on all browsers

---

## 🎓 KEY REFERENCES

### Documentation Priority
```
1. INTEGRATION_PLAN.md         ← START HERE - Complete guide
2. JSON_STRUCTURE_GUIDE.md     ← All question types JSON
3. STRUCTURE_GUIDE.md          ← Visual diagrams
4. QUICKSTART.md               ← Quick reference
```

### Code References
```
1. Notes System Code            → INTEGRATION_PLAN.md Section 2.2.B
2. Text Highlighting Code       → INTEGRATION_PLAN.md Section 2.2.A
3. Audio Control Code           → INTEGRATION_PLAN.md Section 2.2.C
4. Timer Component Code         → INTEGRATION_PLAN.md Section 2.2.D
5. Question Type Examples       → INTEGRATION_PLAN.md Section 3.1
6. API Endpoint Code            → INTEGRATION_PLAN.md Section 4.1
7. Database Models Code         → INTEGRATION_PLAN.md Section 4.2
```

### CSS Files to Use
```
From: /app/Listening/Fill in the gaps/css/
- base.css           → Base styles
- banner.css         → Header/banner styles
- navigation.css     → Navigation bar styles
- tools.css          → Settings/Help buttons
- main.css           → Main content area
- item.css           → Question item styles
- instructions.css   → Instructions display
- custom.css         → Custom overrides
- notepad.css        → Notes system styles

Note: You may need to convert these to your framework's styling system
(CSS Modules, Styled Components, Tailwind, etc.)
```

### JavaScript Files to Reference
```
From: /app/Listening/Fill in the gaps/js/
- notes.js           → Notes system logic (convert to React/Vue)
- qti.js             → Core exam functionality (study logic, adapt)
- theme.js           → Highlighting setup (adapt to your framework)
- jquery.js          → May need if using plain JS
- jquery-ui.js       → Draggable functionality (or use modern alternative)
```

---

## 🚨 CRITICAL WARNINGS

### DO NOT:
❌ Skip reading INTEGRATION_PLAN.md - it has ALL the code
❌ Forget audio control ONLY for Listening tests
❌ Hardcode question types - use dynamic rendering
❌ Skip validation on JSON import
❌ Forget to test all 24 question types
❌ Skip mobile responsiveness
❌ Delete the admin panel
❌ Remove the AI Import feature

### DO:
✅ Follow the exact interface design from listening.xhtml, reading.xhtml, writing.xhtml
✅ Implement ALL features: notes, highlighting, audio, timer
✅ Test each question type thoroughly
✅ Validate JSON structure strictly
✅ Save user progress regularly
✅ Handle errors gracefully
✅ Make it responsive
✅ Optimize for performance

---

## 💬 QUESTIONS TO ASK USER (If Needed)

Before starting, confirm with user:

1. **Tech Stack:**
   - Frontend framework? (React, Vue, Angular, etc.)
   - State management? (Redux, Vuex, Context API)
   - Styling approach? (CSS Modules, Styled Components, Tailwind)
   - Backend? (Node.js, Python, PHP, etc.)
   - Database? (MongoDB, PostgreSQL, MySQL)

2. **Current Admin Panel:**
   - What framework is admin panel built with?
   - Where is the "AI Import" feature located?
   - Current authentication system?

3. **Hosting:**
   - Where are audio files stored? (S3, local, CDN)
   - Where will app be deployed?

---

## 📞 SUPPORT & CLARIFICATIONS

If you need clarification on any part:

1. **For interface questions:** Check listening.xhtml, reading.xhtml, writing.xhtml
2. **For functionality questions:** Check INTEGRATION_PLAN.md
3. **For JSON format questions:** Check JSON_STRUCTURE_GUIDE.md
4. **For question type specs:** Check JSON_STRUCTURE_GUIDE.md (all 24 types detailed)

---

## 🎯 SUCCESS CRITERIA

You're done when:
✅ User can import exam via JSON in admin panel
✅ Exam displays with proper interface (header, timer, navigation, footer)
✅ All 24 question types render correctly
✅ Notes system works (create, drag, edit, delete)
✅ Text highlighting works (select, color, save)
✅ Audio control works for listening tests (with volume slider)
✅ Timer counts down and warns appropriately
✅ User can navigate between questions
✅ User can mark questions for review
✅ User can submit test and get results
✅ All features work on mobile devices
✅ No bugs in any question type

---

## 📦 FINAL DELIVERABLES

After implementation, provide:
1. Updated codebase with new exam interface
2. Documentation of any changes from spec
3. List of any issues encountered
4. Testing report showing all features work
5. Deployment instructions (if applicable)

---

## 🚀 YOU'RE READY!

You have everything you need:
✅ Complete implementation plan
✅ All CSS/JS files
✅ JSON structures for all 24 question types
✅ Code examples for all features
✅ Step-by-step guide
✅ Verification checklist

**Start with:** Reading INTEGRATION_PLAN.md from top to bottom.

Good luck! 🎉
