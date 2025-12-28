# Resume Optimizer

AI-powered tool to dramatically reduce the time it takes to update and optimize resumes for job applications at scale.

## Project Overview

**Purpose:** Dramatically reduce the time it takes to update and optimize resumes for job applications at scale by intelligently blending past resume content with new experiences and job-specific requirements.

**Target Users:** Job seekers who are applying to multiple positions and need to quickly tailor their resumes without starting from scratch each time.

**Success Criteria:** 
- User can go from "I have a new accomplishment" to "polished, job-specific resume" in under 5 minutes
- Resume passes ATS systems and doesn't obviously look AI-generated
- Grammar and formatting are publication-ready

## Core Problem Statement

**Pain Point:** Job seekers know they should customize their resume for each application, but it's exhausting to:
- Rewrite bullet points for every job
- Optimize keywords without sounding robotic
- Maintain consistent formatting
- Ensure perfect grammar
- Make it not sound AI-generated

**Solution:** An intelligent system that takes unstructured input ("I led a team of 5 on a React project") and blends it with your existing resume context to create polished, job-specific versions at scale.

## Key Features

### Quick Update
- User can paste unstructured text about new accomplishments/jobs
- System accepts messy, incomplete input (text bomb)
- No rigid forms or fields required

### Chunker
- Breaks resume into logical sections (Experience, Education, Skills, Summary)
- Allows users to add unstructured bullets to specific chunks
- Each chunk processed independently for better AI results

### Accelerator
- Loads past resume as baseline context
- AI agent available on-demand to help brainstorm new bullet points
- Suggests ways to frame accomplishments (STAR method, metrics, impact)

### Resume Styler
- Applies optimal ATS-friendly formatting
- Consistent style across all sections
- Professional template that's clean and readable
- Designed for extensibility (easy to add more templates later)

### Job Intentionality
- User can paste job description
- System extracts and highlights key requirements/keywords
- Naturally integrates keywords into resume content
- Tailors existing bullets to match job priorities

### AI Washer
- Varies sentence structure to avoid AI patterns
- Uses natural language, not corporate buzzwords
- Adds personal voice/authenticity markers
- Maintains perfect grammar and structure while hiding AI origin
- **Goal:** Make it structurally perfect and grammatically flawless, but hide obvious AI patterns

### Quality Control

#### Resume Grading
Scores resume on:
- ATS compatibility (formatting, keywords)
- Impact (metrics, action verbs, specificity)
- Keyword match to job description
- Overall quality score

#### English Teacher Final Pass
- Perfect grammar
- Syntax optimization
- Readability score
- Consistency check (tense, punctuation, formatting)

## User Workflow
```
1. Upload Base Resume
   ↓
2. Quick Updates (Chunked)
   - See resume broken into sections
   - Add unstructured notes to each section
   - AI Assistant available on-demand
   ↓
3. Job-Specific Optimization (Optional)
   - Paste job description
   - System extracts keywords
   ↓
4. AI Blending
   - Merges old resume + new bullets + job keywords
   - Shows draft with highlights
   - User reviews and edits
   ↓
5. AI Washer + Quality Control
   - Humanization pass
   - Grammar and syntax check
   - Quality scores with improvement tips
   ↓
6. Export
   - Download as PDF/DOCX
   - Save version for future iterations
```

## Tech Stack

**Frontend:**
- Framework: Next.js with TypeScript
- Styling: Tailwind CSS
- State Management: React Context or Zustand
- File Upload: react-dropzone
- PDF Generation: jsPDF or react-pdf

**Backend:**
- Runtime: Next.js API routes
- AI Integration: Claude API (Anthropic)
- Document Parsing: 
  - PDF: pdf-parse
  - DOCX: mammoth.js

**Database (Future):**
- PostgreSQL or MongoDB for saving resume versions
- LocalStorage/IndexedDB for MVP (client-side only)

**Hosting:**
- Vercel (easy deployment, serverless functions)

## Data Models

### Resume Object
```typescript
interface Resume {
  id: string;
  userId?: string;
  version: number;
  createdAt: Date;
  
  sections: {
    summary?: Section;
    experience: Section[];
    education: Section[];
    skills: Section;
    projects?: Section[];
    certifications?: Section[];
  };
  
  targetJob?: string;
  targetCompany?: string;
  jobDescription?: string;
  
  scores?: {
    atsCompatibility: number;
    keywordMatch: number;
    grammarScore: number;
    impactScore: number;
    aiDetectionRisk: number;
  };
}

interface Section {
  id: string;
  title: string;
  originalContent: string;
  userAdditions?: string;
  optimizedContent: string;
  isApproved: boolean;
  changesHighlighted?: boolean;
}
```

