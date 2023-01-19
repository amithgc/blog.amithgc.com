---
title: "SQLite Cheat-Sheet"
date: 2023-01-18T19:17:56+05:30
authorbox: true
sidebar: false
pager: true
weight: 2
categories:
  - "Cheat Sheets"
tags:
  - "Cheat-Sheet"
  - "DATABASE"
  - "DEV-OPS"
---

SQLite is a relational database contained in a C library. In contrast to many other databases, SQLite is not a client-server database engine. Rather, it's embedded into an end program.

SQLite generally follows the PostgreSQL ([[postgres]]) syntax but does not enforce type checking.

You can open a SQLite Database with `sqlite3 <filename>` directly.

## Commands

`.help` Shows all commands `.databases` Show all existing databases `.quit` Exists `.tables` Shows all tables `.backup` Backups current database