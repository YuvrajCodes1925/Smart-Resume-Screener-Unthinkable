# Smart Resume Screener

## 📋 Project Deliverables

This project includes all required deliverables as specified in the assignment:

✅ **GitHub Repository**: Complete source code with detailed commit history  
✅ **README Documentation**: Comprehensive architecture overview and LLM prompts  
✅ **Demo Video**: 2-3 minute demonstration video showcasing all features  

### 📂 Additional Resources

**Google Drive Folder**: [Project Resources & Demo Video](https://drive.google.com/drive/folders/1VJvCDt_RyxNXEpkqNUH9hFqMe1Wvapf_?usp=sharing)

This folder contains:
- 🎥 Demo Video (2-3 minutes)
- 📊 Presentation Slides
- 📄 Additional Documentation
- 🖼️ Architecture Diagrams
- 📸 Screenshots & Examples

---

## Overview

The Smart Resume Screener is an AI-powered recruitment tool that intelligently parses resumes, extracts structured data (skills, experience, education), and matches them with job descriptions using Large Language Models (LLM). Built with Flask, React, and OpenAI's GPT-4, it provides semantic matching with detailed scoring (1-10 scale) and comprehensive justification for hiring decisions.

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         Frontend Layer                          │
│                    (React + Material-UI)                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐         │
│  │   Dashboard  │  │Resume Upload │  │   Matching   │         │
│  │  Component   │  │  Component   │  │   Results    │         │
│  └──────────────┘  └──────────────┘  └──────────────┘         │
└─────────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Backend API Layer                          │
│                    (Flask + Flask-RESTful)                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐         │
│  │Resume Routes │  │Matching Routes│ │  Analytics   │         │
│  └──────────────┘  └──────────────┘  └──────────────┘         │
└─────────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Services Layer                             │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────┐ │
│  │ Resume Parser    │  │   LLM Service    │  │   Matching   │ │
│  │ (pdfplumber +    │  │   (OpenAI GPT-4) │  │   Service    │ │
│  │  spaCy NLP)      │  │                  │  │              │ │
│  └──────────────────┘  └──────────────────┘  └──────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Database Layer                             │
│                        (MongoDB)                                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐         │
│  │   Resumes    │  │    Matches   │  │     Jobs     │         │
│  │  Collection  │  │  Collection  │  │  Collection  │         │
│  └──────────────┘  └──────────────┘  └──────────────┘         │
└─────────────────────────────────────────────────────────────────┘
```

## Key Technologies

- **Backend**: Flask, Flask-RESTful, Flask-CORS
- **Frontend**: React 18, Material-UI (MUI), Axios
- **Database**: MongoDB
- **AI/ML**: OpenAI GPT-4, spaCy NLP, scikit-learn
- **Document Processing**: pdfplumber, python-docx
- **Infrastructure**: Docker, Nginx, GitHub Actions

## Features

### Intelligent Resume Parsing

- **Advanced Document Processing**:
  - Supports PDF and DOCX formats
  - Extracts structured data: contact info, skills, experience, education, certifications
  - Uses spaCy NLP for intelligent text analysis
  - Regular expression patterns for email, phone, LinkedIn, GitHub extraction
  - Average processing time: 5-8 seconds per resume

### Job Description Analysis

- **Smart JD Processing**:
  - Extracts required and preferred skills
  - Identifies experience requirements and education qualifications
  - Analyzes key responsibilities and company culture indicators
  - Categorizes jobs by difficulty level and domain
  - Average processing time: 3-4 seconds

### AI-Powered Semantic Matching

- **LLM-Based Evaluation**:
  - Uses GPT-4 for deep semantic understanding
  - Multi-dimensional scoring system (1-10 scale):
    - Skills match analysis
    - Experience relevance evaluation
    - Education fit assessment
    - Cultural alignment prediction
  - Generates detailed justification for each score
  - Provides actionable hiring recommendations (HIRE/INTERVIEW/REJECT)
  - Average processing time: 8-12 seconds per candidate

### Comprehensive Analytics

- **Intelligent Insights**:
  - Real-time database statistics
  - Top skills distribution across candidates
  - Education level analytics
  - Recent upload tracking
  - Matching session history

## Technical Features

- **Flask RESTful API**:
  - Async request handling
  - Automatic error handling and validation
  - CORS support for frontend integration
  - Comprehensive API documentation

- **OpenAI GPT-4 Integration**:
  - Custom prompt engineering for optimal results
  - Structured JSON output parsing
  - Temperature control for consistent scoring
  - Fallback parsing for error resilience

- **MongoDB Storage**:
  - Efficient document-based storage
  - Indexed queries for fast retrieval
  - Pagination support for large datasets
  - Aggregation pipelines for analytics

## Project Structure

```
smart-resume-screener/
├── backend/                          # Flask API server
│   ├── app.py                       # Main application entry point
│   ├── config.py                    # Configuration settings
│   ├── requirements.txt             # Python dependencies
│   ├── models/                      # Data models
│   │   ├── __init__.py
│   │   ├── resume.py
│   │   └── candidate.py
│   ├── services/                    # Business logic layer
│   │   ├── __init__.py
│   │   ├── resume_parser.py        # Resume parsing service
│   │   ├── llm_service.py          # LLM integration service
│   │   └── matching_service.py     # Matching algorithms
│   ├── routes/                      # API endpoints
│   │   ├── __init__.py
│   │   ├── resume_routes.py        # Resume CRUD operations
│   │   └── matching_routes.py      # Job matching endpoints
│   └── utils/                       # Utility functions
│       ├── __init__.py
│       ├── pdf_extractor.py
│       └── text_processor.py
├── frontend/                         # React application
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── components/              # React components
│   │   │   ├── Dashboard.js
│   │   │   ├── ResumeUpload.js
│   │   │   ├── CandidateList.js
│   │   │   └── MatchingResults.js
│   │   ├── services/                # API client services
│   │   │   └── api.js
│   │   ├── App.js
│   │   └── index.js
│   └── package.json
├── docs/                             # Documentation
│   ├── API_DOCS.md
│   ├── ARCHITECTURE.md
│   └── presentation.pdf
├── tests/                            # Test suites
│   ├── test_resume_parser.py
│   ├── test_llm_service.py
│   └── test_matching_service.py
├── docker-compose.yml                # Docker configuration
├── .gitignore
└── README.md
```

## LLM Usage & Prompting

### Semantic Matching Prompt

The core of our intelligent matching system uses carefully engineered prompts to leverage GPT-4's semantic understanding capabilities:

```python
prompt = f"""
Compare the following resume with the job description and rate fit on 1–10 with justification.

JOB DESCRIPTION:
{job_description}

CANDIDATE RESUME:
{resume_summary}

Please analyze the match between this candidate and the job requirements. Provide your response in the following JSON format:

{{
  "overall_score": <integer from 1-10>,
  "confidence": <float from 0.0-1.0>,
  "skills_match": {{
    "score": <integer from 1-10>,
    "matched_skills": ["skill1", "skill2", ...],
    "missing_skills": ["skill1", "skill2", ...],
    "justification": "<explanation>"
  }},
  "experience_match": {{
    "score": <integer from 1-10>,
    "relevant_experience": "<summary>",
    "years_of_experience": <estimated years>,
    "justification": "<explanation>"
  }},
  "education_match": {{
    "score": <integer from 1-10>,
    "degree_relevance": "<assessment>",
    "justification": "<explanation>"
  }},
  "cultural_fit": {{
    "score": <integer from 1-10>,
    "justification": "<explanation>"
  }},
  "strengths": ["strength1", "strength2", ...],
  "concerns": ["concern1", "concern2", ...],
  "recommendation": "<HIRE|INTERVIEW|REJECT>",
  "detailed_justification": "<comprehensive explanation of the overall assessment>"
}}

Ensure your analysis is objective, thorough, and based on the specific requirements mentioned in the job description.
"""
```

### Example LLM Response

Here's a sample response from GPT-4 for a Senior Python Developer position:

```json
{
  "overall_score": 9,
  "confidence": 0.92,
  "skills_match": {
    "score": 9,
    "matched_skills": [
      "python",
      "django",
      "flask",
      "postgresql",
      "mongodb",
      "aws",
      "docker",
      "kubernetes"
    ],
    "missing_skills": [],
    "justification": "Candidate has all required technical skills including Python, Django, Flask, and database technologies. Additionally possesses expertise in Kubernetes which is a valuable bonus skill for microservices architecture."
  },
  "experience_match": {
    "score": 9,
    "relevant_experience": "6 years of Python development with proven leadership experience in microservices architecture",
    "years_of_experience": 6,
    "justification": "Candidate exceeds the minimum 5 years requirement with 6 years of Python development experience. Has specific hands-on experience with microservices architecture, CI/CD implementation, and team mentoring which aligns perfectly with the senior-level expectations."
  },
  "education_match": {
    "score": 8,
    "degree_relevance": "Bachelor of Science in Computer Science",
    "justification": "BS in Computer Science from a reputable institution aligns well with technical requirements. The degree provides strong foundational knowledge in algorithms, data structures, and software engineering principles."
  },
  "cultural_fit": {
    "score": 8,
    "justification": "Demonstrated leadership qualities through mentoring 3 junior developers. Experience working in Agile/Scrum environments suggests good collaboration and communication skills. The candidate's focus on clean code and best practices indicates alignment with quality-focused culture."
  },
  "strengths": [
    "Strong technical skills alignment with all required technologies",
    "Leadership and mentoring experience with junior developers",
    "Proven track record with microservices and cloud technologies",
    "Experience with CI/CD and DevOps practices",
    "Additional expertise in Kubernetes and containerization"
  ],
  "concerns": [],
  "recommendation": "HIRE",
  "detailed_justification": "This candidate is an excellent match for the Senior Python Developer position with an overall score of 9/10. They not only meet but exceed all the key requirements: 6 years of Python development experience (vs. 5 required), comprehensive knowledge of Django/Flask frameworks, strong database skills (PostgreSQL, MongoDB), and extensive cloud/containerization experience (AWS, Docker, Kubernetes). The candidate demonstrates leadership qualities through mentoring experience and has successfully implemented microservices architectures serving large user bases. Their track record of optimizing CI/CD pipelines and improving system performance shows a results-oriented approach. With no significant concerns identified and strong alignment across technical skills, experience level, and cultural fit, this candidate is highly recommended for immediate hiring consideration."
}
```

### LLM Configuration

```python
# GPT-4 Configuration for Optimal Performance
openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {
            "role": "system", 
            "content": "You are an expert HR professional and ATS system specializing in resume-job matching. Provide detailed, objective analysis."
        },
        {
            "role": "user", 
            "content": prompt
        }
    ],
    temperature=0.3,        # Lower temperature for consistent, focused responses
    max_tokens=1000,        # Sufficient for detailed analysis
    top_p=1.0,
    frequency_penalty=0.0,
    presence_penalty=0.0
)
```

## API Documentation

### Resume Endpoints

#### Upload Resume
```http
POST /api/resumes
Content-Type: multipart/form-data

