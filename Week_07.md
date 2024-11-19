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

<details><summary><strong>DevOps(maybe)</strong></summary>

---
Last week I mentioned I took a Devops role but I think I am refering to something different. What I meant was It was my role to get the backend set up and all dependancies and packages installed and planned how the backend would be communicating with the front end. 

This week I expanded on my function that handles quesries so that it could POST as well as GET data 

```ts
const fetchData = async (
  table: string,
  method: string,
  body?: any, 
): Promise<any> => {
  try {
    const response = await fetch(`http://localhost:3000/${table}`, {
      method: method,
      headers: {
        "Content-Type": "application/json",
      },
      body: method === "POST" ? JSON.stringify(body) : null, 
    });

    if (!response.ok) {
      throw new Error(`Error: ${response.status}`);
    }

    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Error fetching data:", error);
    throw error;
  }
};

export { fetchData };
```

And this can be called like this

```ts
 const handleSubmit = async (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    await fetchData("register", "POST", await createUserObject());
  };
```
This function will need to be renamed for readability
</details>

<details><summary><strong>Authentication</strong></summary>

---
We decided to handle password hashing on ourr front end. I found it easiest to do this by breaking the task down into steps to make it easier for me to understand. I did this by storing the users details into a object including the hashed password, which was generated using the hashPassword function

```ts
  const createUserObject = async (): Promise<UserObject> => {
    const { confirm_password, password, ...userObject } = formData;
    userObject.password_hash = await hashPassword(password);
    return userObject as UserObject;
  };
```

This object then gets sent to our backend using the function stated in the previous section

```ts
await fetchData("register", "POST", await createUserObject());
      setIsSuccess(true);
      setFormData(INITIAL_FORM_STATE);
    } catch (error) {
      console.error("Registration failed:", error);
    }
```

I'm sure this task could be handled in fewer steps, but when we decided to hash the password before storing it, this method felt easiest forr me to write. Below is how the password is being hashed and salted

```ts
import bcrypt from "bcryptjs";

const hashPassword = async (password: string): Promise<string> => {
  const saltRounds = 12;
  const hash = await bcrypt.hash(password, saltRounds);
  return hash;
};

export default hashPassword;
```

</details>



## 2. Difficulties

<details><summary>Toggle List</summary>

---
I previously felt like I was getting more confident using Typescript, but in this project so farr it has been a bit of a struggle for me. Using it with React feels like a bit of a pain, and often quite confusing. I'm feeling like im using ChatGpt more than I would like to to figure out why my code isn't working, and it quite often comes down to type issues.

</details>



### Additional

---

Overall I am happy with my progress this week. I've found working on personal projects over the weekend has really helped me grasped some concepts and I'm feeling more confident to start working on freelance work now.

</details>

[Facilitator]
Alexander

[What went well]
Strong systematic approach to debugging the SQLite implementation with detailed logging. Good modular design of the fetchData function for handling different HTTP methods. Clear breakdown of authentication process with password hashing.

[Even better if]
Document specific TypeScript/React issues you're encountering instead of just mentioning general struggles. Since you're using bcrypt on frontend, discuss the security implications of this architectural decision.
