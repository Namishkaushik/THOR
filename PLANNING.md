# Thor — Gym Management System

## Problem Statement
A web-based gym management system to handle member records, attendance
(including face-recognition entry), fee tracking and reminders, trainer
attendance, churn prediction, and bulk data entry via Excel.

## Stack
- Backend: Flask (Python)
- Frontend: AdminLTE (HTML/CSS/JS theme) + Jinja2 templates
- Database: SQLite (via SQLAlchemy ORM)
- Face recognition: separate Python process, writes to shared DB (library TBD)

## Requirements
- [ ] Member CRUD (add/edit/view/delete members)
- [ ] Trainer CRUD
- [ ] Member attendance (view + log)
- [ ] Trainer attendance
- [ ] Fee tracking
- [ ] Fee reminders
- [ ] Excel bulk entry
- [ ] Churn prediction (rule-based first, ML later)
- [ ] Face recognition entry (RTSP/IP camera)

## Build Order (dependency-first)
1. DB schema
2. CRUD (members, trainers)
3. Attendance
4. Fees + reminders
5. Churn rule engine
6. Excel entry
7. Face recognition (last — most isolated, most unknowns)

## Architecture Notes
- Churn: starts as a rule-based engine (e.g. "no visit in N days" →
  flag). Upgrades to ML once real historical data exists.
- Face recognition: runs as its own script watching the camera feed,
  independent of the Flask request cycle. Writes attendance rows
  directly into the shared DB. Flask just reads whatever's there.
- `Member` is the hub table — Attendance, Fees, and (later)
  FaceEmbeddings all reference it via foreign key.

## Decisions Log
(Add dated entries here as we make schema/design decisions, with the
reasoning — future-you will forget why otherwise.)

- YYYY-MM-DD: ...

## Status
Current stage: project skeleton set up, repo linked to GitHub.
Next: design Member table schema.