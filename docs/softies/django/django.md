install python -> create virtual env -> install django

- Create VE: $ python3 -m venv .venv
- Activate VE: $ source .venv/bin/activate
- Deactivate VE: $ deactivate
- Update pip: $ python -m pip install –upgrade pip
- Install Django: $ python -m pip install django~=<version>
- Create Project: $ django-admin startproject <proj_name> .
- Run Project: $ python manage.py runserver
- Apply Available Migrations: $ python manage.py migrate
- Create An App: $ python manage.py startapp <app_name>
- Output Content of Current VE: $ pip freeze > requirements.txt
- Install Deps: $ pip install -r requirements.txt
- Run Tests: $ python manage.py test
- API Schema Generation: $ python manage.py spectacular --file api.yaml
- Postgres DB URL: $ DATABASE_URL: postgres://<username>:<password>@<host>:<port>/<database>
- For SSH Access: $ git@github.com:username/repo_name.git
- PAT: $ https://username:PERSONAL_ACCESS_TOKEN@github.com/username/repo.git
- .gitignore: CTRL + Shift + P
- Env vars: $ pip install django-environ

### Django Cheat Sheet

- Create django project steps:

  1- Create VE: # make sure that python is installed on your system
  - `python -m venv .venv`

  2- Activate VE:
  - `source .venv/bin/activate`

  3- Install django:
  - `python -m pip install django~=<version>`

  4- Create proj:
  - `django-admin startproject <project_name> .` # . means create project in the current folder

  5- Run proj:
  - `python manage.py runserver`

  6- Deactivate VE:
  - `deactivate`

- Database-related commands:
  - Make migrations:
    - `python manage.py makemigrations`

  - Apply available migrations:
    - `python manage.py migrate`

  - Postgres DB URL: $ DATABASE_URL: postgres://<username>:<password>@<host>:<port>/<database>

- App-related commands:
  - Create app:
    - `python manage.py startapp <app_name>`

- Test-related commands:
  - Run Tests:
    - `python manage.py test`

- Dep-related commands:
  - Update pip:
    - `python -m pip install –upgrade pip`

  - Output content of current VE:
    - `pip freeze > requirements.txt`

  - Env vars manager lib:
    - `pip install django-environ`

- VS-code-related commands:
  - Create .gitignore: CTRL + Shift + P

- ngrok-related commands:
  - Install:
    - `sudo snap install ngrok`

  - Connect:
    - `ngrok http 8000`

- API Schema Generation: $ python manage.py spectacular --file api.yaml

- For SSH Access: $ git@github.com:username/repo_name.git
- PAT: $ https://username:PERSONAL_ACCESS_TOKEN@github.com/username/repo.git

- Environment Variable Setup:

1- Install libs:

```bash
pip install django-environ
```

2- create .env.dev and .env.prod in the root

- PostgreSQL Setup:

1- Install libs:

```bash
pip install psycopg[binary]
```

** Postgress Local Connection **

- Run psql: $ sudo -u postgres psql
- Quit psql: $ \q
- List all users: $ \du
- Remove user: $ DROP USER IF EXISTS username;
- List all DBs: $ \l
- Remove DB: $ DROP DATABASE database_name;
- Create new user: $ CREATE USER myuser WITH PASSWORD 'mypassword';
- Create new DB: $ CREATE DATABASE mydb OWNER myuser;
- DB URL: postgresql://{env('DB_USER')}:{env('DB_PASSWORD')}@localhost:5432/{env('DB_NAME')}
- Grant full permission: $ ALTER ROLE myuser SET client_encoding TO 'utf8';
  $ ALTER ROLE myuser SET default_transaction_isolation TO 'read committed';
  $ ALTER ROLE myuser SET timezone TO 'UTC';
  $ GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;

- CREATE DATABASE your_database_name;
- CREATE USER your_username WITH ENCRYPTED PASSWORD 'your_password';
- GRANT ALL PRIVILEGES ON DATABASE your_database_name TO your_username;

