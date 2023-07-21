---
title: "How to Generate PDF's using Java"
date: 2023-07-21T12:17:12+05:30
description: How to Generate PDF's using Java
authorbox: true
sidebar: false
thumbnail: "img/pg.png"
pager: true
categories:
  - "Knowledge"
  - "Development"
tags:
  - "DEVELOPMENT"
  - "AUTOMATION"
---


## Introduction

Ah, the age-old problem of mundane tasks sucking up our precious time! Picture this: you, a busy individual juggling multiple responsibilities, faced the dreaded ***monthly ritual of uploading phone bills, fuel bills, and rent receipts***. Oh, the horror! Frankly, there's nothing worse than being caught in a never-ending cycle of paperwork. But fear not, fellow bill-bearer, for I embarked on a quest to liberate myself from the shackles of bill generation drudgery!

Thus, in a stroke of brilliance (or perhaps desperation), the PDF Bill Generator was born! This open-source project was conceived with the sole purpose of rescuing busy souls from the clutches of repetitive billing tasks.

Here is the **GitHub Repo**, Please free to Use the Code
<a href="https://github.com/amithgc/BillGenerator" target="_blank">[ View GitHub Repo ]</a>

## Overview

The Bill Generator is a powerful Java-based tool that allows you to effortlessly generate bills using a **base PDF file** as a template and a **JSON data file** to define the text placement. Whether you're running a small business, managing finances for a project, or just need to create customized bills, this tool has got you covered!

## Features

-   **Easy to Use:** With a simple command-line interface, you can quickly generate bills without any hassle.
    
-   **Customizable Templates:** The tool utilizes a base PDF file as a template, giving you complete freedom to design your bill's layout. Just create your perfect template once, and you're ready to generate countless customized bills.
    
-   **JSON Data Integration:** Simply provide a JSON file with the required text details and their respective positions on the bill. The tool will seamlessly merge the data with the template, saving you valuable time.
    
-   **Font and Styling Options:** Customize the appearance of your bills with various font styles, colors, and font sizes to make them look professional and appealing.

![](../images/bg.png)


## Getting Started

To generate your bills, follow these simple steps:

1.  **Clone the Repository:** Start by cloning this repository to your local machine.
    
2.  **Compile the Code:** Use your favorite Java compiler to compile the code.
    
3.  **Prepare Your Template:** Ensure you have a base PDF file that will act as the template for your bills. Make sure it contains the necessary placeholders for the text elements you want to insert dynamically.
    
4.  **Create JSON Data:** Craft a JSON file containing the text details, positions, font styles, and colors for each element you want to place on the bill. Refer to the provided example JSON file for guidance.
    
5.  **Run the Application:** Use the command-line interface to specify the required options, including the template name, JSON input file, and the output PDF file path. For example:
    
 ```shell
 java -jar billGenerator.jar -t ./data/base-pdf/bill-template.pdf -j ./data/json/bill-data.json -o ./output/bill.pdf
 ``` 
    
6.  **Voila!** Your customized bill will be generated and saved at the specified output location.
    

## Example JSON Data

The JSON file should contain an array of objects, each representing a text element to be placed on the bill. Here's an example:

```json

[
  {
    "text": "Your Company Name",
    "locationX": 50,
    "locationY": 100,
    "fontSize": 14,
    "color": "#336699",
    "font": "Roboto-Bold.ttf"
  },
  {
    "text": "Invoice Number: 123456",
    "locationX": 60,
    "locationY": 200,
    "fontSize": 11,
    "color": "#444444",
    "font": "Helvetica-Regular.ttf"
  },
  {
    "text": "Total Amount: $100.00",
    "locationX": 80,
    "locationY": 250,
    "fontSize": 12,
    "color": "#222222",
    "font": "Arial-Bold.ttf"
  },
  {
    "enricher": "RandomNumber",
    "locationX": 125,
    "locationY": 300,
    "fontSize": 11,
    "color": "#222222",
    "font": "VictorMono-Bold.ttf"
  }
]
```

In this example, the JSON data instructs the tool to place various texts at specific positions on the bill and apply different font styles and colors.

## Extensibility using Enrichers

The Bill Generator is designed to be highly extensible, allowing users to enhance its functionality by incorporating custom enrichers. Enrichers are small modules that generate dynamic text values based on specific rules or calculations. As an example, let's explore the built-in `RandomNumber`, `DateToday`, and `TimeNow` enrichers, and then see how you can easily create your own enrichers.

### Built-in Enrichers

#### RandomNumber

The `RandomNumber` enricher generates a random 10-digit number, which can be useful for creating unique identifiers such as invoice numbers or bill numbers. In the example JSON file, you can see the `RandomNumber` enricher in action:

```json
{
  "enricher": "RandomNumber",
  "locationX": 125,
  "locationY": 300,
  "fontSize": 11,
  "color": "#222222",
  "font": "VictorMono-Bold.ttf"
}
```

This enricher will produce a random 10-digit number at the specified location on the PDF bill.

#### DateToday

The `DateToday` enricher generates the current date in the desired format. You can use it to automatically add the current date to your bills. To use the `DateToday` enricher, you would modify your JSON data like this:

```json
{
  "enricher": "DateToday",
  "locationX": 80,
  "locationY": 260,
  "fontSize": 11,
  "color": "#444444",
  "font": "Helvetica-Regular.ttf"
}
``` 

