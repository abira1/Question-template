# 🚀 Complete Integration Plan for IELTS Website

## Overview
This document provides a step-by-step plan to integrate the IELTS exam interface, question types, and features (notes, highlighting, audio control, etc.) into your existing website.

---

## 📊 Current IELTS Features Available

### 1. **Interface Components**
- ✅ Header with IELTS branding
- ✅ Candidate information display
- ✅ Timer system
- ✅ Audio player with volume control (Listening only)
- ✅ Settings, Help, Hide buttons
- ✅ Navigation bar with question links
- ✅ Review checkbox
- ✅ Previous/Next navigation

### 2. **Question Features**
- ✅ **Text Highlighting** - Users can select and highlight text
- ✅ **Notes System** - Draggable sticky notes
- ✅ **Audio Playback** - For listening tests with volume control
- ✅ **Multiple Question Types** - 24 different formats
- ✅ **Form Validation** - Answer validation
- ✅ **Timer Management** - Test time limits
- ✅ **Review System** - Mark questions for review
- ✅ **Instructions** - Pre-test instructions

### 3. **Question Type Categories**

#### **Listening (10 Types)**
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

#### **Reading (12 Types)**
1. Flow-chart Completion (selecting words from text)
2. Identifying Information (True/False/Not Given)
3. Matching Features
4. Matching Headings
5. Matching Sentence Endings
6. Multiple choice with more than one answer
7. Multiple choice with one answer
8. Note Completion
9. Sentence Completion
10. Summary Completion (list selection)
11. Summary Completion (text selection)
12. Table Completion

#### **Writing (2 Types)**
1. Writing Part 1
2. Writing Part 2

---

## 🎯 Integration Strategy

### Phase 1: Architecture Planning

#### Step 1.1: Understand Your Current Tech Stack
```
Questions to answer:
- What framework? (React, Vue, Angular, Plain JS?)
- Backend? (Node.js, Python, PHP?)
- Database? (MongoDB, MySQL, PostgreSQL?)
- Authentication system?
```

#### Step 1.2: Define JSON Structure for Admin Panel
Create a standardized JSON format that your AI (DeepSeek) should generate from PDFs:

```json
{
  "exam": {
    "id": "unique-exam-id",
    "type": "listening|reading|writing",
    "title": "IELTS Sample Listening Test 1",
    "duration": 1800,
    "instructions": {
      "title": "IELTS Listening",
      "time": "Approximately 30 minutes",
      "candidateInstructions": [
        "Answer all the questions",
        "You can change your answers at any time during the test"
      ],
      "information": [
        "There are 40 questions in this test",
        "Each question carries one mark"
      ]
    },
    "questions": [
      {
        "questionId": "q1",
        "questionNumber": 1,
        "questionType": "fill-in-gaps|mcq-single|mcq-multiple|matching|true-false|etc",
        "section": "Part 1",
        "instructions": "Complete the notes. Write ONE WORD in each gap.",
        "audioFile": "audio/listening-part1.mp3", // Only for listening
        "content": {
          "text": "Phone call about second-hand furniture",
          "table": [
            {
              "row": 1,
              "cells": [
                {"type": "label", "content": "Dining table"},
                {"type": "input", "questionNum": 1, "correctAnswer": "round"}
              ]
            }
          ]
        },
        "answers": [
          {
            "id": "q1-answer",
            "type": "text-input",
            "correctAnswer": "round",
            "maxLength": 10,
            "placeholder": ""
          }
        ],
        "marks": 1
      }
    ]
  }
}
```

---

### Phase 2: Frontend Implementation

#### Step 2.1: Create Component Structure

