# 📄 Complete JSON Structure Guide for IELTS Exam Import

## Overview
This guide provides detailed JSON structures for all 24 IELTS question types. Use this as a reference when converting PDFs to JSON using AI (DeepSeek).

---

## Base Exam Structure

```json
{
  "exam": {
    "id": "unique-exam-identifier",
    "type": "listening|reading|writing",
    "title": "IELTS Sample Test 1",
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
    "questions": []
  }
}
```

---

## Question Type Structures

### 1. Fill in the Gaps (Table Format)

```json
{
  "questionId": "q1-7",
  "questionNumber": "1-7",
  "questionType": "fill-in-gaps-table",
  "section": "Part 1",
  "instructions": "Complete the notes. Write ONE WORD AND/OR A NUMBER in each gap.",
  "audioFile": "audio/listening-part1.mp3",
  "content": {
    "type": "table",
    "title": "Phone call about second-hand furniture",
    "rows": [
      {
        "rowType": "header",
        "cells": [
          {"type": "label", "content": "Items", "colspan": 1},
          {"type": "label", "content": "Details", "colspan": 1}
        ]
      },
      {
        "rowType": "data",
        "cells": [
          {"type": "label", "content": "Dining table"},
          {"type": "mixed", "content": [
            {"type": "text", "value": "- "},
            {"type": "input", "questionNum": 1, "questionId": "q1", "maxLength": 10},
            {"type": "text", "value": " shape"}
          ]}
        ]
      },
      {
        "rowType": "data",
        "cells": [
          {"type": "label", "content": ""},
          {"type": "mixed", "content": [
            {"type": "text", "value": "- medium size"}
          ]}
        ]
      },
      {
        "rowType": "data",
        "cells": [
          {"type": "label", "content": ""},
          {"type": "mixed", "content": [
            {"type": "text", "value": "- "},
            {"type": "input", "questionNum": 2, "questionId": "q2", "maxLength": 10},
            {"type": "text", "value": " old"}
          ]}
        ]
      }
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "round", "acceptableAnswers": ["circular"]},
    {"questionId": "q2", "correctAnswer": "20", "acceptableAnswers": ["twenty", "20 years"]}
  ]
}
```

### 2. Multiple Choice (Single Answer)

```json
{
  "questionId": "q1",
  "questionNumber": 1,
  "questionType": "mcq-single",
  "section": "Part 2",
  "instructions": "Choose the correct letter, A, B, C or D.",
  "audioFile": "audio/listening-part2.mp3",
  "content": {
    "question": "What is the main topic of the lecture?",
    "options": [
      {"id": "A", "text": "Environmental conservation"},
      {"id": "B", "text": "Urban development"},
      {"id": "C", "text": "Economic growth"},
      {"id": "D", "text": "Social welfare"}
    ]
  },
  "answers": [
    {"correctAnswer": "A"}
  ]
}
```

### 3. Multiple Choice (Multiple Answers)

```json
{
  "questionId": "q1-2",
  "questionNumber": "1-2",
  "questionType": "mcq-multiple",
  "section": "Part 3",
  "instructions": "Choose TWO letters, A-E.",
  "audioFile": "audio/listening-part3.mp3",
  "content": {
    "question": "Which TWO factors does the speaker mention about climate change?",
    "selectCount": 2,
    "options": [
      {"id": "A", "text": "Rising sea levels"},
      {"id": "B", "text": "Increased rainfall"},
      {"id": "C", "text": "Higher temperatures"},
      {"id": "D", "text": "Stronger winds"},
      {"id": "E", "text": "More frequent storms"}
    ]
  },
  "answers": [
    {"correctAnswers": ["A", "C"]}
  ]
}
```

