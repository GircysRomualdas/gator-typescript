# Gator

Command-line RSS Feed Aggregator built in TypeScript that allows users to subscribe to RSS feeds, fetch posts, and manage subscriptions — all backed by PostgreSQL.

This is the starter code used in Boot.dev's [Build a Blog Aggregator in TypeScript](https://www.boot.dev/courses/build-blog-aggregator-typescript) course.

---

## Requirements

- Node.js 20+
- PostgreSQL

---

## Installation

1. Clone the Repository

2. Install dependencies:
```bash
npm install
```

3. Install PostgreSQL:  
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```
4. Configure PostgreSQL:

```bash
sudo service postgresql start
sudo -u postgres psql
```

Inside the psql shell:
```sql
CREATE DATABASE gator;
ALTER USER postgres PASSWORD 'postgres';
\q
```

5. Create configuration file ~/.gatorconfig.json
```json
{
  "db_url": "postgres://postgres:postgres@localhost:5432/gator?sslmode=disable",
  "current_user_name": "your_username"
}
```

6. Run migrations:
```bash
npm run migrate
```

---

## Usage

Run Gator:
```bash
npm run start <command> [arguments]
```

### Example Session

#### Reset users:
```bash
npm run start reset
```

Output:
```bash
All users deleted
```

#### Register:
```bash
npm run start register kahya
```

Output:
```bash
Registered as kahya
```

#### Login:
```bash
npm run start login kahya
```

Output:
```bash
Logged in as kahya
```

#### Add feed:
```bash
npm run start addfeed "Hacker News RSS" "https://hnrss.org/newest"
```

Output:
```bash
Feed Hacker News RSS created successfully
* ID:            940681df-54b5-4baa-aaa1-11de92751fba
* Created:       Mon Nov 10 2025 00:44:33 GMT+0200
* Updated:       Mon Nov 10 2025 00:44:33 GMT+0200
* name:          Hacker News RSS
* URL:           https://hnrss.org/newest
* User:          kahya
```

#### Follow feed:
```bash
npm run start follow "https://hnrss.org/newest"
```

Output:
```bash
Feed Hacker News RSS followed by user kahya
```

#### View followed feeds:
```bash
npm run start following
```

Output:
```bash
Feed follows for user kahya:
followed feed Hacker News RSS
```

#### Aggregate posts:
```bash
npm run start agg 5s
```

Output:
```bash
Collecting feeds every 5s
Fetched feed:
Created post: Holocaust Database
Created post: AI Progress and Recommendations
Created post: Coxeter Groups
...
```

#### Browse recent posts:
```bash
npm run start browse 3
```

Output:
```bash
Found 3 posts for user kahya
Sun Nov 09 2025 22:33:48 GMT+0200 from Hacker News RSS
--- Holocaust Database ---
Link: https://www.ushmm.org/online/hsv/person_advance_search.php
=====================================
Sun Nov 09 2025 22:33:44 GMT+0200 from Hacker News RSS
--- AI Progress and Recommendations ---
Link: https://openai.com/index/ai-progress-and-recommendations/
=====================================
Sun Nov 09 2025 22:32:23 GMT+0200 from Hacker News RSS
--- Coxeter Groups ---
Link: https://arxiv.org/abs/2510.23002
```

## Commands

| Command | Description |
|---------|-------------|
| `register <username>` | Register a new user |
| `login <username>` | Log in as an existing user |
| `reset` | Delete all users from the database |
| `users` | List all registered users |
| `addfeed <feed-name> <feed-url>` | Add a new RSS feed |
| `feeds` | List all available feeds |
| `follow <feed-url>` | Follow a feed |
| `unfollow <feed-url>` | Unfollow a feed |
| `following` | List all feeds you are currently following |
| `agg <interval>` | Aggregate (fetch and store latest posts at a specified interval, e.g., `5s`) |
| `browse [limit]` | Browse recent posts from feeds you follow (optionally limit results) |