**Component Hierarchy:**
```
ExamInterface/
├── Header/
│   ├── Logo.jsx
│   └── PartnerLogos.jsx
├── TestBanner/
│   ├── CandidateInfo.jsx
│   ├── Timer.jsx
│   ├── AudioControl.jsx (conditional - listening only)
│   └── ActionButtons.jsx (Settings, Help, Hide)
├── Navigation/
│   ├── QuestionNavigation.jsx
│   └── ViewToggle.jsx (Summary/Details)
├── MainContent/
│   ├── QuestionRenderer.jsx
│   ├── QuestionTypes/
│   │   ├── FillInGaps.jsx
│   │   ├── MultipleChoice.jsx
│   │   ├── Matching.jsx
│   │   ├── TrueFalse.jsx
│   │   ├── TableCompletion.jsx
│   │   └── ... (all 24 types)
│   └── Instructions.jsx
├── Footer/
│   ├── ReviewCheckbox.jsx
│   └── NavigationButtons.jsx (Previous/Next)
└── Features/
    ├── NotesSystem.jsx
    ├── TextHighlighter.jsx
    └── HelpModal.jsx
```

#### Step 2.2: Implement Core Features

##### **A. Text Highlighting System**
```javascript
// TextHighlighter.jsx
import React, { useEffect } from 'react';

const TextHighlighter = ({ contentRef }) => {
  useEffect(() => {
    const setupHighlighting = () => {
      const content = contentRef.current;
      if (!content) return;

      // Add context menu for highlighting
      content.addEventListener('mouseup', handleTextSelection);
      
      return () => {
        content.removeEventListener('mouseup', handleTextSelection);
      };
    };

    const handleTextSelection = () => {
      const selection = window.getSelection();
      const selectedText = selection.toString().trim();
      
      if (selectedText.length > 0) {
        showHighlightMenu(selection);
      }
    };

    const showHighlightMenu = (selection) => {
      // Create context menu with highlight colors
      const colors = ['yellow', 'green', 'blue', 'pink'];
      // Show menu at cursor position
      // Apply highlighting on color selection
    };

    setupHighlighting();
  }, [contentRef]);

  return null; // This is a functional component without UI
};

export default TextHighlighter;
```

**CSS for Highlighting:**
```css
.highlighted-text {
  position: relative;
  padding: 2px 0;
}

.highlighted-text.yellow {
  background-color: rgba(255, 255, 0, 0.3);
}

.highlighted-text.green {
  background-color: rgba(0, 255, 0, 0.2);
}

.highlighted-text.blue {
  background-color: rgba(0, 100, 255, 0.2);
}

.highlighted-text.pink {
  background-color: rgba(255, 192, 203, 0.4);
}
```

##### **B. Notes System**
```javascript
// NotesSystem.jsx
import React, { useState, useRef } from 'react';
import './NotesSystem.css';

const NotesSystem = () => {
  const [notes, setNotes] = useState([]);
  const [activeNote, setActiveNote] = useState(null);
  const noteIdCounter = useRef(0);

  const createNote = (x, y, highlightedText = '') => {
    const newNote = {
      id: noteIdCounter.current++,
      x: x,
      y: y,
      text: '',
      highlightedText: highlightedText,
      zIndex: 500 + noteIdCounter.current
    };
    
    setNotes([...notes, newNote]);
    setActiveNote(newNote.id);
  };

  const updateNote = (id, text) => {
    setNotes(notes.map(note => 
      note.id === id ? { ...note, text } : note
    ));
  };

  const deleteNote = (id) => {
    setNotes(notes.filter(note => note.id !== id));
  };

  const moveNote = (id, x, y) => {
    setNotes(notes.map(note =>
      note.id === id ? { ...note, x, y } : note
    ));
  };

  return (
    <div className="notes-container">
      {notes.map(note => (
        <DraggableNote
          key={note.id}
          note={note}
          onUpdate={updateNote}
          onDelete={deleteNote}
          onMove={moveNote}
          isActive={activeNote === note.id}
          setActive={() => setActiveNote(note.id)}
        />
      ))}
      <button 
        className="add-note-btn"
        onClick={() => createNote(100, 100)}
      >
        ➕ Add Note
      </button>
    </div>
  );
};

const DraggableNote = ({ note, onUpdate, onDelete, onMove, isActive, setActive }) => {
  const [isDragging, setIsDragging] = useState(false);
  const [dragOffset, setDragOffset] = useState({ x: 0, y: 0 });
  const noteRef = useRef(null);

  const handleMouseDown = (e) => {
    if (e.target.classList.contains('draghandle')) {
      setIsDragging(true);
      setDragOffset({
        x: e.clientX - note.x,
        y: e.clientY - note.y
      });
      setActive();
    }
  };

  const handleMouseMove = (e) => {
    if (isDragging) {
      onMove(note.id, e.clientX - dragOffset.x, e.clientY - dragOffset.y);
    }
  };

  const handleMouseUp = () => {
    setIsDragging(false);
  };

  useEffect(() => {
    if (isDragging) {
      document.addEventListener('mousemove', handleMouseMove);
      document.addEventListener('mouseup', handleMouseUp);
      return () => {
        document.removeEventListener('mousemove', handleMouseMove);
        document.removeEventListener('mouseup', handleMouseUp);
      };
    }
  }, [isDragging]);

  return (
    <div
      ref={noteRef}
      className={`note ${isActive ? 'active' : ''}`}
      style={{
        left: `${note.x}px`,
        top: `${note.y}px`,
        zIndex: note.zIndex
      }}
      onMouseDown={handleMouseDown}
    >
      <div className="close" onClick={() => onDelete(note.id)}>✕</div>
      <div className="draghandle">≡</div>
      <div className="edit">
        {note.highlightedText && (
          <div className="highlightText">{note.highlightedText}</div>
        )}
        <textarea
          className="mainText"
          value={note.text}
          onChange={(e) => onUpdate(note.id, e.target.value)}
          placeholder="Type your note here..."
        />
      </div>
    </div>
  );
};

export default NotesSystem;
```