### 4. Matching

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "matching",
  "section": "Part 4",
  "instructions": "Match each statement with the correct person.",
  "audioFile": "audio/listening-part4.mp3",
  "content": {
    "statements": [
      {"id": "q1", "number": 1, "text": "Prefers morning exercise"},
      {"id": "q2", "number": 2, "text": "Likes team sports"},
      {"id": "q3", "number": 3, "text": "Enjoys swimming"},
      {"id": "q4", "number": 4, "text": "Practices yoga regularly"},
      {"id": "q5", "number": 5, "text": "Goes to the gym daily"}
    ],
    "options": [
      {"id": "A", "text": "John"},
      {"id": "B", "text": "Mary"},
      {"id": "C", "text": "Peter"},
      {"id": "D", "text": "Sarah"},
      {"id": "E", "text": "David"}
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "B"},
    {"questionId": "q2", "correctAnswer": "C"},
    {"questionId": "q3", "correctAnswer": "D"},
    {"questionId": "q4", "correctAnswer": "A"},
    {"questionId": "q5", "correctAnswer": "E"}
  ]
}
```

### 5. True/False/Not Given

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "true-false-not-given",
  "section": "Reading Passage 1",
  "instructions": "Do the following statements agree with the information given in the text? Write TRUE, FALSE or NOT GIVEN.",
  "content": {
    "passage": "The Amazon rainforest is the largest tropical rainforest in the world, covering approximately 5.5 million square kilometers. It spans across nine countries in South America, with Brazil containing about 60% of the forest...",
    "statements": [
      {"id": "q1", "number": 1, "text": "The Amazon rainforest covers more than 5 million square kilometers."},
      {"id": "q2", "number": 2, "text": "Brazil has the largest portion of the Amazon rainforest."},
      {"id": "q3", "number": 3, "text": "The Amazon rainforest is increasing in size."},
      {"id": "q4", "number": 4, "text": "Nine countries share the Amazon rainforest."},
      {"id": "q5", "number": 5, "text": "The rainforest produces 50% of the world's oxygen."}
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "TRUE"},
    {"questionId": "q2", "correctAnswer": "TRUE"},
    {"questionId": "q3", "correctAnswer": "NOT GIVEN"},
    {"questionId": "q4", "correctAnswer": "TRUE"},
    {"questionId": "q5", "correctAnswer": "NOT GIVEN"}
  ]
}
```

### 6. Sentence Completion

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "sentence-completion",
  "section": "Reading Passage 2",
  "instructions": "Complete the sentences below. Choose NO MORE THAN TWO WORDS from the passage for each answer.",
  "content": {
    "passage": "Renewable energy sources such as solar and wind power are becoming increasingly popular...",
    "sentences": [
      {
        "id": "q1",
        "number": 1,
        "template": "Solar panels convert sunlight into {input} energy.",
        "maxWords": 2
      },
      {
        "id": "q2",
        "number": 2,
        "template": "Wind turbines are most effective in areas with {input} wind speeds.",
        "maxWords": 2
      },
      {
        "id": "q3",
        "number": 3,
        "template": "Renewable energy reduces dependence on {input}.",
        "maxWords": 2
      }
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "electrical", "acceptableAnswers": ["electric"]},
    {"questionId": "q2", "correctAnswer": "high", "acceptableAnswers": ["strong", "consistent"]},
    {"questionId": "q3", "correctAnswer": "fossil fuels", "acceptableAnswers": ["non-renewable energy"]}
  ]
}
```

### 7. Summary Completion (From List)

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "summary-completion-list",
  "section": "Reading Passage 3",
  "instructions": "Complete the summary below. Choose NO MORE THAN TWO WORDS from the box for each answer.",
  "content": {
    "summary": "The Industrial Revolution began in {q1} during the 18th century. It transformed society through the development of {q2} and new manufacturing processes. The introduction of {q3} revolutionized transportation, while the textile industry benefited from the {q4}. These changes led to significant {q5} growth.",
    "wordBox": [
      "Britain", "steam engine", "spinning jenny", "economic", 
      "factories", "railways", "urban", "agricultural"
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "Britain"},
    {"questionId": "q2", "correctAnswer": "factories"},
    {"questionId": "q3", "correctAnswer": "steam engine"},
    {"questionId": "q4", "correctAnswer": "spinning jenny"},
    {"questionId": "q5", "correctAnswer": "economic"}
  ]
}
```

