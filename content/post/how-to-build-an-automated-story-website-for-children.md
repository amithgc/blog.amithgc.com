---
title: "How to Build an Automated Story Website for Children"
date: 2023-07-12T12:17:12+05:30
description: How to Build an Automated Story Website for Children
authorbox: true
sidebar: false
thumbnail: "img/how-to-stories.png"
pager: true
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

## Introduction
### Demo
Before you dive into the realm of story-generating magic, take a moment to witness the awesomeness that awaits you at <a href="https://stories.amithgc.com/" target="_blank">stories.amithgc.com</a>. Brace yourself for a whimsical journey through the realm of imagination!


### Goal
Welcome to the wacky world of automated storytelling! Our mission: to create a website that hosts enchanting stories exclusively for children. We've set our sights on banishing manual labor from the equation and automating everything in sight. We're talking stories generated daily and posted effortlessly, accompanied by beautiful images magically conjured to bring the tales to life. And we won't lift a finger to make it happen (except for typing this blog, of course)!

So fasten your seatbelts, folks, because we're about to embark on an adventure that would make even the most talented fairy godmother raise an eyebrow. Get ready to witness the birth of a website that would make Mother Goose herself green with envy!

### Requirements
So, you're up for the challenge of building an automated website that spins magical tales? Excellent! But before we sprinkle our programming prowess, let's go over the ingredients you'll need for this whimsical recipe:

- **Java Programming Language**: You should have some experience or at least a friendly acquaintance with **Java**. Don't worry, we won't ask you to cast any complicated spells or turn frogs into princes. Just enough Java knowledge to work some coding magic.

- **GitHub Account**: As we embrace the powers of automation, we'll be summoning the mystical energies of **GitHub Actions**. So, make sure you have an account ready. Because let's face it, even the greatest wizards need a place to store their magical potions and incantations.

- **Hugo Know-How**: Prepare to befriend a magical creature called **Hugo**. We'll be relying on its spellbinding abilities to publish our captivating stories. If you haven't met Hugo yet, fear not! I have a blog post dedicated to unraveling the secrets of this fantastical creature. Make sure to give it a read.

- **Firebase Account**: We're not building an ordinary website here; we're crafting a portal to enchantment! To host our creation, we'll need the powers of **Firebase**. So, make sure you have an account ready. Who said magic was free?

- **OpenAI Membership**: Prepare to tap into the creative forces of **OpenAI**. We'll be summoning the mighty GPT (that's short for "Generative Pre-trained Transformer") to weave our tales of wonder. So, make sure you have an account with OpenAI. And don't worry, they won't ask you to cast any Avada Kedavra spells during the registration process.

- **leonardo.ai Account** *(Optional)*: For an extra sprinkle of enchantment, you can also create captivating images to accompany our stories. One option is to join the illustrious ranks of **leonardo.ai**, where imagination takes shape. However, if you prefer to keep your magic potion streamlined, fear not! We can also conjure images using the sorcery of **Dall-E**, courtesy of OpenAI.

Congratulations, my aspiring sorcerer of storytelling! Gather these elements, and we shall embark on an epic quest to create an automated website that would make even Merlin himself raise an eyebrow in awe. Are you ready to unlock the secrets of digital enchantment? Let the journey begin!

## Plan
Hold on to your wizard hats because here's the grand plan, or as I like to call it, the "flow of enchantment":

**Java Spellcasting**: First, we'll summon the power of Java to conjure a **random prompt**. This prompt will serve as the magical catalyst for our story generation using OpenAI's GPT Model. Remember, the key to a good story is a pinch of randomness!

**Decoding the Magic**: Once the story is magically woven by GPT, our Java incantations will come into play again. We'll unravel the mysterious text and extract its hidden meaning. Why, you ask? Because we need to generate enchanting images to accompany our tales! It's all about painting a vivid picture in the minds of our young readers.

