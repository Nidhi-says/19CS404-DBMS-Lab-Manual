# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_fitness.png)

### Entities and Attributes

| Entity         | Attributes (PK, FK)                                                         | Notes                                      |
| -------------- | --------------------------------------------------------------------------- | ------------------------------------------ |
| **Member**     | PK: Member\_ID<br>Attributes: Name, MembershipType, StartDate               | A member can join multiple programs.       |
| **Program**    | PK: Trainer\_ID<br>Attributes: Name                                         | A program is conducted by a trainer.       |
| **Attendance** | PK: Attendance\_ID (in lower table)<br>FKs link to Member, Program, Payment | Tracks member’s participation in sessions. |
| **Payment**    | PK: Payment\_ID<br>Attributes: MembershipFee, SessionFee                    | Payments are linked to attendance/members. |

### Relationships and Constraints

| Relationship                                   | Cardinality                                                | Participation        | Notes                                                             |
| ---------------------------------------------- | ---------------------------------------------------------- | -------------------- | ----------------------------------------------------------------- |
| Member **joins** Program                       | 1\:N (Member to joins), N\:M (joins to Program)            | Total for joins      | A member can join many programs; a program can have many members. |
| Program **conducts** Attendance                | 1\:M (Program to Attendance), 1\:N (Attendance to Program) | Partial              | Each attendance is conducted by one trainer.                      |
| Attendance **is booked by** Member             | 1\:N (Member to Attendance)                                | Total for Attendance | Attendance records are tied to members.                           |
| Attendance **is recorded/tracked for** Payment | 1\:N both sides                                            | Total                | Each payment is linked to attendance tracking.                    |


### Assumptions
- Each member must join at least one program.

- Each attendance record belongs to exactly one member and one program.

- Payment can cover membership fee or session fee.

- A trainer may conduct multiple programs, but each program is managed by only one trainer.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_library.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_restaurant.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
