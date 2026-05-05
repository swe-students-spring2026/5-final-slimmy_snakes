# StudyCast

[![log github events](https://github.com/swe-students-spring2026/5-final-slimmy_snakes/actions/workflows/event-logger.yml/badge.svg)](https://github.com/swe-students-spring2026/5-final-slimmy_snakes/actions/workflows/event-logger.yml)
[![CI (planner web)](https://github.com/swe-students-spring2026/5-final-slimmy_snakes/actions/workflows/planner-web-ci.yml/badge.svg)](https://github.com/swe-students-spring2026/5-final-slimmy_snakes/actions/workflows/planner-web-ci.yml)
[![CI (study session service)](https://github.com/swe-students-spring2026/5-final-slimmy_snakes/actions/workflows/study-session-service-ci.yml/badge.svg)](https://github.com/swe-students-spring2026/5-final-slimmy_snakes/actions/workflows/study-session-service-ci.yml)

StudyCast is a containerized academic planner that helps students manage exams, organize preparation plans, and schedule study sessions. It also enables weather-aware planning so students can decide whether to study outdoors, while providing focused study session monitoring to keep them on track.

The calendar does more than just display events. It highlights exams in blue, warns students in red when an outdoor preparation session is scheduled on a rainy or snowy day, and marks past-due preparation sessions in red as reminders. The study-session feature also supports active focus monitoring: students can start a timed session, and the system will trigger a beep and turn the screen red if it detects loss of focus, such as turning their head away or looking at a phone.

## Digital Ocean Link:
```https://167.99.153.128.sslip.io/auth```
## Subsystems

- `planner-web`: Flask web dashboard for authentication, tasks, exams, preparation planning, calendar/weather views, and study-session controls.
- `study-session-service`: Flask API for starting/ending study sessions and classifying distraction risk.
- `mongodb`: MongoDB database container with starter initialization data.

## Run Locally

```powershell
docker compose up --build
```

Then open:

```text
http://localhost:5001
```

## Run Tests

From the repository root:

```powershell
.\.venv\Scripts\python.exe -m pytest
```

Run each subsystem with the required 80% coverage gate:

```powershell
cd planner-web
..\.venv\Scripts\python.exe -m pytest --cov=app --cov=calendar_weather --cov-report=term-missing --cov-fail-under=80
```

```powershell
cd study-session-service
..\.venv\Scripts\python.exe -m pytest --cov=app --cov=detector --cov-report=term-missing --cov-fail-under=80
```

## How To Use StudyCast

### 1. Create an account or sign in

1. Create an account with your name, email, and password, or sign in with an existing account.
2. After signing in, you will be taken to the dashboard.

### 2. Dashboard

The dashboard is the main summary page. It shows a list of:

- upcoming exams
- upcoming preparation sessions
- past exams and past preparations
- short-term tasks
- long-term tasks

Use the navigation bar at the top to move between `Dashboard`, `Exams`, `Preparations`, `Calendar`, `Study Sessions`, and `To-Do`.

### 3. Add exams

1. Open the `Exams` page.
2. Add an exam by entering:
   - subject
   - exam date
   - exam type

You can also mark an exam as done or delete it later.

### 4. Add preparation sessions

1. Open the `Preparations` page.
2. Choose the exam you are preparing for.
3. Pick a preparation date.
4. Choose how much study time you expect:
   - `Light (~1 hr)`
   - `Medium (~3 hrs)`
   - `Heavy (~5+ hrs)`
5. Choose whether the session is `Indoor` or `Outdoor`.
6. Optionally add notes about what you want to review.

Important preparation features:

- You must add an exam first before you can create a preparation session.
- The preparation date cannot be later than the exam date.
- StudyCast prevents you from planning 24 or more total preparation hours on the same day.

### 5. Calendar & Weather

Open the `Calendar` page to see your exams and preparation sessions for the selected month.

Features on this page:

- monthly calendar view 
- weather lookup of the past month&today(Open-Meteo) and weather forcast of 7 days(National Weather Service weather.gov) for all U.S. cities.
- temperature range and weather label for each day when available
- quick actions to mark exams or preparations as done or delete.

Weather warning example:

- If you scheduled an `Outdoor` preparation session and that day has bad weather such as rain, snow, drizzle, or storms, the preparation is highlighted with a warning in the calendar. For example, if you plan an outdoor preparation session on Tuesday and that day is raining, the calendar will flag that preparation so you know the weather may interfere with the plan.
- If an preparation session is past, there will be warnings as well.

### 6. To-Do

Open the `To-Do` page to create tasks and sort them into:

- short-term tasks
- long-term tasks

You can mark tasks as completed or delete them when they are no longer needed.

### 7. Study session

Open the `Study Sessions` page to start a timed study session.

How it works:

1. Set the session length in hours and minutes.
2. Click `Start Session`.
3. Allow camera access so the focus check can run.
4. Keep the camera on while you study.
5. Click `End Session` when finished, or let the timer end automatically.

During a session, the app:

- checks whether a face is present
- beeps and the screen turn red when you appear to be looking away or looking at a phone
- records distraction counts when the session ends

## Team

- James Huang — [@JamesHuang2004](https://github.com/JamesHuang2004)
- Jerry Wang — [@JerrrryWang](https://github.com/JerrrryWang)
- Rohan Malhotra — [@Rohanmalhotra0](https://github.com/Rohanmalhotra0)
- Ryan Lu — [@CHEology](https://github.com/CHEology)
- Jai — [@hyperjasm](https://github.com/hyperjasm)