**CSS for Notes:**
```css
.notes-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.note {
  position: absolute;
  width: 200px;
  min-height: 150px;
  background: #feff9c;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.3);
  padding: 10px;
  cursor: default;
  font-family: Arial, sans-serif;
}

.note.active {
  box-shadow: 3px 3px 15px rgba(0, 0, 0, 0.5);
}

.note .close {
  position: absolute;
  top: 5px;
  right: 5px;
  cursor: pointer;
  font-size: 16px;
  color: #888;
}

.note .close:hover {
  color: #000;
}

.note .draghandle {
  cursor: move;
  text-align: center;
  padding: 5px;
  background: #f0f0f0;
  margin: -10px -10px 10px -10px;
  border-radius: 5px 5px 0 0;
  font-weight: bold;
}

.note .highlightText {
  background: #e0e0e0;
  padding: 5px;
  margin-bottom: 10px;
  border-radius: 3px;
  font-size: 12px;
  font-style: italic;
}

.note textarea {
  width: 100%;
  min-height: 80px;
  border: none;
  background: transparent;
  resize: none;
  font-size: 14px;
  outline: none;
}

.add-note-btn {
  position: fixed;
  bottom: 100px;
  right: 30px;
  background: #4CAF50;
  color: white;
  border: none;
  padding: 15px 20px;
  border-radius: 50px;
  cursor: pointer;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.2);
  font-size: 16px;
  z-index: 1000;
}

.add-note-btn:hover {
  background: #45a049;
}
```

