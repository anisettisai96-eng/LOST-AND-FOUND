# Lost & Found System

A web-based platform where users can report lost or found items, search through existing reports, and recover belongings through a claim-and-approval process. Built with **PHP, MySQL, HTML, CSS and JavaScript**.

> Final project, Mumbai University (2026-2027), by D Sai Anshetty.

## The Problem

Lost belongings are usually handled through notice boards, chat groups or a help-desk counter. Information is scattered, hard to search, and there is no reliable way to check who the real owner is. This project puts everything in one searchable place and adds a structured claim workflow between the finder and the owner.

## Features

**For users**
- Register and log in (passwords stored as hashes)
- Report a lost or found item with title, category, description, location, date and an optional photo
- Browse and search items by keyword, status (lost / found) and category
- View item details, including the reporter's contact e-mail
- **Claim a found item** by sending a message to the owner (duplicate claims are blocked)
- **Report "I found this"** on a lost item to let the owner know
- Owners can **approve or reject claims**; approving marks the item as resolved
- Edit your own items, mark them resolved, and track them on **My Items**
- Personal dashboard with counts of lost, found and resolved items and pending claims
- Light and dark theme, remembered in the browser

**For admins**
- Admin dashboard with totals of users, items, resolved items and claims
- Recent items, recent users and pending claims

## Screenshots

| Home | Login |
|---|---|
| ![Home](screenshots/home.png) | ![Login](screenshots/login.png) |

| Dashboard | Browse Items |
|---|---|
| ![Dashboard](screenshots/dashboard.png) | ![Browse Items](screenshots/browse-items.png) |

| My Items |
|---|
| ![My Items](screenshots/my-items.png) |

## Tech Stack

| Layer | Technology |
|---|---|
| Server side | PHP 8 with PDO |
| Database | MySQL / MariaDB (InnoDB, utf8mb4) |
| Front end | HTML5, CSS3, JavaScript (`fetch()` for AJAX calls) |
| Local server | Apache via XAMPP or WAMP |

## Database

Three related tables, created automatically on first run:

- `users`: id, name, email (unique), password (hash), role (`user` / `admin`)
- `items`: id, user_id, title, description, category, status (`lost` / `found`), location, date_lost_found, image_path, is_resolved
- `claims`: id, item_id, claimant_id, message, status (`pending` / `approved` / `rejected`)

Foreign keys use `ON DELETE CASCADE`, and the columns used in searches are indexed.

## Getting Started

1. Install **XAMPP** or **WAMP** and start **Apache** and **MySQL**.
2. Copy this project folder into the web-server root (for example `htdocs`).
3. Open `http://localhost/<project-folder>/` in your browser. The `lost_found_system` database and its tables are created automatically on first load.
4. Optionally open `test-connection.php` to check the database connection.
5. Register a new account. A default admin account is also created on first run (see `config/database.php`). **Change its password immediately.**

## Project Structure

```
├── index.php                Home page
├── login.php, signup.php, logout.php
├── dashboard.php            Personal dashboard
├── items.php                Browse / search / filter
├── add-item.php             Report a lost or found item
├── view-item.php            Item details, claim and found actions
├── edit-item.php, my-items.php
├── admin.php                Admin dashboard
├── process-claim.php, process-found.php,
│   update-claim.php, mark-resolved.php, search.php   (JSON endpoints)
├── config/                  database.php, session.php
├── includes/                auth.php, header.php, footer.php
├── css/, js/                Styles, animations and client-side behaviour
└── uploads/                 Item images
```

## Security

- Passwords hashed with `password_hash()` and checked with `password_verify()`
- Prepared statements (PDO) for database queries
- Output escaping with `htmlspecialchars()`
- Session-based access control with role checks for admin pages
- Ownership checks before approving claims or resolving items
- CSRF tokens on the JSON endpoints

## Known Limitations

- Lost and found items are **not matched automatically**; users search manually
- No e-mail or SMS notifications, and no in-app chat (contact is through the e-mail shown on the item page)
- Image uploads are not yet validated for file type or size on the server
- CSRF tokens are not yet added to the HTML forms (login, signup, report, edit)
- The Items page has no pagination, and the sign-up phone field is not stored
- Default local database credentials and an auto-created admin account should be changed before any public deployment

## Future Improvements

- Automatic matching of lost and found items by category, location, date and text similarity
- E-mail / SMS notifications for new claims and status changes
- In-app chat between owner and finder
- Server-side upload validation, CSRF tokens on all forms and rate limiting
- Pagination, sorting and map-based location selection
- Admin tools to moderate items and users
- Mobile app or progressive web app

## Author

** Sai Anshetty**, Mumbai University. Guide: Manoj Singh.
