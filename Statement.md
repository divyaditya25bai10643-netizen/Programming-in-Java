# Problem Statement

Small and mid-sized libraries (college department libraries, community
reading rooms, office libraries) often track book lending using registers
or spreadsheets. This makes it hard to know, at a glance, which books are
available, which members currently hold books, which loans are overdue,
and how much in fines has accumulated. Manual tracking is error-prone,
hard to search, and does not scale as the collection grows.

## Scope of the Project

This project delivers a **command-line Library Management System** that
digitizes the core lending workflow of a small library:

- Maintaining a catalog of books with copy counts
- Maintaining a registry of members
- Issuing books to members and recording due dates
- Returning books and automatically computing overdue fines
- Reporting on overdue loans and fines collected

The system is intentionally scoped to a **single-library, single-user
(librarian-operated) CLI tool** with local file-based persistence — it does
not cover multi-branch libraries, concurrent multi-user access, online
member self-service, or integration with barcode scanners. These are noted
as future enhancements in the project report.

## Target Users

- **Librarians / library assistants** who need a fast, reliable way to
  register members, manage the catalog, and process issues/returns from a
  terminal, without needing to learn a complex GUI or database tool.
- **Students/instructors** evaluating the project, who need to run it
  end-to-end from the command line with no external setup.

## High-Level Features

1. **Member Management module** — register, view, update, deactivate, and
   delete members, with email/phone validation and duplicate-email
   prevention.
2. **Book Inventory module** — add, view, search (by title/author), update,
   and delete book titles, with copy-count tracking.
3. **Issue / Return & Reporting module** — issue a book (with eligibility
   checks), return a book (with automatic fine calculation and a per-loan
   fine cap), list active loans per member, list all overdue loans, and
   report total fines collected.

Supporting concerns applied across all modules: input validation, custom
checked exceptions for every predictable failure mode, and centralized
logging of every significant operation and error to `logs/library.log`.