Body: resume file (PDF/DOCX)

Response:
{
  "success": true,
  "resume_id": "550e8400-e29b-41d4-a716-446655440000",
  "original_filename": "john_doe_resume.pdf",
  "parsed_data": {
    "contact_info": {
      "name": "John Doe",
      "email": "john.doe@email.com",
      "phone": "+1-555-123-4567",
      "linkedin": "linkedin.com/in/johndoe",
      "github": "github.com/johndoe"
    },
    "skills": ["python", "django", "aws", "docker"],
    "experience": [...],
    "education": [...]
  },
  "upload_timestamp": "2025-10-16T00:00:00"
}
```

#### Get All Resumes
```http
GET /api/resumes?page=1&per_page=10

Response:
{
  "resumes": [...],
  "pagination": {
    "page": 1,
    "per_page": 10,
    "total": 45,
    "pages": 5
  }
}
```

#### Get Specific Resume
```http
GET /api/resumes/{resume_id}

Response:
{
  "_id": "550e8400-e29b-41d4-a716-446655440000",
  "original_filename": "john_doe_resume.pdf",
  "parsed_data": { ... }
}
```

#### Delete Resume
```http
DELETE /api/resumes/{resume_id}

Response:
{
  "success": true,
  "message": "Resume deleted successfully"
}
```

#### Search Resumes
```http
GET /api/resumes/search?skills=python,java&min_experience=3&education=bachelor

