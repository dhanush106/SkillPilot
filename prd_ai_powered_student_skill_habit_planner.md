# Product Requirements Document (PRD)

## 1. Product Overview
**Product Name:** AI-Powered Student Skill & Habit Planner  
**Target Users:** College & university students  
**Problem Statement:** Students struggle to consistently manage skill learning, habits, workouts, and academics within limited free time. Manual planning fails when days are missed.

**Solution:** A smart web platform that automatically plans daily skill learning, habits, and workouts based on the student’s schedule and dynamically replans when tasks are missed.

---

## 2. Goals & Objectives
- Help students convert free time into consistent skill growth
- Reduce cognitive load of daily planning
- Adapt schedules automatically when tasks are missed
- Provide curated free learning resources

**Success Metrics:**
- Daily active usage
- Task completion rate
- User retention over 7 days

---

## 3. User Personas
**Primary Persona:**
- College student (18–25)
- Wants to learn technical skills
- Has irregular schedules
- May go to gym

---

## 4. Core Features (MVP)
1. Authentication & onboarding
2. Time-aware skill planning
3. Daily AI-generated todo list
4. Auto replanning of missed tasks
5. YouTube learning resource suggestions
6. Optional workout planning

---

## 5. User Flow
1. User signs up
2. Completes onboarding (time, sleep, gym, skills)
3. Adds skills to learn
4. System generates plan
5. Daily todo list shown
6. User completes or skips tasks
7. System replans automatically

---

# 🧩 Exact MongoDB Schemas

## User Schema
```
{
  name: String,
  email: String,
  password: String,
  dailyLearningHours: Number,
  freeTimeSlots: [String],
  sleepStart: String,
  sleepEnd: String,
  dayStart: String,
  dayEnd: String,
  workoutEnabled: Boolean,
  workoutTime: String,
  createdAt: Date
}
```

## Skill Schema
```
{
  userId: ObjectId,
  skillName: String,
  category: String,
  targetDays: Number,
  progress: Number,
  createdAt: Date
}
```

## Task Schema
```
{
  userId: ObjectId,
  skillId: ObjectId,
  title: String,
  type: String,
  scheduledDate: Date,
  timeSlot: String,
  resources: [String],
  completed: Boolean
}
```

---

# 🧠 AI Prompt Templates

## Skill Planning Prompt
```
You are a smart study planner.
User daily learning hours: {{hours}}
Skills to learn: {{skills}}
Target days: {{days}}
Sleep time: {{sleep}}
Workout time: {{workout}}

Break skills into daily topics and return a day-wise plan.
```

## Replanning Prompt
```
Some tasks were missed.
Remaining days: {{remainingDays}}
Pending tasks: {{tasks}}

Reassign tasks evenly without exceeding daily hours.
```

---

# 🔗 REST API Contract

## Auth
- POST /auth/register
- POST /auth/login

## User
- POST /user/onboarding
- GET /user/profile
- PUT /user/profile

## Skills
- POST /skills
- GET /skills
- PUT /skills/:id
- DELETE /skills/:id

## Tasks
- GET /tasks/today
- GET /tasks/week
- POST /tasks/complete/:id

---

# 🧪 Test Cases

## Authentication
- Register with valid email
- Reject duplicate email
- Login with wrong password

## Planning
- Skill added generates tasks
- Tasks do not exceed daily hours

## Replanning
- Missed task moves to next free day
- Multiple missed tasks rebalance correctly

---

# 🗂️ Folder-by-Folder Code Skeleton

## Backend
```
backend/
 ├─ controllers/
 ├─ models/
 ├─ routes/
 ├─ services/
 │   ├─ aiPlanner.js
 │   ├─ replanner.js
 ├─ middleware/
 ├─ utils/
 └─ server.js
```

## Frontend
```
frontend/
 ├─ components/
 ├─ pages/
 ├─ services/
 ├─ hooks/
 └─ App.jsx
```

---

## 6. Non-Goals (Out of Scope)
- Job recommendations
- Google Classroom integration
- Mobile app

---

## 7. Risks & Mitigation
- AI failure → fallback to rule-based planning
- User overload → daily hour cap

---

## 8. Future Enhancements
- Job matching
- Classroom integration
- Analytics dashboard

---

**End of PRD**