**Summoning the Visual Sorcery**: With our story in hand, it's time to cast a spell upon leonardo.ai. By invoking its name, we shall procure captivating images that bring our tales to life. Of course, if you haven't joined the leonardo.ai ranks, fear not! We can also tap into the mystical powers of OpenAI's Dall-E to generate the necessary images. Though, I must admit, I find Dall-E's image dimensions a bit... squashed. But hey, we'll work with what we have!

**Java Code Incantation, Part Two**: Armed with both our bewitching story and its accompanying images, we'll now channel the power of Java once more. We'll craft a mesmerizing **MarkDown file** that perfectly captures the essence of our tale. This file will be our golden ticket to the magical land of Firebase.

**Firebase**: *The Enchanted Host*: Now, it's time to unveil our creation to the world! We'll weave a GitHub action that gracefully transports our MarkDown file to Firebase, where our website shall take shape. Like a majestic phoenix rising from the ashes, our website will emerge, ready to captivate young hearts.

**The Automation Spell**: Last but not least, let's sprinkle some automation into the mix. We'll concoct not one, but two GitHub actions to handle our magical workflow. The first action will summon the story, generate the MarkDown file, and commit it to our GitHub repository. The second action, ever so dutifully, will publish the repository to Firebase, bringing our website to life.

And there you have it, dear magical apprentice! The roadmap to creating a mesmerizing website that generates captivating stories with just a flick of Java's wand. So grab your spellbook and let's cast a spell of digital wonderment!

---


### Java Spellcasting - Generating Prompts

**Let the Constants Play**: It's time to unleash the power of constants! We'll create a magical assortment of random prompts that will ignite our story generator. Feel free to come up with your own wacky topics and categories. How about "Talking Turtles" or "Wizards and Waffles"?

Lets have some Constants to generate the Random Prompts like these
```java
private static String[] topics = {
            "dragons",
            "tigers",
            "aliens",
            "alien planets",
            "Spider-Man",
            "Iron Man",
            "Captain America",
            "Hulk",
            };

    private static String[] categories = {
            "Adventure",
            "Fantasy",
            "Science fiction",
            "Mystery",
            "Historical fiction",
            "Animal",
            "Humor", 
            "Fables and fairy tales"};
```
**The Unique String Picker**: Behold the utility method that can pluck ***n*** unique strings from any array. With this mystical function, we can summon random topics or categories to spice up our stories. No repeated spells, please!

Here is the Utility Method to ***n*** pick unique strings from any of the provided array.

```java
private static String[] pickUnique(String[] array, int count) {
        HashSet<String> selectedSet = new HashSet<>();

        // Create a Random object to generate random indices
        Random rand = new Random();

        // Loop until we have selected enough unique topics
        while (selectedSet.size() < count) {
            // Generate a random index
            int index = rand.nextInt(array.length);
            // Add the topic at the index to the selected set
            selectedSet.add(array[index]);
        }

        // Convert the HashSet to an array and return it
        return selectedSet.toArray(new String[0]);
    }

```
**The Wizardry of Random Prompts**: Brace yourselves for the grand unveiling of the method that generates our random prompts for the magnificent OpenAI's GPT. Feel free to tweak this section to your heart's desire. Let your imagination run wild, just like a unicorn on roller skates!

and, Here is the method which I use to generate the Random Prompt to get the Story generated using OpenAI's GPT, You can change this part as you wish.
```java

    private String generateTextPrompt(BaseContent content) {

        int maxAge = Constants.getMaxAge();
        int totalWords = 1000;

        String categories = Constants.getCategory();
        String topics = Constants.getTopics();

        content.setCategories(new ArrayList<>(Arrays.asList(categories.split(", "))));
        content.setTags(new ArrayList<>(Arrays.asList(topics.split(", "))));

        String initialMessage = "\n" +
                "Write me a " +
                categories +
                " story for children of age " +
                maxAge +
                " with " +
                totalWords +
                " words include " +
                topics;

        String secondaryMessage = "\n" +
                Constants.getInclusion() +
                "\n" +
                "Content you return should have 3 sections with the section names as - TITLE: , STORY: , PROMPT: " +
                "\n" +
                "At the end of the story, Give me a prompt to generate good images depicting the story in dall-e. " +
                "dall-e is a image generation tool. Dont use Ahani and Aarya name in the prompt.";

        content.setTextPrompt(initialMessage);

        return initialMessage + secondaryMessage;
    }

```