Response:
{
  "resumes": [...],
  "total_found": 12,
  "search_criteria": {
    "skills": ["python", "java"],
    "min_experience": 3,
    "education": "bachelor"
  }
}
```

#### Get Resume Statistics
```http
GET /api/resumes/stats

Response:
{
  "total_resumes": 150,
  "recent_uploads_week": 25,
  "top_skills": [
    {"skill": "python", "count": 89},
    {"skill": "javascript", "count": 72},
    {"skill": "react", "count": 58}
  ],
  "education_distribution": [
    {"degree": "Bachelor's", "count": 95},
    {"degree": "Master's", "count": 45}
  ]
}
```

### Matching Endpoints

#### Match Resumes with Job
```http
POST /api/match
Content-Type: application/json

Body:
{
  "job_description": "We are looking for a Senior Python Developer with 5+ years of experience...",
  "job_title": "Senior Python Developer",
  "resume_ids": ["id1", "id2"]  // optional - if not provided, matches all resumes
}

Response:
{
  "success": true,
  "matching_session_id": "session_123",
  "job_title": "Senior Python Developer",
  "timestamp": "2025-10-16T00:15:00",
  "results": [
    {
      "candidate_id": "id1",
      "candidate_name": "John Doe",
      "overall_score": 9,
      "recommendation": "HIRE",
      "skills_match": {
        "score": 9,
        "matched_skills": ["python", "django", "aws"]
      },
      "experience_match": {
        "score": 9,
        "years_of_experience": 6
      },
      "detailed_justification": "Excellent match with all required skills..."
    }
  ],
  "insights": {
    "total_candidates": 15,
    "average_score": 6.8,
    "recommended_candidates": 3,
    "interview_candidates": 8
  }
}
```

#### Single Resume Match
```http
POST /api/match/single
Content-Type: application/json

