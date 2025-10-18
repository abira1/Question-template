# IELTS Test Interface Documentation

## Overview
This project now includes unified interface templates for the three IELTS test types: Listening, Reading, and Writing. Each interface provides a consistent structure with dynamic content loading capabilities.

## File Structure

### Main Entry Point
- **index.html** - Landing page that allows users to select test type (Listening, Reading, or Writing)

### Interface Files
1. **listening.xhtml** - Listening test interface WITH volume control bar
2. **reading.xhtml** - Reading test interface WITHOUT volume control
3. **writing.xhtml** - Writing test interface WITHOUT volume control

## Interface Components

### Common Components (All Three Interfaces)
All interfaces include the following standardized components:

#### 1. Banner Section
- IELTS logo and partner logos
- Candidate information display (name and number)
- Timer display
- Settings, Help, and Hide buttons

#### 2. Navigation Bar
- Section label for test type
- Links to all available question types within that test category
- Navigation view toggles (summary/details view)

#### 3. Footer Navigation Controls
- Review checkbox
- Previous Question button
- Next Question button

#### 4. Main Content Area
- Dynamic content loading area

### Unique Features

#### Listening Interface (listening.xhtml)
**Includes Audio Control Bar:**
```xml
<div id="audio-control">
  <div id="slider"></div>
  <input type="hidden" id="amount"/>
  <input value="test-content/Audio_OGG-1.OGG" type="hidden" id="main-audio-content"/>
</div>
<div id="audio-content"></div>
```

**Question Types Available (10):**
1. Fill in the gaps
2. Fill in the gaps short answers
3. Flow-chart Completion
4. Form Completion
5. Labelling on a map
6. Matching
7. Multiple Choice (more than one answer)
8. Multiple Choice (one answer)
9. Sentence Completion
10. Table Completion

#### Reading Interface (reading.xhtml)
**No audio controls** (as reading tests don't require audio)

**Question Types Available (12):**
1. Flow-chart Completion (selecting words from the text)
2. Identifying Information (True/False/Not Given)
3. Matching Features
4. Matching Headings
5. Matching Sentence Endings
6. Multiple choice with more than one answer
7. Multiple choice with one answer
8. Note Completion
9. Sentence Completion
10. Summary Completion (selecting from a list of words or phrases)
11. Summary Completion (selecting words from the text)
12. Table Completion

#### Writing Interface (writing.xhtml)
**No audio controls** (as writing tests don't require audio)

**Tasks Available (2):**
1. Writing Part 1
2. Writing Part 2

## How It Works

### Navigation Flow
1. User opens **index.html** and sees three test type options
2. User clicks on their desired test type (Listening, Reading, or Writing)
3. The corresponding interface file (.xhtml) loads with:
   - Full navigation showing all available question types
   - Appropriate controls (with/without audio based on test type)
   - Dynamic content area ready to load specific questions

### Dynamic Content Loading
Each interface file includes links to the actual question content stored in their respective folders:
- Listening → `/app/Listening/[Question Type]/index.xhtml`
- Reading → `/app/Reading/[Question Type]/index.xhtml`
- Writing → `/app/Writing/[Writing Part]/index.xhtml`

## Technical Details

### CSS Dependencies
All interfaces link to standard CSS files:
- jquery-ui.css
- base.css
- access.css
- banner.css
- navigation.css
- tools.css
- main.css
- item.css
- calc.css
- chart.css
- notepad.css
- instructions.css
- jquery.contextMenu.css
- custom.css

### JavaScript Dependencies
All interfaces include:
- jQuery and jQuery UI
- QTI framework
- Audio player (for Listening)
- Rangy libraries for text selection
- Various utility scripts

### Time Limits
- **Listening:** 342 seconds (5.7 minutes)
- **Reading:** 1800 seconds (30 minutes)
- **Writing:** 3600 seconds (60 minutes)

## Key Features

### 1. Accessibility
- Proper ARIA labels
- Reader-only spans for screen readers
- Keyboard navigation support

### 2. Responsive Design
- Uses existing responsive CSS from question type folders
- Adapts to different screen sizes

### 3. Consistent User Experience
- Same header/footer across all test types
- Familiar navigation patterns
- Consistent branding (IELTS logos)

### 4. Help & Instructions
- Built-in help system via Help button
- Instructions accessible within interface
- Settings for customization

## Usage Instructions

### For Test Takers:
1. Open `index.html` in a web browser
2. Select your test type (Listening, Reading, or Writing)
3. Use the navigation bar to access different question types
4. For Listening tests, use the volume control slider to adjust audio
5. Use Previous/Next buttons to navigate between questions
6. Mark questions for review using the Review checkbox

### For Developers:
- Original question type folders remain intact in `/app/Listening/`, `/app/Reading/`, and `/app/Writing/`
- New consolidated interfaces reference these existing files
- Modify CSS/JS in original question folders to affect all interfaces
- Update navigation links in interface files to add/remove question types

## Benefits of This Structure

1. **Unified Interface:** Consistent look and feel across all test types
2. **Easy Navigation:** All question types accessible from one place
3. **Type-Specific Features:** Audio controls only where needed (Listening)
4. **Maintainability:** Central interface files make updates easier
5. **Backward Compatibility:** Original question files remain unchanged
6. **Scalability:** Easy to add new question types by updating navigation

## Future Enhancements

Possible improvements:
- Add breadcrumb navigation
- Implement progress tracking
- Add test completion summary
- Include answer submission functionality
- Add practice vs. actual test modes
- Implement responsive mobile-first design updates

---

**Last Updated:** October 18, 2024
**Version:** 1.0