### 8. Summary Completion (From Text)

```json
{
  "questionId": "q1-4",
  "questionNumber": "1-4",
  "questionType": "summary-completion-text",
  "section": "Reading Passage 1",
  "instructions": "Complete the summary using words from the passage. Write NO MORE THAN TWO WORDS for each answer.",
  "content": {
    "passage": "Scientists have discovered that dolphins use a complex system of sounds to communicate...",
    "summary": "Dolphins communicate through a {q1} of sounds. Research shows they can recognize {q2} even after many years. Their ability to use {q3} demonstrates advanced cognitive skills. Studies also revealed that dolphins can {q4} to solve problems."
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "complex system", "acceptableAnswers": ["system"]},
    {"questionId": "q2", "correctAnswer": "each other", "acceptableAnswers": ["one another"]},
    {"questionId": "q3", "correctAnswer": "tools", "acceptableAnswers": ["objects"]},
    {"questionId": "q4", "correctAnswer": "work together", "acceptableAnswers": ["cooperate", "collaborate"]}
  ]
}
```

### 9. Note Completion

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "note-completion",
  "section": "Listening Part 1",
  "instructions": "Complete the notes below. Write ONE WORD AND/OR A NUMBER for each answer.",
  "audioFile": "audio/listening-note-completion.mp3",
  "content": {
    "title": "Tourist Information - City Museum",
    "notes": [
      {"text": "Opening hours: ", "input": {"id": "q1", "maxLength": 15}, "suffix": " to 6 PM"},
      {"text": "Entrance fee: $", "input": {"id": "q2", "maxLength": 5}, "suffix": " for adults"},
      {"text": "Special exhibitions on ", "input": {"id": "q3", "maxLength": 10}, "suffix": ""},
      {"text": "Audio guide available in ", "input": {"id": "q4", "maxLength": 15}, "suffix": " languages"},
      {"text": "Café located on ", "input": {"id": "q5", "maxLength": 10}, "suffix": " floor"}
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "9 AM", "acceptableAnswers": ["9am", "9:00 AM"]},
    {"questionId": "q2", "correctAnswer": "12", "acceptableAnswers": ["twelve"]},
    {"questionId": "q3", "correctAnswer": "Saturdays", "acceptableAnswers": ["Saturday"]},
    {"questionId": "q4", "correctAnswer": "5", "acceptableAnswers": ["five"]},
    {"questionId": "q5", "correctAnswer": "third", "acceptableAnswers": ["3rd", "top"]}
  ]
}
```

### 10. Table Completion

```json
{
  "questionId": "q1-6",
  "questionNumber": "1-6",
  "questionType": "table-completion",
  "section": "Reading Passage 2",
  "instructions": "Complete the table below. Write NO MORE THAN THREE WORDS from the passage for each answer.",
  "content": {
    "passage": "Different types of renewable energy have various advantages and disadvantages...",
    "table": {
      "headers": ["Energy Type", "Advantages", "Disadvantages"],
      "rows": [
        {
          "cells": [
            {"type": "label", "value": "Solar Power"},
            {"type": "input", "id": "q1", "maxWords": 3},
            {"type": "label", "value": "Weather dependent"}
          ]
        },
        {
          "cells": [
            {"type": "label", "value": "Wind Power"},
            {"type": "label", "value": "Clean and renewable"},
            {"type": "input", "id": "q2", "maxWords": 3}
          ]
        },
        {
          "cells": [
            {"type": "input", "id": "q3", "maxWords": 2},
            {"type": "input", "id": "q4", "maxWords": 3},
            {"type": "label", "value": "High construction costs"}
          ]
        }
      ]
    }
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "Low maintenance costs", "acceptableAnswers": ["Minimal maintenance"]},
    {"questionId": "q2", "correctAnswer": "Noise pollution", "acceptableAnswers": ["Creates noise"]},
    {"questionId": "q3", "correctAnswer": "Hydroelectric", "acceptableAnswers": ["Hydro power"]},
    {"questionId": "q4", "correctAnswer": "Reliable output", "acceptableAnswers": ["Consistent generation"]}
  ]
}
```

### 11. Flow-chart Completion

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "flow-chart-completion",
  "section": "Reading Passage 1",
  "instructions": "Complete the flow-chart below. Choose NO MORE THAN TWO WORDS from the passage for each answer.",
  "content": {
    "passage": "The water cycle is a continuous process...",
    "flowchart": {
      "nodes": [
        {
          "id": 1,
          "type": "box",
          "content": "Water evaporates from {q1}"
        },
        {
          "id": 2,
          "type": "arrow",
          "direction": "down"
        },
        {
          "id": 3,
          "type": "box",
          "content": "Water vapor rises and forms {q2}"
        },
        {
          "id": 4,
          "type": "arrow",
          "direction": "down"
        },
        {
          "id": 5,
          "type": "box",
          "content": "Precipitation occurs as {q3}"
        },
        {
          "id": 6,
          "type": "arrow",
          "direction": "down"
        },
        {
          "id": 7,
          "type": "box",
          "content": "Water returns to {q4} and {q5}"
        }
      ]
    }
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "oceans", "acceptableAnswers": ["seas", "water bodies"]},
    {"questionId": "q2", "correctAnswer": "clouds", "acceptableAnswers": ["cloud formations"]},
    {"questionId": "q3", "correctAnswer": "rain", "acceptableAnswers": ["rainfall", "precipitation"]},
    {"questionId": "q4", "correctAnswer": "rivers", "acceptableAnswers": ["streams"]},
    {"questionId": "q5", "correctAnswer": "oceans", "acceptableAnswers": ["seas"]}
  ]
}
```