As an Example, This method will generate a **prompt** for GTP as below

> Write me a **Animal** story for children of age **14** with **1000** words include **Goblins, Magic spells and potions, Cursed objects, dragons** *Your story should also include a 8 year old boy named Aarya in a negative role and a 11 year old girl named Ahani in a positive role*. Content you return should have 3 sections with the section names as - TITLE: , STORY: , PROMPT: At the end of the story, Give me a prompt to generate good images depicting the story in dall-e. dall-e is a image generation tool. Dont use Ahani and Aarya name in the prompt.

**The Marvelous Output**: Now, after the magical code has completed its incantations, OpenAI will grant you the gift of a complete story along with a prompt for image creation. Behold the sample output (responseString) that holds the key to a world of wonder and imagination. Prepare to be amazed!

Now with this prompt, make an API hit to OpenAi, to get the Story Generated.

```java
    final List<ChatMessage> messages = new ArrayList<>();
            final ChatMessage systemMessage = new ChatMessage(ChatMessageRole.SYSTEM.value(), "You are a great story teller, You are an expert children story book author.");
            final ChatMessage userMessage = new ChatMessage(ChatMessageRole.USER.value(), message);
            messages.add(systemMessage);
            messages.add(userMessage);

            ChatCompletionRequest chatCompletionRequest = ChatCompletionRequest
                    .builder()
                    .model("gpt-3.5-turbo")
                    .messages(messages)
                    .n(1)
                    .maxTokens(2000)
                    .logitBias(new HashMap<>())
                    .build();

            List<ChatCompletionChoice> response = service.createChatCompletion(chatCompletionRequest).getChoices();

            if (response != null && !response.isEmpty()) {
                responseString = response.get(0).getMessage().getContent();
            }
```

Now after this code executes, OpenAI should return you the complete **story** and the **prompt for image creation**., Here is a sample output (*responseString*)

>
>
>**TITLE**: The Enchanted Forest Adventure
>
>**STORY**:
>Once upon a time, in a small village nestled on the edge of an enchanted forest, lived a young girl named Ahani. She was eleven years old and had a heart full of curiosity and kindness. Ahani loved exploring the forest and had heard stories of magical creatures that dwelled within its depths. However, the villagers also spoke of goblins that lurked in the shadows, causing mischief and chaos wherever they went.
>
>One sunny morning, as Ahani ventured into the enchanted forest, she stumbled upon a hidden clearing. To her surprise, she found a tiny cottage covered in ivy and moss. Intrigued, Ahani cautiously entered the cottage. Inside, she discovered an array of spellbooks, potions, and mysterious objects. Ahani's eyes sparkled with excitement as she realized she had stumbled upon a magical hideaway.
>
>Just as she was about to explore further, a mischievous goblin named Aarya appeared. Aarya was only eight years old but had a knack for trouble. He had discovered the secret cottage and had been using its contents for his own selfish desires. Aarya loved playing pranks on the villagers and causing mischief wherever he went.
>
>Aarya, seeing Ahani in the cottage, smirked and decided to play a trick on her. He grabbed a cursed object—a small, shiny pendant—and waved it in the air. With a flick of his wrist, he recited an ancient incantation, not realizing the pendant had the power to turn anyone who wore it into an animal.
>
>As soon as Aarya finished the incantation, a puff of smoke enveloped the room, and Ahani found herself transformed into a deer. Panic surged through her veins as she realized what had happened. Aarya laughed triumphantly, reveling in his malicious act.
>
>Determined to find a way to break the curse, Ahani, now a graceful deer, set off deeper into the forest. Along her journey, she encountered various magical creatures who were willing to help. She came across a wise old owl who guided her to a hidden dragon's lair. The dragon, known as Ember, possessed ancient knowledge of spells and potions.
>
>Ember sympathized with Ahani's plight and agreed to assist her. The dragon brewed a potion using rare ingredients and whispered ancient incantations to lift the curse. Ahani, now back in her human form, thanked Ember for his kindness.
>
>Armed with the potion, Ahani returned to the cottage where Aarya had been causing more trouble. She approached him with a forgiving heart, offering the potion as a gesture of peace. Aarya, initially skeptical, hesitantly drank the potion. In a brilliant flash of light, he transformed into a tiny goblin mouse.
>
>Ahani, understanding the value of empathy and forgiveness, decided not to leave Aarya in his new form. She carried him on her shoulder, showing him kindness and teaching him the importance of using magic responsibly.
>
>Together, Ahani and Aarya ventured back into the village, now working together to undo the mischievous pranks Aarya had played. The villagers were amazed at the change in Aarya and applauded Ahani for her compassion.
>
>From that day forward, Ahani and Aarya became the village's protectors, using their newfound friendship and understanding of magic to help others. The enchanted forest thrived under their care, and peace was restored.
>
>**PROMPT**: Generate an image depicting a magical forest filled with talking animals, a wise old owl, a curious deer, a mischievous goblin mouse, and a friendly dragon sharing wisdom with the young girl.
>
>