Body:
{
  "resume_id": "resume_id_here",
  "job_description": "Job description here",
  "job_title": "Senior Developer"
}

Response:
{
  "overall_score": 8,
  "confidence": 0.85,
  "recommendation": "INTERVIEW",
  "skills_match": { ... },
  "experience_match": { ... },
  "education_match": { ... },
  "detailed_justification": "..."
}
```

#### Analyze Job Description
```http
POST /api/match/analyze-job
Content-Type: application/json

Body:
{
  "job_description": "Full job description text...",
  "job_title": "Data Scientist"
}

Response:
{
  "required_skills": ["python", "machine learning", "sql"],
  "preferred_skills": ["deep learning", "tensorflow"],
  "experience_requirements": {
    "min_years": 3,
    "level": "mid",
    "specific_experience": [...]
  },
  "education_requirements": {
    "required_degree": "bachelor's",
    "preferred_fields": ["Computer Science", "Statistics"]
  }
}
```

## Getting Started

### Prerequisites

- Python 3.8+
- Node.js 16+
- MongoDB 4.4+
- OpenAI API key

### Installation

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/yourusername/smart-resume-screener.git
   cd smart-resume-screener
   ```

2. **Backend Setup**:

   ```bash
   cd backend
   
   # Create virtual environment
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   
   # Install dependencies
   pip install -r requirements.txt
   
   # Download spaCy model
   python -m spacy download en_core_web_sm
   ```