### 12. Matching Headings

```json
{
  "questionId": "q1-7",
  "questionNumber": "1-7",
  "questionType": "matching-headings",
  "section": "Reading Passage 1",
  "instructions": "The reading passage has seven paragraphs, A-G. Choose the correct heading for each paragraph from the list of headings below.",
  "content": {
    "headings": [
      {"id": "i", "text": "The origins of written language"},
      {"id": "ii", "text": "Modern communication methods"},
      {"id": "iii", "text": "The impact of the printing press"},
      {"id": "iv", "text": "Future trends in communication"},
      {"id": "v", "text": "Oral traditions in ancient societies"},
      {"id": "vi", "text": "The digital revolution"},
      {"id": "vii", "text": "Barriers to effective communication"},
      {"id": "viii", "text": "The role of social media"},
      {"id": "ix", "text": "Language evolution"}
    ],
    "paragraphs": [
      {"id": "A", "number": 1, "text": "For thousands of years, humans communicated primarily through spoken language..."},
      {"id": "B", "number": 2, "text": "The development of writing systems around 3500 BCE marked a revolutionary change..."},
      {"id": "C", "number": 3, "text": "Johannes Gutenberg's invention in the 15th century transformed how information..."},
      {"id": "D", "number": 4, "text": "The 20th century witnessed rapid technological advancements..."},
      {"id": "E", "number": 5, "text": "Today's digital age has brought unprecedented changes..."},
      {"id": "F", "number": 6, "text": "Social networking platforms have redefined personal communication..."},
      {"id": "G", "number": 7, "text": "Looking ahead, artificial intelligence and virtual reality..."}
    ]
  },
  "answers": [
    {"paragraphId": "A", "correctAnswer": "v"},
    {"paragraphId": "B", "correctAnswer": "i"},
    {"paragraphId": "C", "correctAnswer": "iii"},
    {"paragraphId": "D", "correctAnswer": "ii"},
    {"paragraphId": "E", "correctAnswer": "vi"},
    {"paragraphId": "F", "correctAnswer": "viii"},
    {"paragraphId": "G", "correctAnswer": "iv"}
  ]
}
```