##### **C. Audio Control (Listening Only)**
```javascript
// AudioControl.jsx
import React, { useState, useRef, useEffect } from 'react';
import './AudioControl.css';

const AudioControl = ({ audioSrc, autoPlay = false }) => {
  const [volume, setVolume] = useState(50);
  const [isPlaying, setIsPlaying] = useState(false);
  const [currentTime, setCurrentTime] = useState(0);
  const [duration, setDuration] = useState(0);
  const audioRef = useRef(null);

  useEffect(() => {
    const audio = audioRef.current;
    if (!audio) return;

    const updateTime = () => setCurrentTime(audio.currentTime);
    const updateDuration = () => setDuration(audio.duration);
    const handleEnded = () => setIsPlaying(false);

    audio.addEventListener('timeupdate', updateTime);
    audio.addEventListener('loadedmetadata', updateDuration);
    audio.addEventListener('ended', handleEnded);

    return () => {
      audio.removeEventListener('timeupdate', updateTime);
      audio.removeEventListener('loadedmetadata', updateDuration);
      audio.removeEventListener('ended', handleEnded);
    };
  }, []);

  useEffect(() => {
    if (audioRef.current) {
      audioRef.current.volume = volume / 100;
    }
  }, [volume]);

  const togglePlayPause = () => {
    const audio = audioRef.current;
    if (isPlaying) {
      audio.pause();
    } else {
      audio.play();
    }
    setIsPlaying(!isPlaying);
  };

  const formatTime = (time) => {
    const minutes = Math.floor(time / 60);
    const seconds = Math.floor(time % 60);
    return `${minutes}:${seconds.toString().padStart(2, '0')}`;
  };

  return (
    <div className="audio-control">
      <audio ref={audioRef} src={audioSrc} />
      
      <div className="audio-controls">
        <button onClick={togglePlayPause} className="play-pause-btn">
          {isPlaying ? '⏸' : '▶'}
        </button>
        
        <div className="time-display">
          {formatTime(currentTime)} / {formatTime(duration)}
        </div>
        
        <div className="volume-control">
          <span className="volume-icon">🔊</span>
          <input
            type="range"
            min="0"
            max="100"
            value={volume}
            onChange={(e) => setVolume(e.target.value)}
            className="volume-slider"
          />
          <span className="volume-value">{volume}%</span>
        </div>
      </div>
    </div>
  );
};

export default AudioControl;
```

**CSS for Audio Control:**
```css
.audio-control {
  background: #f5f5f5;
  padding: 15px;
  border-radius: 8px;
  margin: 10px 0;
}

.audio-controls {
  display: flex;
  align-items: center;
  gap: 15px;
}

.play-pause-btn {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: #667eea;
  color: white;
  border: none;
  font-size: 20px;
  cursor: pointer;
  transition: background 0.3s;
}

.play-pause-btn:hover {
  background: #5568d3;
}

.time-display {
  font-size: 14px;
  color: #333;
  min-width: 100px;
}

.volume-control {
  display: flex;
  align-items: center;
  gap: 10px;
  flex: 1;
}

.volume-slider {
  flex: 1;
  height: 5px;
  border-radius: 5px;
  background: #ddd;
  outline: none;
  -webkit-appearance: none;
}

.volume-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #667eea;
  cursor: pointer;
}

.volume-slider::-moz-range-thumb {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #667eea;
  cursor: pointer;
  border: none;
}

.volume-value {
  font-size: 12px;
  color: #666;
  min-width: 40px;
}
```

##### **D. Timer Component**
```javascript
// Timer.jsx
import React, { useState, useEffect } from 'react';
import './Timer.css';

const Timer = ({ initialTime, onTimeUp }) => {
  const [timeLeft, setTimeLeft] = useState(initialTime);
  const [isRunning, setIsRunning] = useState(true);

  useEffect(() => {
    if (!isRunning || timeLeft <= 0) return;

    const timer = setInterval(() => {
      setTimeLeft(prev => {
        if (prev <= 1) {
          setIsRunning(false);
          if (onTimeUp) onTimeUp();
          return 0;
        }
        return prev - 1;
      });
    }, 1000);

    return () => clearInterval(timer);
  }, [isRunning, timeLeft, onTimeUp]);

  const formatTime = (seconds) => {
    const mins = Math.floor(seconds / 60);
    const secs = seconds % 60;
    return `${mins}:${secs.toString().padStart(2, '0')}`;
  };

  const getWarningClass = () => {
    if (timeLeft < 300) return 'warning-critical'; // < 5 minutes
    if (timeLeft < 600) return 'warning-medium'; // < 10 minutes
    return '';
  };

  return (
    <div className={`timer ${getWarningClass()}`}>
      <span className="timer-label">Time:</span>
      <span className="timer-value">{formatTime(timeLeft)}</span>
      <span className="timer-unit">minutes left</span>
    </div>
  );
};

export default Timer;
```

---

### Phase 3: Question Type Renderers

#### Step 3.1: Create Question Type Components