When processed, the `DateToday` enricher will insert the current date in the format "dd/MM/yyyy" at the specified location.

#### TimeNow

The `TimeNow` enricher works similarly to the `DateToday` enricher, but it generates the current time. Here's an example of how to use it in your JSON data:

```json
{
  "enricher": "TimeNow",
  "locationX": 80,
  "locationY": 280,
  "fontSize": 11,
  "color": "#444444",
  "font": "Helvetica-Regular.ttf"
}
``` 

This will place the current time in the format "HH:mm a" on your bill.

### Creating Custom Enrichers

The true power of the Bill Generator lies in its extensibility, allowing you to create custom enrichers tailored to your specific needs. To create a new enricher, follow these steps:

1.  Implement the `IEnricher` Interface: Start by creating a new Java class that implements the `IEnricher` interface. This interface ensures that your enricher will have the necessary methods for processing and retrieving the enricher's name.
    
2.  Annotate with `@Enricher`: Add the `@Enricher` annotation to your custom enricher class. This annotation marks the class as an enricher, allowing the Bill Generator to identify and utilize it.
    
3.  Define the Enricher's Functionality: Within your enricher class, define the logic to generate the dynamic text you want to insert into the bill. In the example below, we'll create an enricher that generates a random discount percentage:
    

```java

package com.amithgc.billgenerator.enricher;

import com.amithgc.billgenerator.enricher.utils.Enricher;

import java.util.Random;

@Enricher
public class RandomDiscountEnricher implements IEnricher {
    @Override
    public String getName() {
        return "RandomDiscount";
    }

    @Override
    public String process() {
        return String.format("%.2f", generateRandomDiscount());
    }

    private double generateRandomDiscount() {
        Random random = new Random();
        return random.nextDouble() * 50; // Generates a random discount between 0 and 50%
    }
}
``` 

4.  Utilize the Custom Enricher: Once you've created your custom enricher, you can use it in your JSON data just like the built-in enrichers:

jsonCopy code

```json
{
  "text": "RandomDiscount",
  "locationX": 80,
  "locationY": 320,
  "fontSize": 11,
  "color": "#444444",
  "font": "Helvetica-Regular.ttf"
}
``` 

This example will apply your custom enricher, `RandomDiscount`, to generate a random discount percentage and display it on the bill.

With the ability to create custom enrichers, the possibilities for dynamically generating content in your bills become limitless. Get creative and build enrichers to suit your unique requirements!

----------

By harnessing the power of enrichers, the Bill Generator opens up a world of possibilities for generating dynamic and customized bills. Whether you're utilizing the built-in enrichers or creating your own, the tool empowers you to streamline your billing process and produce professional and appealing invoices. So, why wait? Start generating stunning bills with ease and take your billing experience to the next level! 💰📄


-----

## Automation with GitHub Actions and Telegram Integration
Not only did I create the PDF Bill Generator to revolutionize bill generation, but I took it a step further by automating the entire process! Yes, you heard that right – no more manual execution or tedious tasks. Thanks to the power of GitHub Actions and Telegram integration, generating PDF bills has become a breeze.

**GitHub Actions** - Bill Generation on Autopilot
With GitHub Actions, I've set up an automated workflow that executes the PDF Bill Generator whenever I need a PDF bill, whether it's for a phone bill, fuel bill, or rent receipt. No more manually triggering the tool – it's like having a trusty bill-generating assistant at my beck and call!

The GitHub Actions workflow can be tailored to suit your specific needs, whether you want the bills generated at specific intervals, upon certain events, or as part of your release process. Simply define your workflow in a YAML file, and let GitHub Actions handle the rest.

**Telegram Integration** - Bills at Your Fingertips
But wait, there's more! The automation doesn't stop there. Thanks to Telegram integration, I receive the generated PDF copies directly on my Telegram account. Gone are the days of checking emails or searching through folders to find the bills. With Telegram notifications, the bills are delivered right to my fingertips.

Telegram integration is highly customizable and can be configured to send notifications to your personal or group chats. Now, I can access my bills on-the-go, anytime, anywhere. It's like having a bill delivery service that follows me wherever I wander!

How to Set Up GitHub Actions and Telegram Integration
Now, I know you might be curious about how to set up this magical automation for yourself. Fear not, for I've documented the process in my other blogs. To learn how to leverage the power of GitHub Actions and integrate it with Telegram for bill delivery, head over to my other blogs for step-by-step guides and helpful tips.

Embrace the Future of Automated Billing
With the PDF Bill Generator, GitHub Actions, and Telegram integration, you can unlock the full potential of automation and bid farewell to manual bill generation forever. Embrace the future of streamlined invoicing and focus your time and energy on more important tasks, while the tools do the heavy lifting for you.

So, why settle for mundane paperwork when you can experience the bliss of automated billing? Get started today and join the league of bill-generating superheroes!

Sit back, relax, and let automation take the wheel! Your bills are just a few clicks away. 🤖💬

----

#### License

This project is licensed under the [MIT License](https://chat.openai.com/LICENSE).

#### Contribution

We welcome contributions! If you have any ideas for improvements, bug fixes, or new features, feel free to open an issue or submit a pull request.

We encourage you to write more enrichers and help other users

#### Support

If you encounter any issues or have questions about using the Bill Generator, please [open an issue](https://github.com/amithgc/BillGenerator/issues).

----------

Get ready to revolutionize the way