### 13. Matching Features

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "matching-features",
  "section": "Reading Passage 2",
  "instructions": "Match each characteristic with the correct inventor.",
  "content": {
    "passage": "Several inventors have made significant contributions to modern technology...",
    "characteristics": [
      {"id": "q1", "number": 1, "text": "Developed the telephone"},
      {"id": "q2", "number": 2, "text": "Invented the light bulb"},
      {"id": "q3", "number": 3, "text": "Created the first practical automobile"},
      {"id": "q4", "number": 4, "text": "Pioneered radio communication"},
      {"id": "q5", "number": 5, "text": "Designed the first computer"}
    ],
    "options": [
      {"id": "A", "text": "Thomas Edison"},
      {"id": "B", "text": "Alexander Graham Bell"},
      {"id": "C", "text": "Karl Benz"},
      {"id": "D", "text": "Guglielmo Marconi"},
      {"id": "E", "text": "Charles Babbage"},
      {"id": "F", "text": "Nikola Tesla"}
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "B"},
    {"questionId": "q2", "correctAnswer": "A"},
    {"questionId": "q3", "correctAnswer": "C"},
    {"questionId": "q4", "correctAnswer": "D"},
    {"questionId": "q5", "correctAnswer": "E"}
  ]
}
```

### 14. Matching Sentence Endings

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "matching-sentence-endings",
  "section": "Reading Passage 3",
  "instructions": "Complete each sentence with the correct ending, A-G, below.",
  "content": {
    "passage": "Climate change is affecting ecosystems worldwide...",
    "sentenceStarts": [
      {"id": "q1", "number": 1, "text": "Rising temperatures are causing"},
      {"id": "q2", "number": 2, "text": "Polar ice caps are"},
      {"id": "q3", "number": 3, "text": "Many animal species are"},
      {"id": "q4", "number": 4, "text": "Extreme weather events have"},
      {"id": "q5", "number": 5, "text": "Scientists recommend that governments"}
    ],
    "endings": [
      {"id": "A", "text": "melting at an alarming rate."},
      {"id": "B", "text": "become more frequent in recent years."},
      {"id": "C", "text": "implement sustainable policies immediately."},
      {"id": "D", "text": "glaciers to retreat rapidly."},
      {"id": "E", "text": "forced to migrate to cooler regions."},
      {"id": "F", "text": "increased agricultural production."},
      {"id": "G", "text": "reduced ocean salinity levels."}
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "D"},
    {"questionId": "q2", "correctAnswer": "A"},
    {"questionId": "q3", "correctAnswer": "E"},
    {"questionId": "q4", "correctAnswer": "B"},
    {"questionId": "q5", "correctAnswer": "C"}
  ]
}
```

### 15. Map/Diagram Labelling

```json
{
  "questionId": "q1-5",
  "questionNumber": "1-5",
  "questionType": "map-labelling",
  "section": "Listening Part 2",
  "instructions": "Label the map below. Write the correct letter, A-G, next to questions 1-5.",
  "audioFile": "audio/listening-map.mp3",
  "content": {
    "mapImage": "images/campus-map.png",
    "locations": [
      {"id": "q1", "number": 1, "description": "Library"},
      {"id": "q2", "number": 2, "description": "Student Center"},
      {"id": "q3", "number": 3, "description": "Sports Complex"},
      {"id": "q4", "number": 4, "description": "Cafeteria"},
      {"id": "q5", "number": 5, "description": "Main Entrance"}
    ],
    "mapLabels": [
      {"id": "A", "position": {"x": 100, "y": 150}},
      {"id": "B", "position": {"x": 250, "y": 150}},
      {"id": "C", "position": {"x": 400, "y": 150}},
      {"id": "D", "position": {"x": 150, "y": 300}},
      {"id": "E", "position": {"x": 300, "y": 300}},
      {"id": "F", "position": {"x": 450, "y": 300}},
      {"id": "G", "position": {"x": 275, "y": 450}}
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "C"},
    {"questionId": "q2", "correctAnswer": "E"},
    {"questionId": "q3", "correctAnswer": "F"},
    {"questionId": "q4", "correctAnswer": "D"},
    {"questionId": "q5", "correctAnswer": "G"}
  ]
}
```