**Example: Fill in the Gaps**
```javascript
// QuestionTypes/FillInGaps.jsx
import React, { useState } from 'react';
import './FillInGaps.css';

const FillInGaps = ({ questionData, onAnswerChange }) => {
  const [answers, setAnswers] = useState({});

  const handleInputChange = (questionId, value) => {
    const newAnswers = { ...answers, [questionId]: value };
    setAnswers(newAnswers);
    onAnswerChange(questionId, value);
  };

  return (
    <div className="fill-in-gaps-question">
      <div className="question-instructions">
        {questionData.instructions}
      </div>
      
      <div className="question-content">
        {questionData.content.type === 'table' ? (
          <table className="question-table">
            <tbody>
              {questionData.content.rows.map((row, rowIndex) => (
                <tr key={rowIndex}>
                  {row.cells.map((cell, cellIndex) => (
                    <td key={cellIndex}>
                      {cell.type === 'label' ? (
                        <span>{cell.content}</span>
                      ) : cell.type === 'input' ? (
                        <div className="input-container">
                          <span className="question-number">{cell.questionNum}</span>
                          <input
                            type="text"
                            maxLength={cell.maxLength || 50}
                            value={answers[cell.questionId] || ''}
                            onChange={(e) => handleInputChange(cell.questionId, e.target.value)}
                            placeholder={cell.placeholder || ''}
                            data-testid={`answer-${cell.questionId}`}
                          />
                        </div>
                      ) : (
                        <span>{cell.content}</span>
                      )}
                    </td>
                  ))}
                </tr>
              ))}
            </tbody>
          </table>
        ) : (
          <div dangerouslySetInnerHTML={{ __html: questionData.content.html }} />
        )}
      </div>
    </div>
  );
};

export default FillInGaps;
```

**Example: Multiple Choice (Single Answer)**
```javascript
// QuestionTypes/MultipleChoiceSingle.jsx
import React, { useState } from 'react';
import './MultipleChoice.css';

const MultipleChoiceSingle = ({ questionData, onAnswerChange }) => {
  const [selectedAnswer, setSelectedAnswer] = useState(null);

  const handleSelect = (optionId) => {
    setSelectedAnswer(optionId);
    onAnswerChange(questionData.id, optionId);
  };

  return (
    <div className="mcq-single-question">
      <div className="question-text">
        {questionData.question}
      </div>
      
      <div className="options-container">
        {questionData.options.map((option, index) => (
          <div
            key={option.id}
            className={`option ${selectedAnswer === option.id ? 'selected' : ''}`}
            onClick={() => handleSelect(option.id)}
          >
            <input
              type="radio"
              name={`question-${questionData.id}`}
              id={option.id}
              checked={selectedAnswer === option.id}
              onChange={() => handleSelect(option.id)}
            />
            <label htmlFor={option.id}>
              <span className="option-letter">{String.fromCharCode(65 + index)}</span>
              <span className="option-text">{option.text}</span>
            </label>
          </div>
        ))}
      </div>
    </div>
  );
};

export default MultipleChoiceSingle;
```

**Example: True/False/Not Given**
```javascript
// QuestionTypes/TrueFalseNotGiven.jsx
import React, { useState } from 'react';
import './TrueFalse.css';

const TrueFalseNotGiven = ({ questionData, onAnswerChange }) => {
  const [answers, setAnswers] = useState({});

  const handleSelect = (statementId, value) => {
    const newAnswers = { ...answers, [statementId]: value };
    setAnswers(newAnswers);
    onAnswerChange(statementId, value);
  };

  return (
    <div className="true-false-question">
      <div className="passage">
        {questionData.passage}
      </div>
      
      <div className="instructions">
        Do the following statements agree with the information given in the text?
      </div>
      
      <div className="statements">
        {questionData.statements.map((statement) => (
          <div key={statement.id} className="statement-row">
            <div className="statement-number">{statement.number}</div>
            <div className="statement-text">{statement.text}</div>
            <div className="statement-options">
              {['TRUE', 'FALSE', 'NOT GIVEN'].map((option) => (
                <button
                  key={option}
                  className={`option-btn ${answers[statement.id] === option ? 'selected' : ''}`}
                  onClick={() => handleSelect(statement.id, option)}
                >
                  {option}
                </button>
              ))}
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

export default TrueFalseNotGiven;
```

---

### Phase 4: Backend Implementation

