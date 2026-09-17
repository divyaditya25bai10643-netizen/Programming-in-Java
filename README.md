# Library Management System

A command-line Library Management System built in core Java, demonstrating
object-oriented design, layered architecture, file-based persistence,
custom exception handling, and centralized logging.


## Overview

The system lets a librarian manage members, the book catalog, and the
book issue/return cycle entirely from the terminal — no GUI, no external
database, no internet connection required. All data survives between runs
because it is persisted to plain-text files under `data/`.

## Features

**1. Member Management**
- Register new members (with email/phone validation, duplicate-email checks)
- View all members / view a single member by ID
- Update member details
- Deactivate or delete a member

**2. Book Inventory Management**
- Add new book titles with a copy count
- View the full catalog
- Search books by title or author (partial, case-insensitive match)
- Update book details (including safe adjustment of copy counts)
- Delete a book from the catalog

**3. Issue / Return & Reporting**
- Issue a book to a member (enforces: member must be active, book must have
  an available copy, member cannot hold more than 5 books at once)
- Return a book (automatically calculates a late fine — ₹5/day overdue,
  capped at ₹200 per loan)
- View all transactions
- View an overdue-loans report
- View a member's currently active loans
- View total fines collected (simple analytics)

Cross-cutting concerns applied throughout: input validation, custom checked
exceptions for every failure mode, and centralized logging to `logs/library.log`.

## Technologies / Tools Used

- **Language:** Java 17+ (uses `switch` expressions, `var`, `sealed`-free simple OOP)
- **Persistence:** Plain-text, pipe-delimited files (no external DB needed)
- **Logging:** `java.util.logging`
- **Build:** Plain `javac`/`java` via `build.sh` / `run.sh` (works with zero
  internet access); a `pom.xml` is also included for Maven users
- **Version control:** Git

## Project Structure

```
LibraryManagementSystem/
├── src/main/java/com/library/
│   ├── Main.java                  # CLI entry point / menu
│   ├── model/                     # Book, Member, Transaction
│   ├── exception/                 # 5 custom checked exceptions
│   ├── repository/                # File-backed persistence (CRUD)
│   ├── service/                   # Business logic (3 functional modules)
│   └── util/                      # LoggerUtil, InputValidator, IdGenerator
├── src/test/java/com/library/test/
│   └── LibraryTestRunner.java     # Dependency-free test suite
├── data/                          # Generated at runtime (books.txt, members.txt, transactions.txt)
├── logs/                          # Generated at runtime (library.log)
├── docs/diagrams/                 # Architecture, UML, ER, sequence diagrams
├── build.sh / run.sh / run_tests.sh
└── pom.xml                        # Optional, for Maven users with internet access
```