### Job Description Object
```typescript
interface JobDescription {
  id: string;
  rawText: string;
  extractedKeywords: string[];
  requiredSkills: string[];
  niceToHaveSkills: string[];
  companyName?: string;
  jobTitle?: string;
}
```

## API Endpoints
```
POST /api/resume/upload
- Accepts: PDF or DOCX file
- Returns: Parsed resume JSON

POST /api/resume/optimize-chunk
- Accepts: { sectionId, originalContent, userAdditions, jobDescription? }
- Returns: { optimizedContent, suggestions }

POST /api/resume/wash
- Accepts: { resumeContent }
- Returns: { washedContent, aiDetectionScore }

POST /api/resume/grade
- Accepts: { resumeContent, jobDescription? }
- Returns: { scores: {...}, improvements: [...] }

POST /api/job/extract-keywords
- Accepts: { jobDescription }
- Returns: { keywords, skills, requirements }
```

## Development Phases

### Phase 1: Core Parser (Week 1)
- [x] Set up Next.js project
- [ ] Build file upload UI
- [ ] Integrate pdf-parse for PDF reading
- [ ] Create Claude API integration for parsing
- [ ] Display parsed resume in sections

### Phase 2: Quick Update & Chunker (Week 2)
- [ ] Build chunk editor UI
- [ ] Add unstructured text input per section
- [ ] Implement "optimize chunk" API endpoint
- [ ] Show before/after comparison
- [ ] Save state in LocalStorage

### Phase 3: Job Intentionality (Week 3)
- [ ] Add job description input
- [ ] Build keyword extraction with Claude
- [ ] Integrate keywords into optimization prompts
- [ ] Show keyword match percentage

### Phase 4: AI Washer & Quality Control (Week 4)
- [ ] Implement AI washing prompt
- [ ] Build grammar checking
- [ ] Create scoring system
- [ ] Add visual score display
- [ ] Implement "English teacher" final pass

### Phase 5: Export & Polish (Week 5)
- [ ] PDF generation
- [ ] Resume templates/styling
- [ ] Download functionality
- [ ] UI polish and testing
- [ ] Deploy to Vercel

## Success Metrics

**User Experience:**
- Time from upload to download: < 5 minutes
- User satisfaction with AI suggestions: > 80% approval rate
- Grammar errors in final output: 0

**Technical:**
- ATS compatibility score: > 90%
- AI detection risk: < 30%
- Keyword match (when job provided): > 70%
- API response time: < 3 seconds per chunk

## AI Washing Strategy

**Two-Pass Approach:**

**Pass 1: Quality (Don't Compromise)**
- Perfect grammar ✓
- Strong structure ✓
- Powerful action verbs ✓
- Quantified impact ✓
- Professional tone ✓

**Pass 2: Humanize (Subtle Changes)**
- Remove AI "tells":
  - ❌ "Leveraged cross-functional synergies"
  - ✅ "Worked with marketing and sales teams"
  - ❌ "Spearheaded innovative solutions"
  - ✅ "Led development of new features"
  - ❌ All bullets starting with same verb
  - ✅ Varied sentence starters

**What AI Washing Does NOT Mean:**
- ❌ Adding typos or grammar errors
- ❌ Using weak or vague language
- ❌ Removing metrics or impact

**What It DOES Mean:**
- ✓ Using common phrasing over thesaurus words
- ✓ Varying sentence patterns naturally
- ✓ Avoiding buzzword clusters
- ✓ Making it sound like you wrote it, not a robot

## Template Strategy

**Current:** One clean ATS-friendly format (MVP)

**Future:** Template library with multiple styles
- ATS-optimized (default)
- Creative/Design
- Executive/Premium
- Technical/GitHub-style

**Architecture:** Designed for extensibility from day 1 - easy to add new templates by copying base template folder and modifying styles.

## Getting Started
```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Open http://localhost:3000
```

## Project Structure
```
/src
  /app
    /api
      /resume
        /parse
        /optimize-chunk
        /wash
        /grade
      /job
        /extract-keywords
    /components
      /FileUploader
      /ChunkEditor
      /AIAssistant (on-demand)
      /QualityScores
      /TemplateSelector
  /templates
    /ats-classic
      template.ts
      renderer.tsx
      styles.css
  /lib
    /claude.ts (API integration)
    /parsers.ts
    /types.ts
```

## Contributing

This is a personal project. Not open for contributions at this time.

## License

All rights reserved. This is proprietary software.

## Next Steps

1. **Phase 1:** Build resume parser with Claude API integration
2. Set up file upload component
3. Create chunk-based editor UI
4. Implement first optimization endpoint

---

**Built for Sundai Club** | Started: December 2024