---
### Decoding the Magic: Parsing the response

**Parsing the Story Magic**: With the full story at our fingertips, it's time to unravel its mystical essence. We shall parse the text and construct an object that encapsulates the enchanting narrative. Imagine transforming a dragon's roar into a friendly purr!

Now, construct an object as below

```java

public class BaseContent {
    private String title;
    private String description;
    private String content;
    private String imagePrompt;
    private String textPrompt;
    private String thumbnail;
    private String blogImage;
    private ArrayList<String> tags;
    private ArrayList<String> categories;

    public BaseContent() {
    }
}

```
---
### Summoning the Visual Sorcery - Generating Images

**Summoning Images from leonardo.ai**: And here we are, ready to summon the visual enchantment! We'll need leonardo.ai's aid to generate the mesmerizing images for our tales. By fetching the Image Prompt and utilizing leonardo.ai's mighty APIs, we'll conjure awe-inspiring illustrations that will make unicorns weep with jealousy. Time to press that download button!

![](../images/image-generation.png)

This Java code can be used to generate the Images from **leonardo.ai**
```java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "\n{\n  \"prompt\": \"" + 
        content.getImagePrompt().replaceAll("\n", "")
                .replaceAll("\"", "'") + "\",\n  \"modelId\": \"6bef9f1b-29cb-40c7-b9df-32b51c1f67d3\"," +
        "\n  \"width\": 1152,\n  \"height\": 648,\n  \"num_images\": 2,\"promptMagic\":true}");
Request request = new Request.Builder()
        .url("https://cloud.leonardo.ai/api/rest/v1/generations")
        .method("POST", body)
        .addHeader("accept", "application/json")
        .addHeader("authorization", "Bearer " + Secrets.LEONARDO_KEY)
        .addHeader("content-type", "application/json")
        .build();
Response response = client.newCall(request).execute();

Response response = client.newCall(request).execute();
String responseBodyStr = response.body().string();

```

Similarly, If you wish to get the images generated using **OpenAI's DallE**, here is the code

```java
CreateImageRequest createImageRequest = CreateImageRequest.builder()
    .prompt(content.getImagePrompt())
    .n(1)
    .size("512x512")
    .user("amithgc")
    .build();

List<Image> images = service.createImage(createImageRequest).getData();
if (images != null && !images.isEmpty()) {
    for (Image image : images) {
        saveImage(content, image.getUrl(), true);
    }
}

```

---


### Java Code Incantation - Generating Story Page
Now, brace yourselves for the mystical art of Java code as we conjure the MarkDown file that Hugo craves. Get ready to witness the sorcery of code that dances in perfect harmony with our story and images. Here's the enchanting snippet that weaves the MarkDown file, ready to captivate young minds. Feel free to edit it to suit your magical preferences. And remember, in the realm of coding, even a spell as small as a semicolon can make or break the magic!

