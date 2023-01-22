---
title: "Build a Website With Hugo and Deploy to Firebase"
date: 2023-01-22T10:33:14+05:30
description: Build a Website With Hugo and Deploy to Firebase
authorbox: true
sidebar: false
pager: true
thumbnail: "img/hugo.png"
categories:
  - "Knowledge"
  - "Development"
tags:
  - "HUGO"
  - "DEV-OPS"
  - "DEVELOPMENT"
  - "AUTOMATION"
  - "FIREBASE"
---

## HUGO

### What is HUGO?
**Hugo** is a static site generator written in `Go`. It is designed to be fast and flexible, and can be used to create websites of any kind, from blogs to portfolios to documentation sites. Hugo can be customized using templates and can be configured using a TOML, YAML, or JSON configuration file. It is known for its speed and ability to handle large numbers of pages and media files.

---

### Installation
In MAC, We will be using ***HomeBrew*** to install **HUGO**. It is also very easy to install on other operating systems. Please refer to the complete installation guide [here | *Installation Guide*](https://gohugo.io/installation/)

***Installing on MAC***
```bash
brew install hugo
```

> I'm using a Linux machine, The screenshots and commands shown below are specific to a Linux environment, as that is the operating system being used.

***Installing on Linux***
```bash
sudo snap install hugo
```

Once Installed, You should be able to  execute `hugo --help` in you `terminal`. You should see an output as in the screen-shot below

![hugo](../images/hugo-1.png)

---

### Basic Commands

At this point, You have successfully installed **HUGO**. Now lets look at some of the basic commands of hugo.

```bash
# Show Hugo help
hugo --help

# Create a new Hugo Website/Project
hugo new site project-name --force

# Start Hugo Server
hugo server

# Start Hugo server, also show posts in draft mode
hugo server -D

# Create new post
hugo new posts/new-post-name.md

# Build the Hugo website for publishing/hosting
hugo
```

---

## Building a new Website

Now, lets start building your new blogging website. First, lets create a project
```bash
hugo new site project-name --force
```
![hugo](../images/hugo-2.png)

Once the project is created, You should have a folder created as `project-name` with the following structure

![hugo](../images/hugo-3.png)

The folders above should be empty when generated. Let’s breakdown what each folder is used for.

> detailed information about folder structure can be found [here](https://gohugo.io/getting-started/directory-structure/)

- **archetypes**: In Hugo, front matters are metadata that hold tiny information about our site content (date, title, draft). Archetypes contain custom preconfigured front matters.
- **content**: All content for your website lives inside this directory. Each top-level folder in Hugo is considered a content section. For example, if your site has three main sections — blog, articlesand tutorials—you will have three directories at content/blog, content/articlesand content/tutorials
- **data**: This directory is used to hold configuration files used by Hugo when generating your website. You can write configurations in JSON, YAML or TOML.
- **layout**: This folder is used to store templates in the form of “.html” files that specify how views of your content will be rendered into a static website.
- **static**: Stores all the static content: images, CSS, JavaScript, etc.


If you look at the **themes** folder, You should see that the **themes** folder is still empty. You will have to do download a theme. You can download the theme from [here](https://themes.gohugo.io/).

For this tutorial, Lets use [Maverick](https://themes.gohugo.io/themes/maverick/)

![hugo](../images/hugo-4.png)
Please follow the ***Installation Instructions*** in the theme page, The main goal is to download the the theme and place it in the `themes` folder.

Also copy the contents of `exampleSites` to `project-name` folder. Once all these steps are completed. Your Project Folder should look like.

![hugo](../images/hugo-5.png)

---

### Start HUGO Server

Now, you are ready to run your website for the first time. In you project folder `project-name`, execute the following command. This should start the hugo server.

```bash
hugo server -D
```
![hugo](../images/hugo-7.png)


Now your hugo server will be running, this can be accessed in [http://localhost:1313/](http://localhost:1313/)

![hugo](../images/hugo-6.png)

---

### Create New Post

Now to create a **New Post**, You need to create new `.md` file in `./content/posts` folder. You can also use a hugo command to create the new file.

```bash
hugo new posts/new-post-name.md
```
---

### Build Static Pages
Now that you have your posts ready, You can use the `hugo` command to create the static `html` files. Run the command in `project-name` folder

```bash
hugo
```
![hugo](../images/hugo-8.png)

wow!! Your ***New Blog*** is ready to be hosted.

---






