# Week : 4

- [Learning Outcomes](https://learn.foundersandcoders.com/course/syllabus/developer/week03-project03-server/learning-outcomes/)

## 1. Achievements

<details><summary><strong>Understanding The Link Between Front & Back end</strong></summary>

---

Going into the week I didn't really understand how we were going to link our front end to our back end. I was working from home and was assigned the task of creating a feature that generated a random fact about the seelected country.

I initially didn't even know where to start but I was deteremined to figure it out without help from my team or course facilitator.

I started off by writing an external endpoint in the backend code.

``` ts
const { getOpenAIReponse } = require("./openAI-handling"); 

async function getRandomFact(req, res) {
  const country = req.body.country; 
  if (!country) {
    return res.status(400).json({ error: "Country is required" });
  }

  try {
    const fact = await getOpenAIReponse(country); 
    res.json({ fact });
  } catch (error) {
    console.error("Error getting random fact:", error);
    res.status(500).json({ error: "Failed to fetch random fact" });
  }
}

```
This will extract the country name from the value of the request body. It then calls the getOpenAIReponse function with the country as an argument. The returned value is stored in the fact variable.

This functionality is exported as 'getRandomFact' and then posted to the server. 
```ts
app.post("/random-fact", getRandomFact);
```

The way I have come to understand it, is I am creating a 'website' that this functionality lives on that the front end will then 'visit' and send/recieve values.

This is done like this (more on my use of POST in the next achievement . . .)
```ts
  const fetchCountryFact = async (country: string) => {
    try {
      const response = await fetch(`http://localhost:3000/random-fact`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ country }),
      });

      if (!response.ok) {
        throw new Error("Network response was not ok");
      }

      const data = await response.json();
      setCountryFact(data.fact); //set countryFact state to data recieved from backend
    } catch (error) {
      console.error("Error fetching country fact:", error);
    }
  };
```

This is sending the "countrry" value to our server address and recieving back the fact that is set to the countrFact state.


</details>

<details><summary><strong>POST vs GET</strong></summary>

---
I learrned the appropiate times to use POST and when to use GET. In my examples above I initially use app.post because I am making changes to m server to set up the address for my get-fact function. I should have then used GET with my front end as whilst I am sending information, I am not changing anything on my server and I expect data back.

</details>

<details><summary><strong>Spread Operators</strong></summary>

---
I need to do some more reading into them, but from what I understand spread operators allow us to copy objects and arrays, and pass props more conveniently. 

</details>



## 2. Difficulties

<details><summary>Getting Started On Tasks</summary>

---
My biggest challenge sometimes is getting started on tasks. I get overwhelmed with how the logic will work and it can sometimes take a while to get going. This week it was the above mentioned roadblock with how the frontend communicated with the backend.


</details>
<details><summary>Tailwind</summary>

---

I wasn't a huge fan of tailwind to begin with. I prefer to look at a css stylesheet as I feel like I can see everything a bit clearer. I will make more of an effort to get used to using it as I can see the benifits of using tailwind as opposed to traditional CSS.

</details>

## 3. Full Progress List

<details><summary>Toggle Key</summary>

---

</details>



## 4. Feedback

Alexander

### What went well

It is great that you found out how BE-FE interact.

### Things to improve

For this week I would also like to see some React specific content