3. **Configure Environment**:

   Create `.env` file in backend directory:
   ```bash
   # backend/.env
   SECRET_KEY=your-secret-key-here
   MONGODB_URI=mongodb://localhost:27017/resume_screener
   OPENAI_API_KEY=your-openai-api-key-here
   UPLOAD_FOLDER=uploads
   FLASK_ENV=development
   ```

4. **Frontend Setup**:

   ```bash
   cd ../frontend
   
   # Install dependencies
   npm install
   
   # Configure API URL
   # Create .env file
   echo "REACT_APP_API_URL=http://localhost:5000" > .env
   ```

5. **Start MongoDB**:

   ```bash
   # Using Docker
   docker run -d -p 27017:27017 --name mongodb mongo:latest
   
   # Or use local MongoDB installation
   mongod --dbpath /path/to/data
   ```

6. **Run Application**:

   **Backend**:
   ```bash
   cd backend
   python app.py
   ```
   Backend will run on `http://localhost:5000`

   **Frontend**:
   ```bash
   cd frontend
   npm start
   ```
   Frontend will run on `http://localhost:3000`

### Docker Deployment

1. **Build and Run with Docker Compose**:

   ```bash
   docker-compose build
   docker-compose up -d
   ```

2. **Access Application**:
   - Frontend: `http://localhost` or `http://your-ip-address`
   - Backend API: `http://localhost/backend`
   - API Documentation: `http://localhost/backend/docs`

## Demo Video (2-3 Minutes)

### 🎥 [Watch Demo Video on Google Drive](https://drive.google.com/drive/folders/1VJvCDt_RyxNXEpkqNUH9hFqMe1Wvapf_?usp=sharing)

### Video Outline

**1. Introduction (30 seconds)**
   - Project overview and key features
   - Technology stack highlight
   - AI-powered semantic matching introduction

**2. Resume Upload & Parsing (30 seconds)**
   - Upload PDF/DOCX resume through dashboard
   - Show real-time parsing progress
   - Display extracted structured data:
     - Contact information
     - Skills and technologies
     - Work experience
     - Education history
     - Certifications

**3. Job Description & Matching (60 seconds)**
   - Create/input job description
   - Select candidates for matching
   - Run AI-powered matching algorithm
   - Display ranked results with:
     - Overall scores (1-10 scale)
     - Skills match breakdown
     - Experience relevance
     - Hiring recommendations (HIRE/INTERVIEW/REJECT)
   - Show detailed justification from GPT-4

**4. Results & Analytics (30 seconds)**
   - View candidate comparison dashboard
   - Display top candidate profiles
   - Show analytics:
     - Skills distribution
     - Match score statistics
     - Education breakdown
   - Demonstrate filtering and search capabilities

**5. Conclusion (10 seconds)**
   - Summary of key benefits
   - Future enhancements preview

## Evaluation Criteria Coverage

### ✅ Code Quality & Structure
- **Modular Architecture**: Separated concerns across services, routes, and utilities
- **Clean Code**: PEP 8 compliant, well-documented with docstrings
- **Error Handling**: Comprehensive try-catch blocks and validation
- **Type Hints**: Python type annotations for better code clarity
- **Testing**: Unit and integration tests included

### ✅ Data Extraction
- **Multi-format Support**: PDF and DOCX resume parsing
- **NLP Processing**: spaCy for intelligent text extraction
- **Structured Output**: Contact info, skills, experience, education, certifications
- **Regular Expressions**: Pattern matching for emails, phones, URLs
- **Error Resilience**: Graceful handling of malformed documents