#### Step 4.1: Create API Endpoints

```javascript
// Node.js/Express Example

// routes/exams.js
const express = require('express');
const router = express.Router();
const Exam = require('../models/Exam');
const Question = require('../models/Question');

// Get all exams
router.get('/exams', async (req, res) => {
  try {
    const exams = await Exam.find().select('id title type duration');
    res.json(exams);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Get specific exam with questions
router.get('/exams/:id', async (req, res) => {
  try {
    const exam = await Exam.findById(req.params.id).populate('questions');
    if (!exam) {
      return res.status(404).json({ error: 'Exam not found' });
    }
    res.json(exam);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Import exam from JSON (Admin Panel)
router.post('/admin/import-exam', async (req, res) => {
  try {
    const examData = req.body;
    
    // Validate JSON structure
    if (!examData.exam || !examData.exam.questions) {
      return res.status(400).json({ error: 'Invalid JSON structure' });
    }
    
    // Create exam
    const exam = new Exam({
      title: examData.exam.title,
      type: examData.exam.type,
      duration: examData.exam.duration,
      instructions: examData.exam.instructions
    });
    
    await exam.save();
    
    // Create questions
    const questions = await Promise.all(
      examData.exam.questions.map(async (q) => {
        const question = new Question({
          examId: exam._id,
          questionNumber: q.questionNumber,
          questionType: q.questionType,
          content: q.content,
          answers: q.answers,
          audioFile: q.audioFile
        });
        return question.save();
      })
    );
    
    exam.questions = questions.map(q => q._id);
    await exam.save();
    
    res.json({ 
      success: true, 
      examId: exam._id,
      message: 'Exam imported successfully'
    });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Submit answers
router.post('/exams/:id/submit', async (req, res) => {
  try {
    const { answers, timeSpent } = req.body;
    const exam = await Exam.findById(req.params.id).populate('questions');
    
    // Calculate score
    let score = 0;
    const results = [];
    
    for (const question of exam.questions) {
      const userAnswer = answers[question._id];
      const isCorrect = checkAnswer(question, userAnswer);
      
      if (isCorrect) score += question.marks || 1;
      
      results.push({
        questionId: question._id,
        userAnswer,
        correctAnswer: question.answers[0].correctAnswer,
        isCorrect
      });
    }
    
    res.json({
      score,
      totalQuestions: exam.questions.length,
      results,
      timeSpent
    });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

function checkAnswer(question, userAnswer) {
  // Implement answer checking logic based on question type
  const correctAnswer = question.answers[0].correctAnswer;
  
  if (question.questionType.includes('fill-in')) {
    // Case-insensitive comparison for text answers
    return userAnswer.toLowerCase().trim() === correctAnswer.toLowerCase().trim();
  } else if (question.questionType.includes('mcq')) {
    return userAnswer === correctAnswer;
  }
  // Add more question type checks...
  
  return false;
}

module.exports = router;
```

#### Step 4.2: Database Models

```javascript
// models/Exam.js
const mongoose = require('mongoose');

const examSchema = new mongoose.Schema({
  title: { type: String, required: true },
  type: { 
    type: String, 
    enum: ['listening', 'reading', 'writing'], 
    required: true 
  },
  duration: { type: Number, required: true }, // in seconds
  instructions: {
    title: String,
    time: String,
    candidateInstructions: [String],
    information: [String]
  },
  questions: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Question' }],
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});

module.exports = mongoose.model('Exam', examSchema);

// models/Question.js
const questionSchema = new mongoose.Schema({
  examId: { type: mongoose.Schema.Types.ObjectId, ref: 'Exam', required: true },
  questionNumber: { type: Number, required: true },
  questionType: { type: String, required: true },
  section: String,
  instructions: String,
  audioFile: String,
  content: mongoose.Schema.Types.Mixed, // Flexible structure
  answers: [{
    id: String,
    type: String,
    correctAnswer: mongoose.Schema.Types.Mixed,
    maxLength: Number,
    placeholder: String
  }],
  marks: { type: Number, default: 1 }
});

module.exports = mongoose.model('Question', questionSchema);
```

---

