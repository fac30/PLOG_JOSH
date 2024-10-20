# Week : 

- [Learning Outcomes](https://learn.foundersandcoders.com/course/syllabus/developer/week03-project03-server/learning-outcomes/)

## 1. Achievements

<details><summary><strong>SQL</strong></summary>


---
I had a little bit of experience working with SQL prior to this week, but the workshop and Jason's presentation really opened my mind to how it can be used efficiently. While I do think we went a bit overboard on our schema, the feedback we received and seeing other people's presentations has made it clear to me how it could be refined going forward.

I struggled a bit with the workshop, but I went over it again, and it became clearer how SQL can be used in functions to easily manipulate our tables and modify data in them.

</details>

<details><summary><strong>DevOps</strong></summary>

---
I took on a different role in our project than I usually do, and my task was to set up the project and install all the necessary packages for our backend. I wasn’t very confident since I hadn’t done this before, but I was eager to gain experience. I faced some issues with installing the packages and dependencies, which taught me the importance of planning and discussing our needs with the team before getting started.

</details>

<details><summary><strong>Database Logic</strong></summary>

---
I wrote much of the backend code, which handles the server logic and retrieves data from our database. I aimed to keep the code concise in order to maintain organization and readability. The vinyl data is fetched from our database and sent to our server.

Vinyl Data:
```ts
interface Vinyl {
  id: number;
  stock: number;
  description: string;
  price: number;
  artist: string;
  title: string;
  release_date: string;
  limited_edition: boolean;
  new_release: boolean;
  discount: number;
  on_sale: boolean;
  genre: string;
  condition: string;
  price_range: string;
  album_or_single: string;
  time_range: string;
  label: string;
}

const dbRequest = async (): Promise<Vinyl[]> => {
  const { data } = await supabase.from("vinyls").select("*");

  return data || [];
};

export default dbRequest;

```
main.ts
```ts
app.get("/vinyls", async (req: Request, res: Response) => {
  try {
    const vinyls = await dbRequest(); 
    res.status(200).json(vinyls); 
  } catch (error) {
    console.error(error);
    res.status(500).json({ message: "Error fetching vinyl data" }); 
  }
});
```
It was great to have the opportunity to implement this, as I didn’t get much chance to set up this logic in previous projects.

I also wanted to keep the logic that communicates with the backend as clean and modular as possible. My idea was to build a dynamic "fetch data" function that can be called to dynamically fetch the data we need, whether it's customer data or product data.

```ts
const fetchData = async (table: string, method: string): Promise<any> => {
  try {
    const response = await fetch(`http://localhost:3000/${table}`, {
      method: `${method}`,
      headers: {
        "Content-Type": "application/json",
      },
    });

    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Error fetching data:", error);
    throw error;
  }
};

export { fetchData };
```

At the moment, this is only designed with fetching vinyl data in mind, but I'd like to expand it so it can be used for adding data and fetching customer info.

</details>





## 4. Feedback


