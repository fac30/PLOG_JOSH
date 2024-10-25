# Week : 

- [Learning Outcomes](https://learn.foundersandcoders.com/course/syllabus/developer/week03-project03-server/learning-outcomes/)

## 1. Achievements

<details><summary><strong>SQL</strong></summary>

---

We decided to use Supabase for our database, which works differently from SQLite that we had learned in the workshop. I wanted to make sure I could write code in SQL and utilse SQLite, so I did some work on a personal project. The idea was to create a simple user table that stores a user's details when they sign up.

``` js
export const signup = async (req, res) => {
  const { email, password } = req.body;

  try {
    const userId = await createUser(email, password); // Hashing occurs in createUser
    res.status(201).json({ message: "User created successfully", userId });
  } catch (error) {
    console.error("Error creating user:", error);
    res.status(500).json({ message: "Internal server error" });
  }
};
```
```js
const createUser = async (email, password) => {
  try {
    const hashedPassword = await bcrypt.hash(password, 10); // Hash the password
    const query = "INSERT INTO users (email, hashed_password) VALUES (?, ?)";

    const stmt = db.prepare(query);
    const body = stmt.run(email, hashedPassword);
    console.log("User created successfully with ID:", body.lastInsertRowid);
    return body.lastInsertRowid;
  } catch (err) {
    console.error("Error creating user:", err.message); // Log specific error message
    throw new Error("Database error"); // Throw a custom error
  }
};
```

Once I wrote my code, I used Postman to test if it worked and could insert the data into the table. I got a message saying it was successful, but the data wasn't added to the table.
I decided to add console logs at every step to try and determine where the issue was coming from:

```js
const createUser = async (email, password) => {
  console.log('Attempting to create user with email:', email); // Debug log

  const hashedPassword = await bcrypt.hash(password, 10);
  console.log('Password hashed successfully'); // Debug log

  const query = "INSERT INTO users (email, hashed_password) VALUES (?, ?)";
  
  try {
    const stmt = db.prepare(query);
    console.log('Statement prepared'); // Debug log
    
    const body = stmt.run(email, hashedPassword);
    console.log('Insert operation completed with result:', body); // Debug log
    console.log("User created successfully with ID:", body.lastInsertRowid);
    
    // Verify the insert worked
    const verifyStmt = db.prepare('SELECT * FROM users WHERE id = ?');
    const inserted = verifyStmt.get(body.lastInsertRowid);
    console.log('Verified inserted user:', inserted);
    
    return body.lastInsertRowid;
  } catch (err) {
    console.error("Error creating user:", err);
    console.error("Error details:", err.message); // More error details
    throw err;
  }
};
```

After running this, I found the issue was that the process.env.DB_FILE was undefined. I wasn't aware you needed a .env file. I still want to spend some time with SQLite and intend to make some more complex tables and functions.

</details>

<details><summary><strong></strong></summary>

---

</details>

<details><summary><strong></strong></summary>

---

</details>



## 2. Difficulties

<details><summary>Toggle List</summary>

---

</details>

## 3. Full Progress List

<details><summary>Toggle Key</summary>

---

</details>

<details><summary>Toggle List</summary>

---

### TypeScript & Express

---

### RESTFUL APIs

---

### Additional

---

</details>