### Phase 5: AI Integration for PDF to JSON

#### Step 5.1: DeepSeek Prompt Template

```markdown
Convert the following IELTS exam PDF to JSON format. Follow this exact structure:

{
  "exam": {
    "id": "generate-unique-id",
    "type": "listening|reading|writing",
    "title": "Extract title from PDF",
    "duration": 1800,
    "instructions": {
      "title": "Extract main title",
      "time": "Extract time information",
      "candidateInstructions": ["Extract all bullet points"],
      "information": ["Extract all information points"]
    },
    "questions": [
      {
        "questionId": "q1",
        "questionNumber": 1,
        "questionType": "identify from: fill-in-gaps, mcq-single, mcq-multiple, matching, true-false, table-completion, sentence-completion, note-completion, summary-completion, flow-chart, matching-headings, matching-features, matching-endings, map-labelling, form-completion",
        "section": "Extract section name if present",
        "instructions": "Extract question-specific instructions",
        "audioFile": "audio-filename.mp3 (if listening test)",
        "content": {
          // Structure based on question type
          // For tables: include rows and cells
          // For text: include formatted text
          // For passages: include full passage
        },
        "answers": [
          {
            "id": "answer-id",
            "type": "text-input|radio|checkbox|dropdown",
            "correctAnswer": "extract correct answer",
            "maxLength": 10,
            "placeholder": ""
          }
        ],
        "marks": 1
      }
    ]
  }
}

Rules:
1. Preserve exact question numbering from PDF
2. Identify question types accurately
3. Extract all answer options for MCQ questions
4. For fill-in-gaps, identify correct answers from answer key
5. Include audio filenames for listening tests
6. Maintain formatting (bold, italic, tables)
7. Extract instructions precisely
```

---

### Phase 6: Testing & Deployment

#### Step 6.1: Testing Checklist

- [ ] Test each question type renders correctly
- [ ] Test highlighting feature on different browsers
- [ ] Test notes system (create, move, delete)
- [ ] Test audio playback and volume control (listening)
- [ ] Test timer countdown and time-up alerts
- [ ] Test navigation (previous/next questions)
- [ ] Test review checkbox functionality
- [ ] Test answer submission and scoring
- [ ] Test JSON import in admin panel
- [ ] Test responsive design on mobile devices
- [ ] Test accessibility features
- [ ] Load testing with multiple simultaneous users

#### Step 6.2: Performance Optimization

1. **Lazy load questions** - Load one question at a time
2. **Audio preloading** - Preload next audio file
3. **Image optimization** - Compress images for maps/diagrams
4. **Code splitting** - Split by question type
5. **Caching** - Cache exam data on client side

---

## 📋 Implementation Checklist

### Week 1: Foundation
- [ ] Set up project structure
- [ ] Create component hierarchy
- [ ] Implement Header and Footer
- [ ] Set up API routes
- [ ] Create database models

### Week 2: Core Features
- [ ] Implement Timer component
- [ ] Implement Audio Control
- [ ] Create Notes System
- [ ] Create Text Highlighter
- [ ] Build Navigation system

### Week 3: Question Types
- [ ] Implement 5 most common question types
- [ ] Test question rendering
- [ ] Implement answer validation
- [ ] Create question type factory

### Week 4: Integration
- [ ] Connect frontend to backend
- [ ] Implement JSON import
- [ ] Test full flow (import → take test → submit)
- [ ] Add admin panel features

### Week 5: Polish
- [ ] Fix bugs
- [ ] Optimize performance
- [ ] Add responsive design
- [ ] User testing
- [ ] Deploy

---

## 🎓 Next Steps for You

1. **Share your tech stack details** - Framework, backend, database
2. **Review the JSON structure** - Confirm it matches your needs
3. **Test the AI conversion** - Try converting one PDF with DeepSeek
4. **Start with one question type** - Implement Fill-in-Gaps first
5. **Ask specific questions** - I can provide detailed code for any part

Would you like me to:
- Create detailed code for a specific question type?
- Help with the backend API structure?
- Design the admin panel UI?
- Create the AI prompt for PDF conversion?

Let me know which part you want to tackle first! 🚀