### 16. Form Completion

```json
{
  "questionId": "q1-8",
  "questionNumber": "1-8",
  "questionType": "form-completion",
  "section": "Listening Part 1",
  "instructions": "Complete the form below. Write NO MORE THAN THREE WORDS AND/OR A NUMBER for each answer.",
  "audioFile": "audio/listening-form.mp3",
  "content": {
    "formTitle": "Library Membership Application",
    "fields": [
      {"id": "q1", "label": "Full Name:", "maxWords": 3},
      {"id": "q2", "label": "Date of Birth:", "maxWords": 1, "format": "DD/MM/YYYY"},
      {"id": "q3", "label": "Address:", "maxWords": 3},
      {"id": "q4", "label": "Postcode:", "maxWords": 1},
      {"id": "q5", "label": "Telephone:", "maxWords": 1},
      {"id": "q6", "label": "Email:", "maxWords": 1},
      {"id": "q7", "label": "Occupation:", "maxWords": 2},
      {"id": "q8", "label": "Membership Type:", "maxWords": 2}
    ]
  },
  "answers": [
    {"questionId": "q1", "correctAnswer": "Sarah Johnson"},
    {"questionId": "q2", "correctAnswer": "15/03/1995"},
    {"questionId": "q3", "correctAnswer": "42 Oak Street"},
    {"questionId": "q4", "correctAnswer": "SW1 2AB"},
    {"questionId": "q5", "correctAnswer": "07700123456"},
    {"questionId": "q6", "correctAnswer": "sarah.j@email.com"},
    {"questionId": "q7", "correctAnswer": "University student"},
    {"questionId": "q8", "correctAnswer": "Standard membership"}
  ]
}
```

### 17. Writing Task 1 (Academic)

```json
{
  "questionId": "writing-task-1",
  "questionNumber": 1,
  "questionType": "writing-academic-task1",
  "section": "Writing Task 1",
  "instructions": "You should spend about 20 minutes on this task. Write at least 150 words.",
  "content": {
    "taskType": "graph|chart|table|diagram|map",
    "title": "The chart below shows the percentage of households in different income brackets in Country X from 1990 to 2020.",
    "image": "images/income-chart.png",
    "prompt": "Summarise the information by selecting and reporting the main features, and make comparisons where relevant."
  },
  "constraints": {
    "minWords": 150,
    "suggestedTime": 20
  },
  "assessmentCriteria": {
    "taskAchievement": "Covers key features and trends",
    "coherence": "Logical organization",
    "vocabulary": "Range and accuracy",
    "grammar": "Range and accuracy"
  }
}
```

### 18. Writing Task 2

```json
{
  "questionId": "writing-task-2",
  "questionNumber": 2,
  "questionType": "writing-task2",
  "section": "Writing Task 2",
  "instructions": "You should spend about 40 minutes on this task. Write at least 250 words.",
  "content": {
    "essayType": "opinion|discussion|problem-solution|advantages-disadvantages",
    "prompt": "Some people believe that technology has made our lives more complicated. Others think it has simplified many aspects of daily life. Discuss both views and give your own opinion.",
    "requirements": [
      "Give reasons for your answer",
      "Include relevant examples from your knowledge or experience"
    ]
  },
  "constraints": {
    "minWords": 250,
    "suggestedTime": 40
  },
  "assessmentCriteria": {
    "taskResponse": "Addresses all parts of the task",
    "coherence": "Clear progression of ideas",
    "vocabulary": "Appropriate and varied",
    "grammar": "Wide range with accuracy"
  }
}
```