# Chapter 1: Initial Set Up

- Initial set up of every new technology you learn, is a headache but you have to do it once correctly to avoid further headaches.

- Learning Goals:
  - What is Shell?
  - Most used shell commands
  - Install Python
  - Set up virtual environment
  - Use git as version control

## What is Shell?

    - Command line:
        text-only interface,
        used for executing programs, installing software, using Git, connecting to servers in the cloud
        terms refer to the command line:
            Command Line Interface (CLI)
            Console: text-based app
            Terminal: program that opens up a new window to access CL
            Shell: program that runs commands on the underlying OS
            Prompt: where commands are typed and run, $ for Linux prompt, > for Windows and % for macOS.
            PowerShell: built-in terminal & shell on windows
            Terminal: built-in terminal on mac & linux

    - Shell Access:
        - Windows:
            search for “PowerShell” in taskbar search
        - Ubuntu & Mac:
            search for “terminal”,
            Ctrl + Alt + T in ubutnu

    - A Mac Tip:
        Since 2019, zsh is the default macOS shell (% prompt).
        Bash is the previous default macOS shell ($ prompt).

## Most used shell commands

    $ whoami: computer name/username
    $ # some command: not executed, # comment symbol
    $ echo “Hi!”: print sth
    $ pwd: print working dir
    $ cd {dir's_name}: change dir
    $ mkdir {dir's_name}: make new dir
    $ ls: list the dir/file
    $ clear: clear the terminal
    $ exit: close the terminal


    - Command autocomplete: > key in windows, tab in linux/mac
    - ↑ and ↓ keys cycle through previous commands

    * For more commands: https://ss64.com/

## Install Python

    - On Windows: Type “python” in the search bar and select the latest version of Python on the Microsoft Store and to download it.

To confirm that Python is installed correctly, open a new Terminal window with
PowerShell and type python --version. Then, type python to open the Python
interpreter from the command-line shell. You can exit the Python interpreter by typing either exit() or Ctrl-Z plus
Return.

    - On Mac: On Mac, the official installer on the Python website is the best approach. In a

new browser window, go to the Python downloads page and click on the button
underneath the text “Download the latest version for Mac OS X.” As of this
writing, that is Python 3.12. The package will be in your Downloads directory:
double-click on it to launch the Python Installer, and follow the prompts.
To confirm the download was successful, open a new Terminal window and type
python3 --version.

---

title: "Introduction"
lang: en
handle: introduction
layout: default

---

# Chapter 0: Introduction

## Django Properties:

- free & open-source web framework
- written in Python
- “batteries-included” approach provides all the built-in functionality you need to create powerful, real-world web applications quickly
- a “loosely coupled” framework, Django’s components work independently or together, allowing for a high degree of modularity. In
  other words, you only have to use (and learn) what you need.

Same patterns and tasks arise in almost every Django website:

- create and structure a new project
- connect to and query a database
- add logic
- perform CRUD (Create-Read-Update-Delete) operations
- handle user accounts and forms

There is a built-in solution for almost every conceivable use case: that’s what the documentation is for! But no one, even the
original creators and core developers who wrote much of the documentation, can keep it all in their heads. You shouldn’t attempt to either!

In this book, you will learn how to build, test, and deploy six progressively more
complex web applications.

Why Learn Django?

- Django was initially created in the fall of 2003 at the Lawrence Journal-World
  newspaper
- named after the famous jazz guitarist Django Reinhardt
- it was released as a free, open-source project in July 2005
- written in the wonderfully readable yet powerful Python programming
  language
- inherited Python’s “batteries-included” approach and includes a wide
  range of built-in features for routine tasks in web development, including:

-- ORM (Object-Relational Mapper): write Python rather than raw SQL for
creating and querying database tables

-- Authentication: a full-featured and secure system for user accounts,
groups, permissions, and cookie-based user sessions

-- Templating Engine: a simple syntax for adding variables and logic to
create dynamic HTML

-- Forms: a powerful form library that handles rendering and validation

-- URL Routing: a clean, elegant URL schema that is easy to maintain and
reason about

-- Admin Interface: a visual way to interact with all website data, including
users and database tables

-- Internationalization: multilingual support plus locale-specific formatting
of dates, time, numbers, and time zones

-- Security: protection against SQL injection, cross-site scripting, cross-site
request forgery, clickjacking, and remote code execution

## Flask

- micro framework approach
- provides only the bare minimum required for a simple web page
- far more lightweight than Django
- allows for maximum flexibility
- requires adding more third-party packages
- Flask project structure often varies widely, more difficult to move between projects and maintain best practices within the community

There is a saying among long-time Django developers, “Come for the
framework, stay for the community.” And it is true! Django has an unusually
warm and welcoming community for all levels of programmer, represented in
annual volunteer-run DjangoCon conferences across multiple continents, an
active forum for discussion, and regular meetups in major cities.

## Django Version's Rule

- Django 5.0 was released in December 2023 and has official support for Python
  3.10, 3.11, and 3.12
- Django’s versioning policy is time-based rather than feature-based
- Django also follows the pattern of .0, .1, .2, and then back to .0 for feature
  releases, meaning you can expect Django 5.1 in August 2024, Django 5.2 in
  April 2025, Django 6.0 in December 2025, and so on
- Specific releases (those that end in .2, like Django 5.2 and 6.2) are designated as
  long-term support (LTS) releases and receive security and data loss fixes applied
  for a guaranteed period, typically three years
- Still, the best security policy is to be on the latest possible release rather than an LTS version if you can.

Django: - the web framework for perfectionists with deadlines - a free and open-source web framework written in Python
Its origins: a newspaper content management system (CMS)

Django also emphasized a “batteries-included” approach similar to
Python, providing built-in solutions for most tasks while still allowing customization.

## Why Django?

Django was initially created in the fall of 2003 at the Lawrence Journal-World
newspaper and named after the famous jazz guitarist Django Reinhardt; it was
released as a free, open-source project in July 2005. That makes it almost twenty
years old now, quite mature in software terms, but it has continued to thrive and
is arguably more vibrant today than ever before.

Django is written in the wonderfully readable yet powerful Python programming
language, arguably the most popular language in the world today. Python is the
default choice in most undergraduate computer science curriculums, the
dominant language for data science and artificial intelligence, and widely used in
scientific research. Its ease of use and broad applicability make Python suitable
for almost any task.

There is a saying among long-time Django developers, “Come for the
framework, stay for the community.” And it is true! Django has an unusually
warm and welcoming community for all levels of programmer, represented in
annual volunteer-run DjangoCon conferences across multiple continents, an
active forum for discussion, and regular meetups in major cities. Unlike other
open-source projects run by companies or individuals, Django is organized as a
non-profit organization via the Django Software Foundation, whose goal is to
promote, support, and advance the web framework. Its Board of Directors is
voted on annually by the community.

## Django Features

Django inherited Python’s “batteries-included” approach and includes a wide range of built-in features for routine tasks in web development, including:
ORM (Object-Relational Mapper): write Python rather than raw SQL for
creating and querying database tables
Authentication: a full-featured and secure system for user accounts,
groups, permissions, and cookie-based user sessions
Templating Engine: a simple syntax for adding variables and logic to
create dynamic HTML
Forms: a powerful form library that handles rendering and validation
URL Routing: a clean, elegant URL schema that is easy to maintain and
reason aboutAdmin Interface: a visual way to interact with all website data, including
users and database tables
Internationalization: multilingual support plus locale-specific formatting
of dates, time, numbers, and time zones
Security: protection against SQL injection, cross-site scripting, cross-site
request forgery, clickjacking, and remote code execution