```java
 public void generateMDFile(BaseContent content) {
        String filename = content.getTitle();
        filename = filename.replaceAll("[^a-zA-Z0-9\\s]", "")
                .replaceAll("\\n", "").toLowerCase()
                .replaceAll(" ", "-") + ".md";

        String path = "../Website/content/stories/";

        try (BufferedWriter writer = new BufferedWriter(new FileWriter(path + filename))) {
            writer.write("---\n");
            writer.write("title: \"" + content.getTitle() + "\"\n");
            writer.write("date: " + LocalDateTime.now().minusHours(6).format(DateTimeFormatter.ISO_LOCAL_DATE_TIME) + "\n");
            writer.write("description: \"" + content.getDescription() + "\"\n");
            writer.write("authorbox: true\n");
            writer.write("sidebar: true\n");
            writer.write("thumbnail: \"" + content.getThumbnail() + "\"\n");
            writer.write("pager: true\n");
            writer.write("categories:\n");

            for (String category : content.getCategories()) {
                writer.write("  - \"" + category + "\"\n");
            }
            writer.write("tags:\n");
            for (String tag : content.getTags()) {
                writer.write("  - \"" + tag + "\"\n");
            }

            writer.write("---\n\n");
            writer.write(content.getContent());

            if (content.getBlogImage() != null) {
                writer.write("\n\n" + "![](../images/" + content.getBlogImage() + ")" + "\n\n");
            }

            System.out.println("File written successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

---
### Firebase Deployment - Github Actions
**Step 1: GitHub Repository Creation**:
First things first, you need a trusty GitHub repository to house your website's code. Think of it as your very own fortress of digital awesomeness. Create a new repository and fill it with the mystical incantations of your HTML, CSS, and JavaScript spells. Commit your code changes, but beware of the treacherous typo gremlins that lurk in the shadows!

Commit bot of you Java code and the Hugo Base Structure in the same repository, Here is my Code Structure.
- The **StoryGenerator** folder holds the java code to Generate the MarkDown Files.
- The **Website** folder holds the actual hugo files and also the story MarkDown Files.

![](../images/stories-github.png)

**Step 2: Firebase and Its Enchanting Hosting**:
Now that you have your repository in order, it's time to dance with Firebase Hosting. Head over to Firebase and create a magical kingdom for your website. With a flick of the wrist, link your GitHub repository to Firebase Hosting, forging a mystical bond between the two realms. Let the enchantment begin!

**Step 3: The Command-Line Adventure**:
Prepare for a daring command-line escapade! Summon your terminal, navigate to your repository's directory, and cast the spell of the command firebase login. Prove your identity and gain access to the Firebase Kingdom. Then, call forth the almighty command firebase init, selecting the Firebase Hosting option when prompted. Feel the exhilaration as the terminal unfolds a world of possibilities!

**Step 4: Deploying to the Cloud**:
The time has come to ascend to the Cloud Kingdom! Execute the grand command firebase deploy, and watch as your website takes flight, soaring high above the digital horizon. Witness the joyous union of your GitHub repository and Firebase Hosting, as your website becomes accessible to the world.

**Step 5: Revel in the Wonders of Firebase Hosting**:
Congratulations, brave developer! Your website now resides in Firebase Hosting, ready to dazzle the masses. But don't stop there; explore the whimsical features Firebase has to offer. Witness the magic of automatic HTTPS, dynamic content hosting, and even serverless functions. Let your creativity run wild in this digital realm where anything is possible!

And there you have it, dear adventurers! We hope this whimsical guide has brought a smile to your face as you journeyed from GitHub to Firebase Hosting. Now, armed with a pinch of humor and a sprinkling of technical prowess, go forth and publish your website to the world. May your code be bug-free and your imagination boundless!

---
### Automation - Automating All the steps.

To Automate everything what you did above, We need two jobs
 - Compile the Java Code *(Done once, or when the code changes)*
 - Execute the Java Code to generate the Story and Build the MarkDown file. *(Every Day)*
 - Push the generated files to Firebase Hosting. *(Every Day)*

Here is the github action to **Compile Java Code**
```yml
name: Build Project

