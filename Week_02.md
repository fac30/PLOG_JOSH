## Guidance
Answer the following questions considering the learning outcomes for
- [Week 02](https://learn.foundersandcoders.com/course/syllabus/developer/week02-project02-chatbot/learning-outcomes/)

Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of some of the learning outcomes you have achieved this week.
> **Write tests to mimic the behaviour of a user performing different actions**  
> I wrote some tests for our Bot. The idea was to have seperate scripts that tested a specific function.

```javascript
 async function testChatCompletion(prompt) {
  try {
    const response = await openai.chat.completions.create({
      model: "gpt-3.5-turbo",
      messages: [
        { role: "system", content: "You are a helpful assistant." }, //Sets the AI's persona as a "helpful assistant."
        { role: "user", content: prompt } //User message defined in runTests.js
      ]
    });
 ```
I learned about asynchronous functions that wait for the response from the API before continuing execution.

This test is run by a seperate 'runTest' function

```javascript
  const testCases = [
    { prompt: "What is the capital of Mexico?", expectedAnswer: "Mexico City" },
    { prompt: "What is the largest planet in our solar system?", expectedAnswer: "Jupiter" }
  ];

  // Iterate over each test case
  for (const { prompt, expectedAnswer } of testCases) {
    try {
      console.log(`Testing prompt: "${prompt}"`);
      const response = await testChatCompletion(prompt);
      console.log(`Response: ${response}`);
      console.log(`Expected Answer: ${expectedAnswer}`);

      // Optionally, check if the response contains the expected answer
      if (response.includes(expectedAnswer)) {
        console.log(`Test passed\n`);
      } else {
        console.log(`Test failed for prompt: "${prompt}". Expected to include: "${expectedAnswer}"\n`);
      }
    } catch (error) {
      console.error(`Error testing prompt: "${prompt}":`, error.message);
    }
  }
```

I have since learned better and more elegant ways to test through the workshops this week.


**Making API calls**  
I learned how powerful having the ability to send and recieve data from APIs. From sending and recieving conversations to the openAi API to sending search terms to the Giphy API and recieving back Gifs based on those terms.

```javascript
async execute(message) {
    // Get the search term from the user's command input (args)
    const searchTerms = ["face palm", "eye roll", "fed up"];
    const searchTerm =
      searchTerms[Math.floor(Math.random() * searchTerms.length)];

    // Construct Giphy API URL
    const url = `https://api.giphy.com/v1/gifs/random?api_key=${
      config.giphyApiKey
    }&tag=${encodeURIComponent(searchTerm)}&rating=G`;

    try {
      // Fetch a GIF from Giphy
      const response = await fetch(url);
      const data = await response.json();
```
**Preparing and sending the message to the OpenAI API:**
```javascript
async function sendResponse(message, content, userId, isDM) {
  const systemPrompt = {
    role: 'system',
    content: "You're an irritable, sarcastic and rude code helper..." // Defines the assistant's behavior
  };

  // Initialize conversation history if it doesn't exist for this user
  if (!conversationHistories[userId]) {
    conversationHistories[userId] = [systemPrompt];
  }

  // Add the user's message to the conversation history
  conversationHistories[userId].push({ role: "user", content });

  try {

    await message.channel.sendTyping();  // Indicate the bot is typing
    const response = await generateChatResponse(conversationWindow);  // Call the OpenAI API
```

**Handling and sending the response back to the user:**
```javascript
    conversationHistories[userId].push({
      role: "assistant",
      content: response,
    });

    // Send the response back to the user
    if (isDM) {
      await message.author.send(response);  // Send in direct message
    } else {
      await message.channel.send(response);  // Send in the current channel
    }
    console.log("Response sent successfully.");
  } catch (error) {
    console.error("Error during message handling:", error);
    message.channel.send(
      "Sorry, I encountered an error while generating a response."
    );
  }
}
```

 ### 2. Show an example of some of the learning outcomes you have struggled with and/or would like to re-visit.
> [**Learning outcome...**]  
Being a scrum master. Working with dotEnv and our config file caused me issues and I ended up spending a lot of time trying to solve them than I would have liked.

## Feedback (For CF's)
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
