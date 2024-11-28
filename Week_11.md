## Guidance
Answer the following questions considering the learning outcomes for
- [Week 011](https://learn.foundersandcoders.com/course/syllabus/developer/week11-project05-DOTNET-testing/learning-outcomes/)

Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
I struggled quite a bit this week. I found it hard to get any momentum as I had a lot going on outside of FAC which meant I had to take a day off and struggled with getting my head around .NET. My team are very proactive and I felt the project moving along way quicker than I had a chance to properly settle in and write some meaningful code. 

I was hoping to write some tests using Xunit, but the version of some of the packages it required me to have were breaking other parts of the project. It also didn't help that I couldn't get postgres installed on my system. I felt I wasted most of Monday messing about with that before giving up and refarctoring the code I wrote the previous week for our dbcontext file.

The idea was to use snakeNamingConventions to clean up this code.

```csharp
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<Comment>().ToTable("comment");
        modelBuilder.Entity<Collection>().ToTable("collection");
        modelBuilder.Entity<ColourCollection>().ToTable("colour_collection");
        modelBuilder.Entity<Colour>().ToTable("colour");
        modelBuilder.Entity<User>().ToTable("user");

        modelBuilder.Entity<ColourCollection>().HasKey(cc => new { cc.CollectionId, cc.ColourId });
    }
```

However because our database tables were named with singular titles, when I made the changes and pushed to our repo, it broke our site, so we reverted back.

I also used Tuesday to implement a functional search bar on our site using React context. I really enjoyed this but it got made redundant as the project bacame more complex. 

Overall I'm not overly happy with the input I had and will maybe spend some time in the future building something with .NET and C# for some more practice 

## Feedback (For CF's)
> [**Course Facilitator name**]

Alexander

> [*What went well*]  

I think that you did great with the time that you had. It is not so much about the specific learnings, but to get the basics and broad ideas. You may not be able to build a model by heart (is that even important), but you understand the technology and, if you need to work in a .NET project, where to look for resources/examples.
