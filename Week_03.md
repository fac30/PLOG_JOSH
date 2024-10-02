## Guidance
Answer the following questions considering the learning outcomes for
- [Week 03](https://learn.foundersandcoders.com/course/syllabus/developer/week03-project03-server/learning-outcomes/)

Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of some of the learning outcomes you have achieved this week.

 
Here's your text with the spelling mistakes corrected, while preserving the original code and structure:

---

This week, my biggest "aha" moment came on Thursday, as I felt it was a moment when I could really visualise how our program was interacting with the APIs and our database. It was my job to set up the server, and admittedly I was a bit unsure whether I fully understood what I was doing, as I felt like I was perhaps relying on Jack's help. But by Thursday, I had implemented a couple of relatively simple features that, while writing them, made me really get a better understanding of how our code was wrking.

Firstly, my function sends a prompt to OpenAI, passing in two variables using string interpolation. `country1` from our `getRandomCountry` function that utilizes our database, and `country2` from the user's input using a POST request.

```typescript
async function getDistance(country: string, country2: string) {
  const completion = await openai.chat.completions.create({
    messages: [
      {
        role: "system",
        content: `What is the distance between ${country} and ${country2} in km? Do not send any text other than the fact (e.g. sure!, can do! or ok!). Only refer to the country as 'this country'.`,
      },
    ],
    model: "gpt-4o",
  });

  return completion.choices[0].message.content;
}

module.exports = {
  getOpenAIResponse,
  getDistance,
};
```

## country1
```typescript
const myRandomCountryObject = await getRandomCountry(database);
currentCountry = myRandomCountryObject.country; // Store the country globally
```

## country2
```typescript
app.post("/answer", async (req: any, res: any) => {
  // Extract the user's answer from the request body
  const userAnswer = req.body.answer;
```

---

That function is called and displayed to the user in our `index.ts` file:

```typescript
const distance = await getDistance(currentCountry, userAnswer);

// Update the score based on whether the user's answer was correct
handleScoreChange(isCorrect);

// Send a response indicating whether the answer was correct, along with the correct answer, distance, and user's score
res.json({
  isCorrect, // Whether the user's guess was correct
  correctAnswer: currentCountry, // The correct country
  yourGuessDistance: `Your guess was ${distance} from the correct location`, // Dynamic message with the distance
  userScore, // The user's current score
});
```

---

While it's quite simple, implementing this really made me learn the code and the functionality of our server.

### 2. Show an example of some of the learning outcomes you have struggled with and/or would like to revisit.

This week, I don't feel I struggled with anything in particular mainly just getting used to the new syntax, but I would like to delve a little bit deeper into using databases.

Something that has helped me visualise how everything works in this project was to look at it like audio engineering. Our index file works like a mixing desk, and importing, exporting, and making API calls work like sending audio to external equipment to be processed or receiving a signal from an external source, etc. Probably a weird way to look at it but it has helped with this project and also understanding how React works.

---


## Feedback (For CF's)
> [**Course Facilitator name**]

Alexander

> [*What went well*]

Very good code snippets, you covered the most important learnings for this week.

> [*Even better if*]

I wont change much. I would touch a few more topics to make it more complete, but it is fine as it is.
You can have a peak to Jason's, it is a great example of a very complete PLog.
