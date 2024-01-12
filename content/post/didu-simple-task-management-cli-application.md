---
title: "Building Didu - The Todo CLI that Asks, 'Did U?'"
date: 2024-01-11T12:17:12+05:30
description: Building 'Didu' - The Todo CLI that Asks, 'Did U?'
authorbox: true
sidebar: false
thumbnail: "img/didu.png"
pager: true
categories:
  - "Knowledge"
  - "Development"
tags:
  - "DEVELOPMENT"
  - "AUTOMATION"
---

Are you tired of juggling tasks in your mind or scribbling them on sticky notes that mysteriously disappear? Fear not, fellow developers and productivity enthusiasts! I've created a solution that's as fun to use as its name suggests. Say hello to Didu (pronounced "Did U?"), your new command-line buddy for task management.

----------

## What is Didu?

Didu is a Command-Line Interface (CLI) application for managing tasks. It's like that little voice in your head that constantly reminds you of things to do, but less annoying and more organized. Didu stands out with its blend of simplicity and powerful features, making task management a breeze.
Didu is designed for developers who love the terminal more than their pets. It's sleek, efficient, and less annoying than daily stand-up meetings.


**GitHub Repo**,
<a href="https://github.com/amithgc/didu" target="_blank">[ View GitHub Repo ]</a>
**NPM Repo**, 
<a href="https://www.npmjs.com/package/didu" target="_blank">[ View NPM Repo ]</a>

## How it Works and Features
<p align="center">
  <img src="https://raw.githubusercontent.com/amithgc/didu/main/media/demo-video.webp" style="width: 100%;"/>
</p>

## Features

- **Add Tasks Quickly:** Effortlessly add new tasks to your list.
- **Flexible Task Searching:** Use fuzzy search to find and update tasks.
- **Task Status Management:** Easily mark tasks as pending or done.
- **Delete Tasks:** Remove tasks that are no longer needed.
- **Intuitive Command Usage:** Simple commands for all operations.
- **Color-Coded Display:** Visually appealing and easy to read task statuses.

----------


## Installation

Install **Didu** globally via npm:

```bash
npm install -g didu 
```

**Didu** is designed to be straightforward and intuitive. Here are the basic commands:

## Usage

```
  Usage:

    didu add <task>          Creates a new task
    didu                     Lists all pending tasks
    didu ls                  Lists all pending tasks, Changes the status once selected
    didu ls all              Lists all tasks, Changes the status once selected
    didu ls done             Lists all completed tasks, Changes the status once selected
    didu ls pending          Lists all pending tasks, Changes the status once selected
    didu pretty              Displays all tasks
    didu pretty all          Displays all tasks
    didu pretty done         Displays all done tasks
    didu pretty pending      Displays all pending tasks
    didu rm                  Lists all tasks for removal
    didu rm all              Lists all tasks for removal
    didu rm done             Lists all completed tasks for removal
    didu rm pending          Lists all pending tasks for removal
    didu clear               Deletes all done tasks
    didu clear all           Deletes all tasks
    didu clear done          Deletes all done tasks
    didu clear pending       Deletes all pending tasks
    didu help                Displays this help information

  ```


#### Quick Task Addition
```bash
didu add "Learn to cook without setting off the fire alarm"
```
Adding tasks is as easy as convincing a developer that a new JavaScript framework is worth learning.

#### Fuzzy Search
```bash
didu ls all
```
Fuzzy search is like your grandma finding her glasses. She knows they're there; it just takes a bit of looking around.

----------

## Under the Hood of Didu: A Peek at the Code

Now, let's don our developer hats and dive into the mechanics of Didu.

### The `didu` Binary

The entry point is `./bin/didu`. Here, we set up the database path and initialize the tasks module.

```javascript
#!/usr/bin/env node
const argv = require('argvee')();
const path = require('path');
const Database = require('../lib/database');
const Tasks = require('../lib/tasks');
// ...additional setup and error handling
try {
  require(`../lib/cli/${command}`)(argv, tasks);
} catch (e) {
  // Error handling for unrecognized commands
}
```

### Task Management in `./lib/tasks.js`

This file is the backbone of our task management system. We have functions like `list`, `create`, `check`, and `rm` to handle various task operations.

```javascript
function Tasks(database) {
    this.database = database;
}
// ... Task prototype methods for various operations
module.exports = Tasks;
```

### The Task Model in `./lib/task.js`

Each task is an instance of the `Task` class with attributes like `id`, `desc`, `status`, and `modified`.

```javascript
function Task(id, desc, status, modified) {
    // ... Assertions and initialization
}
// ... Task prototype methods and toJSON
module.exports = Task;
```

### Database Interactions in `./lib/database.js`

The `Database` class handles reading and writing tasks to a JSON file, providing persistence for our tasks.

```javascript
function Database(path) {
    this.path = path;
}
// ... read and write methods
module.exports = Database;
```

## Deploying Didu to NPM

The grand finale of our journey was deploying Didu to NPM using GitHub Actions. Here's a snippet from our workflow:

```yaml
name: Publish to NPM
on: workflow_dispatch
jobs:
  build:
    // ... setup steps
    - name: Publish package on NPM 📦
      run: npm publish
      env:
        NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

Deploying with GitHub Actions felt like sending a spacecraft to orbit – a moment of tension followed by immense satisfaction.

## Conclusion

Building Didu was a journey filled with coding, debugging, and a bit of laughter (mostly at my own silly mistakes). It's a simple yet powerful tool that I hope will bring some organization and color to your CLI experience. Happy task managing with Didu!

----

#### License

This project is licensed under the [MIT License](https://chat.openai.com/LICENSE).

#### Contribution

We welcome contributions! If you have any ideas for improvements, bug fixes, or new features, feel free to open an issue or submit a pull request. We encourage you to write more enrichers and help other users

#### Support

If you encounter any issues or have questions about using the Bill Generator, please [open an issue](https://github.com/amithgc/BillGenerator/issues).

----------

*Remember, Didu only helps manage tasks. It won't do them for you. Yet.* 🚀👨‍💻