on:
  workflow_dispatch:

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          ref: main

      - name: Set up JDK 11
        uses: actions/setup-java@v3
        with:
          java-version: '11'
          distribution: 'temurin'
          cache: maven

      - name: Build with Maven
        working-directory: ./StoriesGenerator
        run: mvn -B package --file pom.xml

      - name: Copy the Jar File
        working-directory: ./StoriesGenerator
        run: cp ./target/stories-generator-jar-with-dependencies.jar ./exec/storiesGenerator.jar

      - name: Commit Version Changes to Main
        uses: stefanzweifel/git-auto-commit-action@v4.15.1
        with:
          commit_message: Generated the Jar
```

Here is the github action to **Generate the Stories**

```yml
name: Generate Story

on:
  schedule:
    - cron: '0 2 * * *'

  workflow_dispatch:


jobs:
  generate-story:
    name: Generate Story
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Set up JDK 11
        uses: actions/setup-java@v3
        with:
          java-version: '11'
          distribution: 'temurin'
          cache: maven

      - name: Run
        working-directory: ./StoriesGenerator
        run: java -jar ./exec/storiesGenerator.jar

      - name: Commit Version Changes to Main
        uses: stefanzweifel/git-auto-commit-action@v4.15.1
        with:
          commit_message: Automated Post
```


Here is the github action to **Push the Stories to Firebase Hosting**

```yml
name: Firebase Deploy

on:
  schedule:
    - cron: '10 2 * * *'

  workflow_dispatch:

jobs:
  deploy-to-firebase:
    name: Deploy to firebase
    runs-on: ubuntu-latest
    steps:

      - name: Check out code
        uses: actions/checkout@v2
        with:
          submodules: true
          fetch-depth: 0

      - name: Hugo setup
        uses: peaceiris/actions-hugo@v2.4.12
        env:
          ACTIONS_ALLOW_UNSECURE_COMMANDS: 'true'
        with:
          hugo-version: latest
          extended: false

      - name: Build
        working-directory: ./Website
        run: hugo

      - name: Deploy to Firebase
        uses: w9jds/firebase-action@master
        with:
          args: deploy --only hosting
        env:
          FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
          PROJECT_PATH: ./Website
          PROJECT_ID: amithgc-stories
```


---

## Conclusion
And so, our adventure through the realms of imagination comes to an end. We embarked on a quest to build an automated website that generates captivating children's stories, and oh, what a magical journey it has been!

From Java incantations to summoning the powers of OpenAI's GPT Model, we embraced the wonders of technology to create stories that ignite the minds of young readers. With the assistance of leonardo.ai or the mystical Dall-E, we conjured vivid images that danced alongside our tales, painting a picture of pure wonder.

But it wasn't just about the code and algorithms; it was about the magic of storytelling itself. We weaved narratives that transported children to distant lands, introduced them to extraordinary characters, and kindled their imaginations. Each story was a key to unlock the door to a world where dreams take flight.

Through GitHub Actions and Firebase, we automated our storytelling process, freeing ourselves from manual labor and embracing the power of digital enchantment. Day by day, our website flourishes with new stories and captivating visuals, a testament to the wonders that technology can bring.

In this journey, we've learned that with a dash of Java, a sprinkle of AI, and a touch of humor, we can create a symphony of stories that captivate and inspire. The power to spark joy and ignite imagination lies within our hands.

So, my fellow sorcerers of storytelling, let us continue to wield our technological wands with care and creativity. May our automated website continue to delight children, opening doors to the realms of magic and wonder. And remember, the stories we create today may become the cherished memories of tomorrow.

Now, go forth and let the world be entranced by the tales that emerge from your automated website. Unleash the power of imagination, one story at a time. Happy storytelling, and may your adventures never cease!

With a twinkle in our eyes and a heart full of whimsy, we bid you farewell on this extraordinary journey.

*Until we meet again, in the land of stories.*