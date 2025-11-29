# yourAiTutor
AI Micro-Mentor is a full-stack learning platform that turns student notes or textbook chapters into personalized study materials. Users can upload content, and the system generates flashcards, quizzes, explanations, and adaptive study paths based on performance using AI and vector search.
🚀 Features
Core (MVP)

Upload notes (PDF, pasted text, typed content)

Automatic text cleaning + structuring

AI-generated flashcards & quizzes

Dashboard to review generated items

User authentication (Supabase Auth)

Intermediate

Chunking + embeddings for vector search

Adaptive quizzes based on weak areas

Performance tracking & analytics

Saved AI study sessions and history

Advanced (Planned)

Spaced repetition scheduling

AI-generated weekly study plan

Topic-level knowledge graph

Teacher/Instructor mode for bulk notes

🎯 Problem This Project Solves

Students often review material inefficiently because they don’t know:

What they’ve mastered

What they need to practice

How to turn large notes into actionable study tasks

AI Micro-Mentor fixes this by converting raw notes into structured learning content and adapting to the student’s understanding over time. It acts like a personal tutor — automated, always available, and powered by retrieval-augmented AI.

🧠 High-Level Architecture
Frontend (Next.js)
     ↓
Backend API (Node.js or FastAPI)
     ↓
AI Layer (LLM calls + prompt templates)
     ↓
Vector Store (pgvector / Pinecone)
     ↓
Database (Supabase/Postgres)

Flow Summary

User uploads notes

Text is extracted → cleaned → chunked

Embeddings generated → stored in vector DB

User requests flashcards or quiz

Relevant chunks retrieved via similarity search

AI produces output using structured prompts

Results saved to DB and shown in UI

🛠️ Tech Stack
Frontend

Next.js (App Router)

React

TailwindCSS

Zustand or Context for state management

Backend

Node.js + Express or Python + FastAPI

Supabase client SDK

OpenAI API for LLM + embeddings

Database & Storage

Supabase Postgres

pgvector (built-in vector search)

Supabase Storage for file uploads

AI

OpenAI GPT-4.1 / GPT-4.1-mini

Embeddings (text-embedding-3-large or small)

RAG pipeline with chunk retrieval

JSON-structured function calling for quizzes

📂 Project Structure
ai-micro-mentor/
│
├── frontend/              # Next.js application
├── backend/               # Node.js or FastAPI API
├── database/              # Schema + migrations
├── llm/                   # Prompt templates + evaluation
└── scripts/               # Dev & build helpers


Full directory structure is in the repository for clarity.

⚙️ Setup Instructions
1. Clone the repository
git clone https://github.com/your-username/ai-micro-mentor.git
cd ai-micro-mentor

2. Configure Environment Variables

Create .env files in both /frontend and /backend.

Frontend .env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000

Backend .env
SUPABASE_URL=
SUPABASE_SERVICE_ROLE_KEY=
OPENAI_API_KEY=
DATABASE_URL=

3. Install Dependencies
Frontend
cd frontend
npm install
npm run dev

Backend (Node.js version)
cd backend
npm install
npm run dev

Backend (FastAPI version)
pip install -r requirements.txt
uvicorn src.app:app --reload

4. Database Setup
Supabase SQL (schema.sql)

Run:

-- Users, notes, chunks, flashcards, quizzes, results
-- Vector embeddings stored in pgvector column


Upload seed data if needed:

supabase db restore seed.sql

🔍 API Overview
POST /notes/upload

Uploads raw notes → returns extracted text.

POST /notes/embed

Chunks & embeds text → stores vectors.

POST /generate/flashcards

Retrieves relevant chunks → generates flashcards via LLM.

POST /generate/quiz

Retrieves relevant chunks → returns quiz JSON.

POST /quiz/submit

Saves results + updates performance model.

📘 LLM Pipeline Summary

All quiz and flashcard generation uses:

retrieval → fetch relevant note chunks

formatting → normalize text

prompting → structured messages

function calling → enforce JSON output

Prompts live in /llm/prompts/.

📊 Adaptive Learning Logic (Simplified)

Track success rate per concept

Identify weak areas (below threshold)

Query vector DB for similar chunks

Generate targeted questions

Schedule spaced repetition intervals

This forms the “AI mentor” behavior.

🧪 Testing
Frontend
npm run test

Backend
pytest  # if Python
npm run test  # if Node

🛣️ Roadmap
Phase 1 — MVP

 Notes upload + extract

 Flashcard generator

 Basic quizzes

 User login + dashboard

Phase 2 — Smart Features

 Embeddings + retrieval

 Adaptive quizzes

 Progress tracking

Phase 3 — Advanced

 Spaced repetition

 AI study plan generator

 Knowledge graph UI
