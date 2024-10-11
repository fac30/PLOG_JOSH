
# Week:

- [Learning Outcomes](https://learn.foundersandcoders.com/course/syllabus/developer/week03-project03-server/learning-outcomes/)

## 1. Achievements

<details><summary><strong>Refactoring Code</strong></summary>

---

This week was mostly spent refactoring our code and building some tests. I spent an hour or so adding unique data-test IDs to every element in our game, which at the time was a bit of a pain, but turned out to be worth it as I noticed other teams had struggled with selecting elements using CSS class names, etc.

```js
cy.get('[data-test="current-country"]').then(($currentCountry)
```

This code could have been made even cleaner by declaring 'current-country' at the top of my code, similar to what Jason showed in his team's presentation, to avoid having to type out '[data-test="current-country"]' every time.

I also went through and ensured all of our code was TypeScript compliant. This mostly consisted of adding TypeScript interfaces.

```typescript
interface CountryGroupProps {
  "data-test": string;
  key: number;
  index: number;
  countryName: string;
  pathsArray: string[];
}
```

</details>

<details><summary><strong>Writing Tests</strong></summary>

---

Writing tests has been something I've been quite interested in since I started coding.

I wanted to figure out how to write a test that checked the logic for when a user made a correct/incorrect guess. This would require my code to make Cypress get the current score, get the current country name so it could click on the correct country, and then compare the score after clicking the country to the initial score.

```cy
  it(`Tests that user score increments when guessed correctly.`, () => {

    cy.get('[data-test="user-score"]').then((currentScore) => {
      const initialScore = currentScore.text().trim();

      cy.get('[data-test="current-country"]').then((currentCountry) => {
        const countryText = currentCountry.text().trim();
        cy.get(`[data-test="${countryText}"]`).click();
      });

      cy.get('[data-test="user-score"]').should((newScore) => {
        const updatedScore = newScore.text().trim();
        expect(updatedScore).to.not.equal(initialScore);
      });
    });
  });
```

Initially, the test wouldn't work, and when I was troubleshooting each line of code using console logs to see where the issue was, I noticed that this line was returning an empty string instead of the country name:

```cy
cy.get('[data-test="current-country"]')
```

It took a little while, but I figured that line must have been executing before the country name was rendered. I found a Cypress method called 'cy.wait' that allowed me to make my test wait a short time before executing.

```cy
it(`Tests that user score increments when guessed correctly.`, () => {
    cy.wait(2000);

    cy.get('[data-test="user-score"]').then((currentScore) => {
      const initialScore = currentScore.text().trim();

      cy.get('[data-test="current-country"]')
```

</details>

<details><summary><strong>Confidence In My Code</strong></summary>

---

There was something Alphonso said in his talk last week about trusting your choices/coding ability, and it made me realize I wasn't overly confident. I wanted to spend this week writing as much code as I could without relying on ChatGPT. Everything took a lot longer, but I think in doing so I feel a lot better about my abilities.

</details>

## 2. Difficulties

<details><summary>AWS</summary>

---

AWS's interface seemed straightforward enough to me, but a lot of what Jack was doing and showing me this week really went over my head. I'm keen to maybe in the next project get a bit more hands-on experience with this.

</details>

## 4. Feedback
```

Let me know if you'd like to make any further changes!