---

## Additional Metadata Fields

### Audio Files (For Listening Tests)

```json
{
  "audioFiles": [
    {
      "id": "audio1",
      "filename": "listening-part1.mp3",
      "duration": 300,
      "format": "mp3",
      "url": "https://storage.example.com/audio/listening-part1.mp3"
    }
  ]
}
```

### Images/Diagrams

```json
{
  "images": [
    {
      "id": "img1",
      "filename": "campus-map.png",
      "type": "map",
      "url": "https://storage.example.com/images/campus-map.png",
      "altText": "Campus map showing various buildings"
    }
  ]
}
```

---

## Validation Rules

### Word Count Constraints
- "ONE WORD" = maxWords: 1
- "TWO WORDS" = maxWords: 2
- "THREE WORDS" = maxWords: 3
- "ONE WORD AND/OR A NUMBER" = maxWords: 1, allowNumbers: true
- "NO MORE THAN TWO WORDS" = maxWords: 2

### Answer Matching Rules
```json
{
  "matchingRules": {
    "caseSensitive": false,
    "ignoreArticles": true,
    "ignorePunctuation": true,
    "acceptableSynonyms": ["big:large", "small:little"],
    "spellingVariants": ["colour:color", "centre:center"]
  }
}
```

---

## Complete Example: Full Listening Test

```json
{
  "exam": {
    "id": "ielts-listening-sample-1",
    "type": "listening",
    "title": "IELTS Listening Sample Test 1",
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
        "Each question carries one mark",
        "There are four parts to the test",
        "You will hear each part once",
        "For each part of the test there will be time for you to look through the questions and time for you to check your answers"
      ]
    },
    "questions": [
      {
        "questionId": "q1-7",
        "questionNumber": "1-7",
        "questionType": "fill-in-gaps-table",
        "section": "Part 1",
        "instructions": "Complete the notes. Write ONE WORD AND/OR A NUMBER in each gap.",
        "audioFile": "audio/listening-part1.mp3",
        "content": {
          "type": "table",
          "title": "Phone call about second-hand furniture",
          "rows": [
            // ... table structure
          ]
        },
        "answers": [
          // ... answers
        ]
      },
      // ... more questions
    ]
  }
}
```

---

## AI Conversion Prompt for DeepSeek

```
You are an expert at converting IELTS exam PDFs to structured JSON format.

INPUT: IELTS exam PDF
OUTPUT: Structured JSON following the exact format specified

TASK:
1. Identify the exam type (Listening/Reading/Writing)
2. Extract instructions carefully
3. Identify question types accurately
4. Structure content properly
5. Extract correct answers from answer key
6. Maintain question numbering
7. Preserve formatting (tables, lists, etc.)

QUESTION TYPE IDENTIFICATION:
- If filling blanks in sentences/tables → "fill-in-gaps"
- If choosing one option → "mcq-single"
- If choosing multiple options → "mcq-multiple"
- If matching items → "matching"
- If TRUE/FALSE/NOT GIVEN → "true-false-not-given"
- ... (see full list above)

OUTPUT FORMAT:
Return valid JSON with proper escaping and formatting.
Include all metadata: audio files, images, time limits.

VALIDATION:
- Check all question IDs are unique
- Verify answer keys match questions
- Ensure word limits are specified
- Confirm question types are correct
```

---

## Next Steps

1. **Test the JSON structure** with one question type
2. **Train AI model** on sample conversions
3. **Validate output** against schema
4. **Iterate** based on results

Need help with:
- Specific question type structure?
- AI prompt refinement?
- Validation logic?
- Database schema?

Let me know! 🚀