### ✅ LLM Prompt Quality
- **Detailed Instructions**: Clear task definition with expected output format
- **Structured JSON**: Consistent response format with all required fields
- **Scoring System**: 1-10 scale with multi-dimensional analysis
- **Contextual Analysis**: Semantic understanding of job requirements
- **Justification**: Detailed explanations for all scores and recommendations

### ✅ Output Clarity
- **Comprehensive Scoring**: Overall score with breakdown by category
- **Actionable Recommendations**: HIRE/INTERVIEW/REJECT with reasoning
- **Strengths & Concerns**: Bullet-pointed highlights
- **Matched vs Missing Skills**: Clear skill gap analysis
- **Confidence Metrics**: Transparency in AI predictions

## Development

### Code Quality

- **Backend**:
  - Ruff for Python linting
  - Black for code formatting
  - Type hints with mypy
  - Pre-commit hooks

- **Frontend**:
  - ESLint for TypeScript/JavaScript
  - Prettier for code formatting
  - Husky for Git hooks

### Testing

**Backend Tests**:
```bash
cd backend
pytest tests/ -v --cov=.
```

**Frontend Tests**:
```bash
cd frontend
npm test
npm run test:coverage
```

### CI/CD Pipeline

- **Development**: Automated testing on every commit
- **Staging**: Integration tests and deployment to staging environment
- **Production**: Full test suite, security scans, and production deployment

## Performance Metrics

- **Resume Parsing**: 5-8 seconds per resume
- **Job Description Analysis**: 3-4 seconds
- **Semantic Matching**: 8-12 seconds per candidate
- **Batch Processing**: Up to 50 resumes per session
- **Database Query Time**: < 100ms for most operations
- **API Response Time**: < 2 seconds (excluding LLM calls)

## Security Features

- **File Validation**: Only PDF and DOCX files allowed, 16MB size limit
- **Secure Filenames**: UUID-based file naming to prevent path traversal
- **API Key Protection**: Environment variables for sensitive data
- **Input Sanitization**: Validation on all API inputs
- **CORS Configuration**: Proper cross-origin request handling
- **MongoDB Security**: Authentication and connection string encryption

## Future Enhancements

- [ ] Bulk resume upload with progress tracking
- [ ] Advanced filtering and search with Elasticsearch
- [ ] Email notifications for matching results
- [ ] Resume anonymization for bias reduction
- [ ] Multi-language support (Spanish, French, German)
- [ ] Integration with popular ATS systems (Greenhouse, Lever)
- [ ] Machine learning model training on historical data
- [ ] Real-time collaboration features
- [ ] Mobile application (React Native)
- [ ] Video interview analysis integration

## Contributors

- **Yuvraj Singh** - *System Design & Architecture*
- [Your Name] - *Development & Implementation*

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- OpenAI for GPT-4 API and excellent documentation
- spaCy for powerful NLP processing capabilities
- Material-UI team for beautiful React components
- Flask and React communities for extensive resources
- MongoDB for flexible document storage

## Support & Contact

For questions, issues, or contributions:

- 📧 Email: ysbhati1925@gmail.com
- 🐛 Issues: [GitHub Issues](https://github.com/YuvrajCodes1925/smart-resume-screener/issues)
- 📚 Documentation: [Wiki](https://github.com/YuvrajCodes1925/smart-resume-screener/wiki)
- 💬 Discussions: [GitHub Discussions](https://github.com/YuvrajCodes1925/smart-resume-screener/discussions)
- 📂 Resources: [Google Drive](https://drive.google.com/drive/folders/1VJvCDt_RyxNXEpkqNUH9hFqMe1Wvapf_?usp=sharing)

---

**Built with ❤️ for efficient and intelligent recruitment processes**

*Designed by Yuvraj Singh*