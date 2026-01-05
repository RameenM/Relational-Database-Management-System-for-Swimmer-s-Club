#  The Super Awesome Swimmers Club  
### Relational Database Management System (Oracle SQL)

---

##  Project Overview

This project involves the end-to-end design, normalization, and implementation of a comprehensive relational database system for **The Super Awesome Swimmers Club**. The objective was to model the full operational workflow of a mid-scale swimming club, including swimmer registration, course scheduling, pool maintenance, supplier management, billing, competitions, and charity-based discount programs.

The project followed a structured database design methodology, beginning with business rule identification and entity discovery, followed by metadata table creation, functional dependency analysis, normalization up to **Third Normal Form (3NF)**, and implementation using **Oracle SQL (Oracle APEX)**. An **Enhanced Entity Relationship (EER) diagram** and a complete **relational schema** were developed to ensure data integrity, scalability, and alignment with real-world business constraints.

---

##  Database Design Scope

The database models the following functional areas:

- Swimmer enrollment and course registration  
- Guardian management for minor swimmers  
- Course scheduling and instructor assignment  
- Pool facilities, maintenance schedules, and developer contracts  
- Supplier management, product ordering, billing, and supply tracking  
- Competitive events and participation rules  
- Charity partnerships and population-based discount logic  

Developer and charity entities were incorporated to support pool construction contracts and population-based discount rules.

---

##  Key Technical Components

- **Normalization:** Functional dependency analysis and normalization to 3NF  
- **Modeling:** Enhanced Entity Relationship (EER) diagrams  
- **Schema Design:** Relational schema with PK/FK enforcement  
- **Implementation:** Oracle SQL (Oracle APEX)  
- **Integrity:** Domain, entity, and referential integrity  
- **Queries:** Standard and advanced SQL queries  

---

## My Contributions (Individual Work)

As part of **Team 8**, my individual contributions focused on database rigor, normalization, and SQL implementation for key subsystems.

###  Normalization & Dependency Analysis
- Normalized **Swimmer**, **Supplier**, and **Competition** entities to **Third Normal Form (3NF)**
- Identified and resolved **full, partial, and transitive dependencies**
- Finalized business rules governing swimmer eligibility, competition participation, referrals, and supplier interactions

###  EER & Relational Schema Design
- Designed **EER diagrams** for the Swimmer, Supplier, and Competition subsystems
- Defined **primary keys, foreign keys, and participation constraints**
- Mapped EER models to relational schemas

###  SQL Implementation & Integrity Constraints
- Implemented tables in **Oracle SQL** with explicit constraints
- Enforced **domain, entity, and referential integrity**
- Identified and validated all PK–FK relationships

###  Advanced SQL Query
- Developed a **special SQL query** addressing a non-trivial business question
- Ensured correctness, performance, and schema alignment

---

## Sample SQL Implementation

### Example: Swimmer Table
```sql
CREATE TABLE Swimmer (
    swimmer_id NUMBER(4) PRIMARY KEY,
    first_name VARCHAR2(30) NOT NULL,
    last_name VARCHAR2(30) NOT NULL,
    age NUMBER(2) CHECK (age BETWEEN 10 AND 60),
    swimmer_type VARCHAR2(15) NOT NULL,
    reference_id NUMBER(4),
    charity_name VARCHAR2(50)
);

CREATE TABLE Competition_Schedule (
    competition_name VARCHAR2(10),
    adult_swimmer_id NUMBER(4),
    PRIMARY KEY (competition_name, adult_swimmer_id),
    FOREIGN KEY (competition_name) REFERENCES Competition(competition_name),
    FOREIGN KEY (adult_swimmer_id) REFERENCES Swimmer(swimmer_id)
);

SELECT course_id, COUNT(swimmer_id) AS total_enrollments
FROM Registration
GROUP BY course_id
ORDER BY total_enrollments DESC
FETCH FIRST 5 ROWS ONLY;


