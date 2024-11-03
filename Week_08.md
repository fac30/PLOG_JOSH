# Week : 

- [Learning Outcomes](https://learn.foundersandcoders.com/course/syllabus/developer/week03-project03-server/learning-outcomes/)

## 1. Achievements

<details><summary><strong>Deployment</strong></summary>

---
After the workshop i decided to watch some youtube tutorials on deployment  to get a better idea of how I could apply what I learned in rreal world situations. I feel the workshop was good but very easy to complete without really knowing what you aree doing if you dont make an effort to do extra reading. Although I didn't handle the deployment of our group project as Marika was quite keen on deploying our site, I hope to get some pactice over reading week on a project I have been working on.

</details>

<details><summary><strong>Product Filtering</strong></summary>

---
I really wanted to implement product filtering this week so it was something that I focused on for most of tuesday. I achieved this by creaeting a function that iterates through each vinyl record and creates a new array with all elements that pass the checks.

```ts
      const filtered = vinyls.filter(
        (vinyl) =>
          (!genres.length || genres.includes(vinyl.genres.genre)) &&
          (!priceRanges.length ||
            priceRanges.includes(vinyl.price_ranges.price_range)) &&
          (!timePeriods.length ||
            timePeriods.includes(vinyl.time_periods.time_period)),
      );

```


</details>

<details><summary><strong>Responsive Design</strong></summary>

---

Up until this point our site had been unresponsive and had a lot of issues in mobile view. I took some time out this week to go through and ensure everrything displayed propely in mobile view. It turned out to be quite easy in Tailwind with the "lg:" or "sm:" which adds styling deependant on the display size

```ts
<div className="w-full grid grid-cols-2 lg:grid-cols-4 gap-6 min-h-[500px]">
```

</details>



## 2. Difficulties

<details><summary>Toggle List</summary>

---
A log out function seemed like it would be pretty easy to implement, but ended up giving me issues to try and add. 

in theory I would be using myfunction  that handled DB requests to delete the user session

```ts
const handleLogout = async () => {
    try {
      await fetchData("check-session", "DELETE");
    } catch (error) {
      console.error("Error logging out:", error);
    }
  };
```

However this was returning autherisation errors that we were unable to solve in time by the end of the week

</details>



## 4. Feedback


